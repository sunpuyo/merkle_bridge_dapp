<template>
  <div>
    <v-form ref="form" v-model="valid" lazy-validation>
      <v-row class="pa-0 ma-0" align="center">
        <v-text-field
          v-model="receiver"
          :rules="[validateReceiver]"
          prepend-inner-icon="mdi-account"
          label="To Address"
          required
          clearable
        ></v-text-field>
        <v-btn color="primary" text @click="receiver = sharedReceiver">Load</v-btn>
        <v-btn color="primary" :disabled="valid === false" @click="search">Search</v-btn>
      </v-row>
      <v-container v-if="verifiedReceiver">
        <v-row class="title">Bridge Status ({{updateTime}})</v-row>
        <v-row class="body-1">{{verifiedReceiver}}</v-row>
        <v-row>
          <v-col cols="5">
            <v-card class="my-2" sm="1">
              <v-icon>mdi-sack</v-icon>
              <v-icon large>mdi-bank-transfer-in</v-icon>
              <br />
              <span
                :class="(underVerifyAmount !== '0' ? 'blinking': '') + ' display-1 font-weight-bold lime--text'"
              >{{underVerifyAmount}}</span>
              <br />
              <span class="subtitle-1 grey--text">Erc20 Aergo</span>
              <v-divider class="mx-4"></v-divider>
              <span class="caption">Under Verification</span>
            </v-card>
          </v-col>
          <v-col cols="2">
            <v-card class="my-2" sm="1">
              <v-icon large>mdi-calendar-clock</v-icon>
              <br />
              <span class="display-1 font-weight-bold red--text blinking">{{nextVerifyBlock}}</span>
              <br />
              <span class="subtitle-1 grey--text">Blocks</span>
              <v-divider class="mx-4"></v-divider>
              <span class="caption">Next Verification</span>
            </v-card>
          </v-col>
          <v-col cols="5">
            <v-card class="my-2" sm="1">
              <v-icon large>mdi-weather-cloudy-arrow-right</v-icon>
              <br />
              <span class="display-1 font-weight-bold green--text">{{verifiedAmount}}</span>
              <br />
              <span class="subtitle-1 grey--text">Arc1 Aergo</span>
              <v-divider class="mx-4"></v-divider>
              <span class="overline">Verified</span>
            </v-card>
          </v-col>
        </v-row>
      </v-container>
      <v-btn
        color="primary"
        :disabled="(valid === false || verifiedAmount === '-' || verifiedAmount === '0')"
        @click="clickNext"
      >Continue</v-btn>
      <v-btn text @click="clickBack">Back</v-btn>
    </v-form>
  </div>
</template>

<script>
import { validateAddress } from "./Commons";
import { ethToAergo, utils } from "eth-merkle-bridge-js";
import { AergoClient, GrpcWebProvider } from "@herajs/client";
import Web3 from "web3";

export default {
  name: "Status",
  components: {
    //
  },
  props: ["fromBridge", "toBridge", "sharedReceiver"],
  data: () => ({
    receiver: "",
    receiverRules: [v => !!v || "Address is required"],
    valid: false,
    verifiedAmount: "-",
    underVerifyAmount: "-",
    nextVerifyBlock: "-",
    verifiedReceiver: null,
    updateTime: null
  }),

  methods: {
    reset() {
      this.verifiedReceiver = null;
this.verifiedAmount = "-";
      this.underVerifyAmount = "-";
    },
    clickNext() {
      if (this.$refs.form.validate()) {
        this.$emit(
          "update_finalize_info",
          this.verifiedReceiver,
          this.verifiedAmount
        );
        this.reset();
        this.$emit("stepping", "next");
      }
    },
    clickBack() {
      this.reset();
      this.$refs.form.resetValidation();

      this.$emit("stepping", 1);
    },
    validateReceiver(v) {
      if (this.toBridge) {
        return validateAddress(this.toBridge.net.type, v);
      } else {
        return true;
      }
    },
    search() {
      if (this.$refs.form.validate()) {
        let herajs = new AergoClient(
          {},
          new GrpcWebProvider({ url: this.toBridge.net.endpoint })
        );

        let web3Full = new Web3(
          new Web3.providers.HttpProvider(this.fromBridge.net.endpoint)
        );

        let withdrawStatuseQuery = ethToAergo.unfreezeable(
          web3Full,
          herajs,
          this.fromBridge.contract.id,
          this.toBridge.contract.id,
          this.receiver,
          this.fromBridge.asset.id
        );

        let anchorStatusQuery = utils.getEthAnchorStatus(
          web3Full,
          herajs,
          this.toBridge.contract.id
        );

        Promise.all([withdrawStatuseQuery, anchorStatusQuery])
          .then(results => {
            this.updateTime = new Date().toLocaleString();
            // verified asset info
            this.verifiedReceiver = this.receiver;
            this.verifiedAmount = results[0][0];
            this.underVerifyAmount = results[0][1];

            // expected anchoring block height
            this.nextVerifyBlock =
              results[1].lastAnchorHeight +
              results[1].tAnchor +
              results[1].tFinal -
              results[1].bestHeight;
          })
          .catch(errs => {
            if (errs[0]) {
              alert(errs[0]);
            } else if (errs[1]) {
              alert(errs[0]);
            }
          });
      }
    }
  }
};
</script>


<style>
.blinking {
  animation: blinkingText 3s infinite;
}
@keyframes blinkingText {
  50% {
    color: transparent;
  }
}
</style>