<template>
  <div v-if="bridge">
    <v-list dense>
      <v-list-item class="pa-0">
        <v-list-item-icon class="mr-2">
          <v-icon>mdi-sack</v-icon>
        </v-list-item-icon>
        <v-list-item-content class="text-left">
          <v-list-item-title>Asset Name</v-list-item-title>
          {{bridge.asset.label}}
        </v-list-item-content>
        <v-list-item-content class="text-left" v-show="bridge.asset.id">
          <v-list-item-title>Asset Contract ID</v-list-item-title>
          {{bridge.asset.id}}
        </v-list-item-content>
        <v-btn v-clipboard="bridge.asset.id" icon v-show="bridge.asset.id">
          <v-icon>mdi-content-copy</v-icon>
        </v-btn>
        <v-btn
          v-if="bridge.asset.id"
          icon
          :href="bridge.net.scan + bridge.asset.id"
          target="_blank"
        >
          <v-icon>mdi-launch</v-icon>
        </v-btn>
      </v-list-item>
      <v-list-item class="pa-0">
        <v-list-item-icon class="mr-2">
          <v-icon>mdi-bank</v-icon>
        </v-list-item-icon>
        <v-list-item-content class="text-left">
          <v-list-item-title>Bridge Contract ID</v-list-item-title>
          {{bridge.contract.id}}
        </v-list-item-content>
        <v-btn v-clipboard="bridge.contract.id" icon>
          <v-icon>mdi-content-copy</v-icon>
        </v-btn>
        <v-btn icon :href="bridge.net.scan + bridge.contract.id" target="_blank">
          <v-icon>mdi-launch</v-icon>
        </v-btn>
      </v-list-item>
    </v-list>

    <!-- display logined wallet info -->
    <v-form ref="form" v-model="valid" lazy-validation>
      <v-text-field
        ref="textField"
        v-model="wallet.address"
        label="From Address"
        :rules="[validateAccount]"
        disabled
        required
        :class="wallet.isLogin?'':'errored--disable-textfield'"
      >
        <template v-slot:prepend>
          <v-img
            v-if="wallet.type === 'aergo'"
            :src="require('../assets/aergoicon.png')"
            width="24"
          ></v-img>
          <v-img
            v-else-if="wallet.type === 'ethereum'"
            :src="require('../assets/metamask.png')"
            width="24"
          ></v-img>
        </template>
      </v-text-field>

      <v-text-field
        v-model="nextVerify"
        :rules="nextVerifyRules"
        label=" Next Verification Time (Estimated)"
        required
        disabled
        :class="isTimeOk?'':'errored--disable-textfield'"
      ></v-text-field>
      <div v-if="inout === 'in'">
        <v-text-field
          v-model="receiver"
          :rules="[validateReceiver]"
          :label="'To Address (' + toBridge.net.label + ')'"
          required
          clearable
        ></v-text-field>
        <v-text-field v-model="amount" :rules="amountRules" label="Amount" required clearable>
          <span slot="append" v-if="bridge">{{bridge.asset.label}}</span>
        </v-text-field>
      </div>
      <div v-else-if="inout === 'out'">
        <!-- receiver and amount are fixed at finalization -->
        <v-text-field
          v-model="verifiedReceiver"
          :rules="[validateReceiver]"
          label="To Address"
          required
          disabled
        ></v-text-field>
        <v-text-field
          v-model="verifiedAmount"
          :rules="amountRules"
          label="Amount"
          required
          disabled
        >
          <span slot="append" v-if="bridge">{{bridge.asset.label}}</span>
        </v-text-field>
      </div>
    </v-form>
    <v-btn color="primary" :disabled="valid === false" @click="clickSend">Send {{this.optype}} Tx</v-btn>
    <v-btn text @click="clickBack">Back</v-btn>
  </div>
</template>

<script>
import { validateAddress } from "./Commons";
import { ethToAergo } from "eth-merkle-bridge-js";
import Web3 from "web3";

