<template>
  <div>
    <v-list v-if="bridge" dense>
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
        <v-btn icon v-show="bridge.asset.id">
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
        <v-btn icon>
          <v-icon>mdi-launch</v-icon>
        </v-btn>
      </v-list-item>
    </v-list>

    <v-form ref="form" v-model="valid" lazy-validation>
      <Account
        v-bind:bridge="bridge"
        v-bind:etheraccount="etheraccount"
        v-bind:aergoaccount="aergoaccount"
        v-bind:isLogin="isLogin"
        @checklogin="checklogin"
      />
      <v-text-field
        v-model="toAddress"
        :counter="10"
        :rules="toAddressRules"
        label="To Address"
        required
      ></v-text-field>
      <v-text-field v-model="amount" :rules="amountRules" label="Amount" required>
        <span slot="append" v-if="bridge">{{bridge.asset.label}}</span>
      </v-text-field>
    </v-form>
    <v-btn
      color="primary"
      :disabled="valid === false || isLogin !== true"
      @click="$emit('stepping', 'next');"
    >Send {{this.optype}} Tx</v-btn>
    <v-btn text @click="$emit('stepping', 'prev');">Back</v-btn>
  </div>
</template>

<script>
import Account from "./Account";

export default {
  name: "Form",
  props: ["bridge", "optype", "etheraccount", "aergoaccount"],
  components: { Account },
  data: () => ({
    valid: true,
    isLogin: false,
    toAddress: "",
    toAddressRules: [
      v => !!v || "Address is required",
      v => (v && v.length <= 10) || "Name must be less than 10 characters"
    ],
    amount: "",
    amountRules: []
  }),
  methods: {
    checklogin(isLoggedIn) {
      this.isLogin = isLoggedIn;
    }
  }
};
</script>

<style>
</style>