<template>
  <div id="app">
    <v-app>
      <AccountToolBar />
      <v-content>
        <v-stepper v-model="step" vertical>
          <v-stepper-step :complete="step > 1" step="1">
            Select a bridge
            <small>Summarize if needed</small>
          </v-stepper-step>

          <v-stepper-content step="1">
            <BridgeSelect/>
          </v-stepper-content>

          <v-stepper-step :complete="step > 2" step="2">Login to wallet</v-stepper-step>

          <v-stepper-content step="2">
            <v-card color="grey lighten-1" class="mb-12" height="200px"></v-card>
            <v-btn color="primary" @click="step = 3">Next</v-btn>
            <v-btn text @click="step = 1">Back</v-btn>
          </v-stepper-content>

          <v-stepper-step :complete="step > 3" step="3">Send an asset</v-stepper-step>

          <v-stepper-content step="3">
            <v-card color="grey lighten-1" class="mb-12" height="200px"></v-card>
            <v-btn color="primary" @click="step = 4">Next</v-btn>
            <v-btn text @click="step = 2">Back</v-btn>
          </v-stepper-content>

          <v-stepper-step step="4">Wating a validation</v-stepper-step>
          <v-stepper-content step="4">
            <v-card color="grey lighten-1" class="mb-12" height="200px"></v-card>
            <v-btn color="primary" @click="step = 5">Next</v-btn>
            <v-btn text @click="step = 3">Back</v-btn>
          </v-stepper-content>

          <v-stepper-step step="5">Receive the asset</v-stepper-step>
          <v-stepper-content step="5">
            <v-card color="grey lighten-1" class="mb-12" height="200px"></v-card>
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

export default {
  name: "App",
  components: {
    AccountToolBar,
    BridgeSelect
  },
  data: () => ({
    step: 1
  })
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