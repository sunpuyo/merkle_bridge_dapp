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

    <v-form ref="form" v-model="valid" lazy-validation>
      <Account
        v-bind:bridge="bridge"
        v-bind:etheraccount="etheraccount"
        v-bind:aergoaccount="aergoaccount"
        v-bind:isLogin="isLogin"
        @checklogin="checklogin"
      />
      <v-text-field
        v-model="nextVerify"
        :rules="nextVerifyRules"
        label=" Next Verification Time (Estimated)"
        required
        disabled
      ></v-text-field>
      <div v-if="inout === 'in'">
        <v-text-field
          v-model="receiver"
          :counter="10"
          :rules="receiverRules"
          label="To Address"
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
          :counter="10"
          :rules="receiverRules"
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
    <v-btn
      color="primary"
      :disabled="valid === false || isLogin === false"
      @click="$emit('stepping', 'next');"
    >Send {{this.optype}} Tx</v-btn>
    <v-btn text @click="$emit('stepping', 'prev');">Back</v-btn>
  </div>
</template>

<script>
//:disabled="inout==='out'"
import Account from "./Account";

export default {
  name: "Form",
  props: [
    "bridge",
    "optype",
    "etheraccount",
    "aergoaccount",
    "verifiedReceiver",
    "verifiedAmount"
  ],
  components: { Account },
  data: () => ({
    valid: false,
    isLogin: false,
    receiver: "",
    receiverRules: [
      v => !!v || "Address is required",
      v => (v && v.length <= 10) || "Name must be less than 10 characters"
    ],
    amount: '',
    amountRules: [],
    nextVerify: 100,
    nextVerifyRules: []
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
    }
  },
  methods: {
    checklogin(isLoggedIn) {
      this.isLogin = isLoggedIn;
    }
  }
};
</script>

<style>
</style>