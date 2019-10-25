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
        :label="inout==='in'? 'From Address' : 'Operator Address'"
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
        <v-text-field
          v-model="amount"
          :rules="[validateAmount]"
          :label="'Amount (' + bridge.asset.label +')'"
          required
          clearable
          append-outer-icon="mdi-refresh"
          @click:append-outer="updateDelegateAmount"
        >
          <span slot="append" v-if="bridge">&nbsp; / {{this.delegatedAmount}} Approved</span>
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
        <v-text-field v-model="verifiedAmount" label="Amount" required disabled>
          <span slot="append" v-if="bridge">{{bridge.asset.label}}</span>
        </v-text-field>
      </div>
    </v-form>
    <v-btn
      color="primary"
      :loading="loading"
      :disabled="valid === false"
      @click="clickSend"
    >Send {{this.optype}} Tx</v-btn>
    <v-btn text @click="clickBack">Back</v-btn>

    <!-- result dialog -->
    <v-row justify="center">
      <v-dialog v-model="dialog.open" max-width="290">
        <v-card>
          <v-card-title v-if="dialog.success" class="headline">
            <span v-if="dialog.success">Success</span>
            <span v-else>Fail</span>
          </v-card-title>
          <v-card-text>{{dialog.message}}</v-card-text>
          <v-card-actions>
            <v-spacer></v-spacer>
            <v-btn color="green darken-1" text @click="clickDialogOk">Ok</v-btn>
          </v-card-actions>
        </v-card>
      </v-dialog>
    </v-row>
  </div>
</template>

<script>
import { ethToAergo } from "eth-merkle-bridge-js"; //aergoToEth
import { web3 } from "./Web3Loader";
import { validateAddress } from "./Commons";
import { AergoClient, GrpcWebProvider } from "@herajs/client";

export default {
  name: "Form",
  props: [
    "fromBridge",
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
    delegatedAmount: 0,
    nextVerify: 100,
    nextVerifyRules: [],
    isTimeOk: true,
    loading: false,
    dialog: {
      open: false,
      success: false,
      message: ""
    }
  }),
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
    bridge: function() {
      if (this.inout === "in") {
        return this.fromBridge;
      } else if (this.inout === "out") {
        return this.toBridge;
      } else {
        return null;
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
    /*handleResult(receipt) {
      this.loading = true;

      receipt
        .then(response => {
          const hash = response.transactionHash
            ? response.transactionHash
            : response.hash;
          this.dialog.open = true;
          this.dialog.success = true;
          this.dialog.message = hash;
          this.loading = false;

          return hash;
        })
        .catch(err => {
          this.dialog.open = true;
          this.dialog.success = false;
          this.dialog.message = err;
          this.loading = false;

          return null;
        });
    },*/
    async handleResult(receipt) {
      this.loading = true;
      try {
        const response = await receipt;

        const hash = response.transactionHash
          ? response.transactionHash
          : response.hash;
        this.dialog.open = true;
        this.dialog.success = true;
        this.dialog.message = hash;
        this.loading = false;
        /* eslint-disable */
        console.log(response);

        return hash;
      } catch (err) {
        this.dialog.open = true;
        this.dialog.success = false;
        this.dialog.message = err;
        this.loading = false;
        /* eslint-disable */
        console.log(err);

        return null;
      }
    },
    async clickSend() {
      if (this.$refs.form.validate()) {
        if (this.optype === "lock") {
          await this.handleResult(
            ethToAergo.lock(
              web3,
              this.receiver,
              this.fromBridge.asset.id,
              this.amount,
              this.fromBridge.contract.id,
              this.fromBridge.contract.abi
            )
          );
        } else if (this.optype == "unfreeze") {
          let herajs = new AergoClient(
            {},
            new GrpcWebProvider({ url: this.toBridge.net.endpoint })
          );

          let builtTx = await ethToAergo.buildUnfreezeTx(
            web3,
            herajs,
            this.wallet.address,
            this.fromBridge.contract.id,
            this.toBridge.contract.id,
            this.toBridge.contract.abi,
            this.verifiedReceiver,
            this.fromBridge.asset.id
          );

          builtTx.to = this.toBridge.contract.id;
          console.log(builtTx);
          builtTx.payload_json = JSON.parse(builtTx.payload);
          delete builtTx.payload;

          const txHash = await this.handleResult(
            new Promise((resolve, reject) => {
              try {
                window.addEventListener(
                  "AERGO_SEND_TX_RESULT",
                  event => {
                    console.log("EVNETD", event.detail);
                    resolve(event.detail);
                  },
                  { once: true }
                );

                window.postMessage({
                  type: "AERGO_REQUEST",
                  action: "SEND_TX",
                  data: builtTx
                });
              } catch (err) {
                reject(err);
              }
            })
          );
          
          const receipt = await herajs.getTransactionReceipt(txHash);
          console.log("ret", receipt);
        }
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
    clickDialogOk() {
      this.dialog.open = false;
      if (this.dialog.success) {
        this.$emit("stepping", "next");
        this.$emit("updateSharedReceiver", this.receiver);
      }
    },
    validateReceiver(v) {
      if (this.toBridge) {
        return validateAddress(this.toBridge.net.type, v);
      } else {
        return true;
      }
    },
    validateAccount() {
      if (this.wallet.isLogin) {
        this.$emit("needLogin", false, this.bridge.net.type);

        return true;
      } else {
        return this.wallet.err;
      }
    },
    validateAmount(v) {
      if (!v) {
        return "Amount is required";
      } else if (false === /^\d+(\.?\d*)$/.test(v)) {
        return "Amount must be real number";
      } else if (parseFloat(v) <= 0) {
        return "Amount must be bigger than 0";
      } else if (parseFloat(v) > this.delegatedAmount) {
        return (
          "Delegated Asset Amount is Insufficient (Current Approval = " +
          this.delegatedAmount +
          ")"
        );
      }
      return true;
    },
    updateDelegateAmount() {
      if (this.bridge && this.inout === "in" && this.wallet.isLogin) {
        if (this.fromBridge.asset.type === "erc20") {
          // define contract
          let assetContract = new web3.eth.Contract(
            this.fromBridge.asset.abi,
            this.fromBridge.asset.id
          );
          // call allowance of erc20
          assetContract.methods
            .allowance(this.wallet.address, this.fromBridge.contract.id)
            .call()
            .then(delegated => {
              this.delegatedAmount = delegated;
            });
        } else {
          //TODO
        }

        this.delegatedAmount = "?";
      }

      this.delegatedAmount = "?";
    }
  },

  watch: {
    // this updates delegated amount
    "wallet.address": function() {
      console.log("refresh delegated amount", this.wallet);
      this.updateDelegateAmount();
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