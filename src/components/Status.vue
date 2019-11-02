<template>
  <div>
    <v-form ref="form" v-model="valid" lazy-validation>
      <v-row class="pa-0 ma-0" align="center">
        <v-combobox
          v-model="receiver"
          :rules="[validateReceiver]"
          :items="loadSuggestItems()"
          label="To Address"
          required
          hide-no-data
          clearable
        ></v-combobox>
        <v-btn color="primary" :disabled="valid === false" @click="search">Search</v-btn>
      </v-row>

      <v-container v-if="verifiedReceiver" class="py-0">
        <v-switch
          v-model="isAutoUpdate"
          class="ma-0 py-0"
          dense
          label="Enable Auto Update (every 10s)"
          @click="enableAutoUpdate"
        ></v-switch>
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
import { validateAddress, loadReceivers } from "./common/Utils";
import { ethToAergo, utils, aergoToEth } from "eth-merkle-bridge-js";
import { AergoClient, GrpcWebProvider } from "@herajs/client";
import Web3 from "web3";

export default {
  name: "Status",
  components: {
    //
  },
  props: ["fromBridge", "toBridge"],
  data: () => ({
    receiver: "",
    receiverRules: [v => !!v || "Address is required"],
    valid: false,
    verifiedAmount: "-",
    underVerifyAmount: "-",
    nextVerifyBlock: "-",
    verifiedReceiver: null,
    updateTime: null,
    isAutoUpdate: false,
    autoUpdateIntervalId: null
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
    enableAutoUpdate() {
      if (this.isAutoUpdate) {
        this.autoUpdateIntervalId = setInterval(() => {
          this.search();
        }, 10000);
      } else if (this.autoUpdateIntervalId) {
        clearInterval(this.autoUpdateIntervalId);
      }
    },
    validateReceiver(v) {
      if (this.toBridge) {
        return validateAddress(this.toBridge.net.type, v);
      } else {
        return true;
      }
    },
    search() {
      if (this.$refs.form && this.$refs.form.validate()) {
        var withdrawStatuseQuery;
        var anchorStatusQuery;
        if (
          this.fromBridge.net.type === "ethereum" &&
          this.toBridge.net.type === "aergo"
        ) {
          let herajs = new AergoClient(
            {},
            new GrpcWebProvider({ url: this.toBridge.net.endpoint })
          );

          let web3Full = new Web3(
            new Web3.providers.HttpProvider(this.fromBridge.net.endpoint)
          );
          withdrawStatuseQuery = ethToAergo.unfreezeable(
            web3Full,
            herajs,
            this.fromBridge.contract.id,
            this.toBridge.contract.id,
            this.receiver,
            this.fromBridge.asset.id
          );

          anchorStatusQuery = utils.getEthAnchorStatus(
            web3Full,
            herajs,
            this.toBridge.contract.id
          );
        } else if (
          this.fromBridge.net.type === "aergo" &&
          this.toBridge.net.type === "ethereum"
        ) {
          let herajs = new AergoClient(
            {},
            new GrpcWebProvider({ url: this.fromBridge.net.endpoint })
          );

          let web3Full = new Web3(
            new Web3.providers.HttpProvider(this.toBridge.net.endpoint)
          );

          withdrawStatuseQuery = aergoToEth.unlockeable(
            web3Full,
            herajs,
            this.toBridge.contract.id,
            this.fromBridge.contract.id,
            this.receiver,
            this.toBridge.asset.id
          );

          anchorStatusQuery = utils.getAergoAnchorStatus(
            web3Full,
            herajs,
            this.toBridge.contract.id
          );
        }

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
    },
    loadSuggestItems() {
      return loadReceivers();
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