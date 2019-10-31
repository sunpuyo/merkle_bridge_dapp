<template>
  <div id="app">
    <v-app>
      <!-- navigation menu -->
      <v-navigation-drawer v-model="drawer" absolute temporary>
        <v-list-item @click="step=1; menu='transfer'; drawer=false;">
          <v-list-item-avatar>
            <v-icon large>mdi-bank-transfer-in</v-icon>
          </v-list-item-avatar>
          <v-list-item-content>Transfer Asset</v-list-item-content>
        </v-list-item>
        <v-list-item @click="step=1; menu='navigate'; drawer=false;">
          <v-list-item-avatar>
            <v-icon large>mdi-search-web</v-icon>
          </v-list-item-avatar>
          <v-list-item-content>Navigate</v-list-item-content>
        </v-list-item>
      </v-navigation-drawer>
      <AccountToolBar
        v-bind:isLoginNeeded="isLoginNeeded"
        v-bind:isLoginNeededNetType="isLoginNeededNetType"
        @login_ethereum="login_ethereum"
        @login_aergo="login_aergo"
        @open_drawer="open_drawer"
        @stepping="stepping"
      />
      <v-content class="pa-0">
        최상단에 뭔가 머클브릿지에 대한 간략한 설명과 사용법을 적어야 할거 같다.
        아니면 다른 상세 메인 페이지를 탭으로 제공하는 것도 방법일듯.
        FIXXME
        <v-stepper v-model="step" vertical>
          <v-stepper-step :complete="step > 1" step="1">
            Select a bridge
            <small>TODO Summarize if needed</small>
          </v-stepper-step>
          <v-stepper-content step="1">
            <BridgeSelect @select_bridge="select_bridge" @stepping="stepping" />
          </v-stepper-content>

          <div v-if="menu==='transfer'">
            <v-stepper-step :complete="step > 2" step="2">Send an asset</v-stepper-step>
            <v-stepper-content step="2">
              <Form
                v-bind:fromBridge="fromBridge"
                v-bind:toBridge="toBridge"
                v-bind:optype="fromOpType"
                v-bind:etheraccount="etheraccount"
                v-bind:aergoaccount="aergoaccount"
                v-bind:verifiedReceiver="verifiedReceiver"
                v-bind:verifiedAmount="verifiedAmount"
                @needLogin="needLogin"
                @stepping="stepping"
              />
            </v-stepper-content>

            <v-stepper-step :complete="step > 3" step="3">Wating a verification</v-stepper-step>
            <v-stepper-content step="3">
              <Status
                v-bind:toBridge="toBridge"
                v-bind:fromBridge="fromBridge"
                @stepping="stepping"
                @update_finalize_info="update_finalize_info"
              />
              <br />
            </v-stepper-content>

            <v-stepper-step :complete="step > 4" step="4">Receive the asset</v-stepper-step>
            <v-stepper-content step="4">
              <Form
                v-bind:fromBridge="fromBridge"
                v-bind:toBridge="toBridge"
                v-bind:optype="toOpType"
                v-bind:etheraccount="etheraccount"
                v-bind:aergoaccount="aergoaccount"
                v-bind:verifiedReceiver="verifiedReceiver"
                v-bind:verifiedAmount="verifiedAmount"
                @needLogin="needLogin"
                @stepping="stepping"
              />
            </v-stepper-content>
          </div>

          <div v-else-if="menu==='navigate'">
            <v-stepper-step :complete="step > 2" step="2">Navigate asset transfers</v-stepper-step>
            <v-stepper-content step="2">
              <History />
            </v-stepper-content>
          </div>
          <div v-if="step > 4">
            Finish.
            다른걸 진행하려면 아래 버튼을 눌러라.
            <br />
            <v-btn @click="step=1" color="primary">Select Bridge</v-btn>or
            <v-btn @click="step=2" color="primary">Transfer Again</v-btn>
          </div>
        </v-stepper>
        TMP increase Approval : {{st}} =
        <v-btn @click="increaseApproval" color="primary">Increase Approval</v-btn>
      </v-content>
    </v-app>
  </div>
</template>

<script>
import AccountToolBar from "./components/AccountToolBar";
import BridgeSelect from "./components/BridgeSelect";
import Form from "./components/Form";
import Status from "./components/Status";
import History from "./components/History";
import { web3 } from "./components/common/Web3Loader";
import { erc20Abi } from "./components/abi/EtherERC20";
import { ethToAergo as eta } from "eth-merkle-bridge-js";
//import { AergoClient, GrpcWebProvider } from "@herajs/client";

export default {
  name: "App",
  components: {
    AccountToolBar,
    BridgeSelect,
    Status,
    Form,
    History
  },
  data: () => ({
    step: 1,
    drawer: null,
    menu: "transfer",
    fromBridge: null,
    toBridge: null,
    fromOpType: null,
    toOpType: null,
    verifiedReceiver: "",
    verifiedAmount: 0,
    isLoginNeeded: false,
    isLoginNeededNetType: "",
    etheraccount: null,
    aergoaccount: null,
    st: "",
    tmpText:'',
  }),
  methods: {
    login_ethereum(etheraccount) {
      this.etheraccount = etheraccount;
    },
    login_aergo(aergoaccount) {
      this.aergoaccount = aergoaccount;
    },
    open_drawer() {
      this.drawer = !this.drawer;
    },
    select_bridge(fromBridge, fromOpType, toBridge, toOpType) {
      this.fromBridge = fromBridge;
      this.toBridge = toBridge;
      this.fromOpType = fromOpType;
      this.toOpType = toOpType;
    },
    update_finalize_info(verifiedReceiver, verifiedAmount) {
      /* eslint-disable no-console */
      console.log(verifiedReceiver);
      this.verifiedReceiver = verifiedReceiver;
      this.verifiedAmount = verifiedAmount;
    },
    needLogin(isLoginNeeded, isLoginNeededNetType) {
      this.isLoginNeeded = isLoginNeeded;
      this.isLoginNeededNetType = isLoginNeededNetType;
    },
    stepping(step) {
      if (step === "next") {
        this.step = this.step + 1;
      } else if (step === "prev") {
        this.step = this.step - 1;
      } else {
        this.step = step;
      }
    },
    async increaseApproval() {
      const receipt = await eta.increaseApproval(
        web3,
        "0x89eD1D1C145F6bF3A7e62d2B8eB0e1Bf15Cb2374",
        20000, 
        "0xd898383A12CDE0eDF7642F7dD4D7006FdE5c433e",
        erc20Abi
      );
      console.log("INCREASE APPROVAL RECEIPT:", receipt);
      this.st = receipt.status;
    },
  }
};
</script>


<style>
#app {
  font-family: "DINPro Regular", "sans-serif";
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #ff0097;
  margin-top: 60px;
}
</style>