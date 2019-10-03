<template>
  <div id="app">
    <v-app>
      <AccountToolBar @ethereumlogin="loginEthereum" @aergologin="loginAergo"/>
      <v-content class="pa-0">
        <v-stepper v-model="step" vertical>
          <v-stepper-step :complete="step > 1" step="1">
            Select a bridge
            <small>Summarize if needed</small>
          </v-stepper-step>

          <v-stepper-content step="1">
            <BridgeSelect @select-operation="updateBridge"/>
          </v-stepper-content>

          <v-stepper-step :complete="step > 2" step="2">Login to wallet (sending network)</v-stepper-step>
          <v-stepper-content step="2">
            
             <AccountLogin v-bind:bridge="fromBridge" v-bind:etheraccount="etheraccount" v-bind:aergoaccount="aergoaccount" />

            <v-btn color="primary" @click="step = 3">Continue</v-btn>
            <v-btn text @click="step = 1">Back</v-btn>
          </v-stepper-content>

          <v-stepper-step :complete="step > 3" step="3">Send an asset</v-stepper-step>
          <v-stepper-content step="3">
            TODO<br/>
            <v-btn color="primary" @click="step = 4">Next</v-btn>
            <v-btn text @click="step = 2">Back</v-btn>
          </v-stepper-content>

          <v-stepper-step :complete="step > 4" step="4">Login to wallet (receiving network)</v-stepper-step>
          <v-stepper-content step="4">
            TODO<br/>
            <v-btn color="primary" @click="step = 3">Next</v-btn>
            <v-btn text @click="step = 3">Back</v-btn>
          </v-stepper-content>

          <v-stepper-step :complete="step > 5" step="5">Wating a validation</v-stepper-step>
          <v-stepper-content step="5">
            TODO<br/>
            <v-btn color="primary" @click="step = 5">Next</v-btn>
            <v-btn text @click="step = 4">Back</v-btn>
          </v-stepper-content>

          <v-stepper-step :complete="step > 6" step="6">Receive the asset</v-stepper-step>
          <v-stepper-content step="6">
            TODO<br/>
            <v-btn color="primary" @click="step = 1">Done</v-btn>
          </v-stepper-content>
        </v-stepper>
      </v-content>
    </v-app>
  </div>
</template>

<script>
import AccountToolBar from "./components/AccountToolBar";
import BridgeSelect from "./components/bridge/BridgeSelect";
import AccountLogin from "./components/AccountLogin"

export default {
  name: "App",
  components: {
    AccountToolBar,
    BridgeSelect,
    AccountLogin,
  },
  data: () => ({
    step: 1,
    optype: null,
    fromBridge: null,
    toBridge: null,
    etheraccount: 'x',
    aergoaccount: 'y'
  }),
  methods: {
    loginEthereum(etheraccount) {
      this.etheraccount = etheraccount;
    },
    loginAergo(aergoaccount) {
      this.aergoaccount = aergoaccount;
    },
    updateBridge(optype, fromBridge, toBridge) {
      this.optype = optype;
      this.fromBridge = fromBridge;
      this.toBridge = toBridge;
      if (optype === 'send') {
        this.step = 2; // go to sending network login page
      } else {
        this.step = 4; // go to receiving network login page
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