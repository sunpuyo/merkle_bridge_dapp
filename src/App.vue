<template>
  <div id="app">
    <v-app>
      <AccountToolBar
        @login_ethereum="login_ethereum"
        @login_aergo="login_aergo"
        @stepping="stepping"
      />
      <v-content class="pa-0">
        <v-stepper v-model="step" vertical>
          <v-stepper-step :complete="step > 1" step="1">
            Select a bridge
            <small>Summarize if needed</small>
          </v-stepper-step>

          <v-stepper-content step="1">
            <BridgeSelect @update_bridge="update_bridge" @stepping="stepping" />
          </v-stepper-content>

          <v-stepper-step :complete="step > 2" step="2">Login to wallet (sending network)</v-stepper-step>
          <v-stepper-content step="2">
            <AccountLogin
              v-bind:bridge="fromBridge"
              v-bind:etheraccount="etheraccount"
              v-bind:aergoaccount="aergoaccount"
              @stepping="stepping"
            />
          </v-stepper-content>

          <v-stepper-step :complete="step > 3" step="3">Send an asset</v-stepper-step>
          <v-stepper-content step="3">
            <SendForm v-bind:bridge="fromBridge" @stepping="stepping"/>
          </v-stepper-content>

          <v-stepper-step :complete="step > 4" step="4">Wating a validation</v-stepper-step>
          <v-stepper-content step="4">
             <History />
            <br />
            
          </v-stepper-content>

          <v-stepper-step :complete="step > 5" step="5">Login to wallet (receiving network)</v-stepper-step>
          <v-stepper-content step="5">
            <AccountLogin
              v-bind:bridge="toBridge"
              v-bind:etheraccount="etheraccount"
              v-bind:aergoaccount="aergoaccount"
              @stepping="stepping"
            />
          </v-stepper-content>

          <v-stepper-step :complete="step > 6" step="6">Receive the asset</v-stepper-step>
          <v-stepper-content step="6">
            TODO
            <br />
            <v-btn color="primary" @click="step = 1">Done</v-btn>
          </v-stepper-content>
        </v-stepper>
      </v-content>
    </v-app>
  </div>
</template>

<script>
import AccountToolBar from "./components/AccountToolBar";
import BridgeSelect from "./components/BridgeSelect";
import AccountLogin from "./components/AccountLogin";
import SendForm from "./components/Send";
import History from "./components/History";

export default {
  name: "App",
  components: {
    AccountToolBar,
    BridgeSelect,
    AccountLogin,
    SendForm,
    History
  },
  data: () => ({
    step: 1,
    fromBridge: null,
    toBridge: null,
    etheraccount: "x",
    aergoaccount: "y"
  }),
  methods: {
    login_ethereum(etheraccount) {
      this.etheraccount = etheraccount;
    },
    login_aergo(aergoaccount) {
      this.aergoaccount = aergoaccount;
    },
    update_bridge(fromBridge, toBridge) {
      this.fromBridge = fromBridge;
      this.toBridge = toBridge;
    },
    stepping(step) {
      if (step === "next") {
        this.step = this.step + 1;
      } else if (step === "prev") {
        this.step = this.step - 1;
      } else {
        this.step = step;
      }
    }
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