export default {
  name: "Form",
  props: [
    "bridge",
    "toBridge",
    "optype",
    "etheraccount",
    "aergoaccount",
    "verifiedReceiver",
    "verifiedAmount"
  ],
  components: {},
  data: () => ({
    valid: false,
    receiver: "",
    amount: "",
    amountRules: [
      v => !!v || "Amount is required",
      //v => /[0-9]+(.?[0-9]*)/.test(v) || "Amount must be real number"
      v => /^\d+(\.?\d*)$/.test(v) || "Amount must be real number"
    ],
    nextVerify: 100,
    nextVerifyRules: [],
    isTimeOk: true,
    web3: null
  }),
  created() {
    // load ethereum web3
    // Modern dapp browsers...
    if (window.ethereum) {
      this.web3 = new Web3(window.ethereum);
    }
    // Legacy dapp browsers...
    else if (window.web3) {
      this.web3 = new Web3(window.web3.currentProvider); //window.web3 = new Web3(web3.currentProvider);
    }
    // Non-dapp browsers...
    else {
      /* eslint-disable no-console */
      console.log(
        "Non-Ethereum browser detected. You should consider trying MetaMask!"
      );
      this.web3 = new Web3(
        new Web3.providers.HttpProvider("http://localhost:8545")
      );
    }
  },
  computed: {
    inout: function() {
      if (
        this.optype === "burn" ||
        this.optype === "lock" ||
        this.optype === "freeze"
      ) {
        return "in";
      } else if (
        this.optype === "mint" ||
        this.optype === "unlock" ||
        this.optype === "unfreeze"
      ) {
        return "out";
      } else {
        return "";
      }
    },
    wallet: function() {
      if (this.bridge) {
        if (this.bridge.net.type === "aergo" && this.aergoaccount) {
          if (this.aergoaccount.chainId === this.bridge.net.chainId) {
            return {
              isLogin: true,
              address: this.aergoaccount.address,
              err: "",
              type: this.bridge.net.type
            };
          }
          return {
            isLogin: false,
            address: this.aergoaccount.address,
            err: "The account's chainId is different with the bridge's",
            type: this.bridge.net.type
          };
        } else if (this.bridge.net.type === "ethereum" && this.etheraccount) {
          if (this.etheraccount.selectedAddress) {
            if (
              this.etheraccount.networkVersion ===
              this.bridge.net.networkVersion
            ) {
              return {
                isLogin: true,
                address: this.etheraccount.selectedAddress,
                err: "",
                type: this.bridge.net.type
              };
            }

            return {
              isLogin: false,
              address: this.etheraccount.selectedAddress,
              err:
                "The account's network version is different with the bridge's" +
                this.etheraccount.networkVersion,
              type: this.bridge.net.type
            };
          } else {
            return {
              isLogin: false,
              address: this.etheraccount.selectedAddress,
              err: "Click metamask icon at toolbar to connect this DApp",
              type: this.bridge.net.type
            };
          }
        } else {
          // logged out
          if (this.bridge.net.type === "aergo") {
            return {
              isLogin: false,
              address: "",
              err: "Login to aergo connect",
              type: this.bridge.net.type
            };
          } else {
            return {
              isLogin: false,
              address: "",
              err: "Login to Metamask",
              type: this.bridge.net.type
            };
          }
        }
      } else {
        return {
          isLogin: false,
          address: "",
          err: "Bridge is Not Initialized",
          type: ""
        };
      }
    }
  },

  methods: {
    clickSend() {
      if (this.$refs.form.validate()) {
        console.log(this.receiver, this.bridge.asset.id, this.amount, this.bridge.contract.id)
        const receipt = ethToAergo.lock(
          this.web3, this.receiver, this.bridge.asset.id, this.amount, this.bridge.contract.id, this.bridge.contract.abi);
          
          console.log(receipt);

        this.$emit("updateSharedReceiver", this.receiver);
        this.$emit("stepping", "next");
      } else {
        if (!this.wallet.isLogin) {
          this.$emit("needLogin", true, this.bridge.net.type);
        }
      }
    },
    clickBack() {
      this.$refs.form.resetValidation();
      this.$emit("needLogin", false, this.bridge.net.type);
      this.$emit("stepping", "prev");
    },
    validateReceiver(v) {
      if (!v) {
        return "Address is required";
      } else {
        return validateAddress(this.toBridge.net.type, v);
      }
    },
    validateAccount() {
      if (this.wallet.isLogin) {
        this.$emit("needLogin", false, this.bridge.net.type);

        return true;
      } else {
        return this.wallet.err;
      }
    }
  }
};
</script>

<style>
/*
.theme--light.v-messages {
 color: red !important;
}
.theme--light.v-input--is-disabled .v-label {
  color: red !important;
}
*/
.errored--disable-textfield .theme--light.v-messages {
  color: red !important;
}
.errored--disable-textfield .v-label {
  color: red !important;
}
</style>