<template>
  <v-app-bar app color="#ff0097" dark>
    <v-toolbar-title>Aergo to Ethereum Merkle Bridge</v-toolbar-title>

    <v-spacer></v-spacer>
    <!-- aergo accoount chip -->
    <v-chip outlined @click="getAergoActiveAccount">
      <v-avatar left>
        <v-img :src="require('../assets/aergoicon.png')"></v-img>
      </v-avatar>
      <span v-if="this.argAccount === null">(login to aergo connect)</span>
      <span v-else>{{argAccount.address}}</span>
    </v-chip>

    <!-- ethereum accoount chip -->
    <v-chip outlined @click="getEtherActiveAccount">
      <v-avatar left>
        <v-img :src="require('../assets/metamask.png')"></v-img>
      </v-avatar>
      <span v-if="this.ethAccount === null">(login to metamask)</span>
      <span v-else-if="this.ethAccount.isUnlocked === false">(unlock metamask)</span>
      <span
        v-else-if="this.ethAccount.selectedAddress === null"
      >(allow local connection in metamask)</span>
      <span v-else>{{this.ethAccount.selectedAddress}}</span>
    </v-chip>
  </v-app-bar>
</template>


<script>
//web3.currentProvider.publicConfigStore.on('update', callback);
// if account.selectedAddress is null, go to account configuration -> connection  -> allow local host

export default {
  name: "AccountToolBar",
  components: {},
  data: () => ({
    ethAccount: null,
    argAccount: null,
    web3: null,
    aergoapi: null,
  }),
  created() {
    // load ethereum web3
    // Modern dapp browsers...
    if (window.ethereum) {
      this.web3 = new Web3(ethereum);
    }
    // Legacy dapp browsers...
    else if (window.web3) {
      this.web3 = new Web3(web3.currentProvider); //window.web3 = new Web3(web3.currentProvider);
    }
    // Non-dapp browsers...
    else {
      console.log(
        "Non-Ethereum browser detected. You should consider trying MetaMask!"
      );
      this.web3 = new Web3(new Web3.providers.HttpProvider("http://localhost:8545"));
    }
    // set ethereum account change listener
    this.web3.currentProvider.publicConfigStore.on("update", account => {
      this.ethAccount = account;
      this.$emit('login_ethereum', account);
    });

    // set aergo account event change listener
    window.addEventListener("AERGO_ACTIVE_ACCOUNT", event => {
      this.argAccount = event.detail.account;
      this.$emit('login_aergo', event.detail.account);
    });
  },
  methods: {
    getAergoActiveAccount() {
      window.postMessage({
        type: "AERGO_REQUEST",
        action: "ACTIVE_ACCOUNT"
      });
    },
    getEtherActiveAccount() {
       ethereum.enable();
    }
  }
};
</script>