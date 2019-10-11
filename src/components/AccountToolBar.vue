<template>
  <div>
    <v-app-bar app color="#ff0097" dark>
      <v-app-bar-nav-icon @click.stop="$emit('open_drawer');"></v-app-bar-nav-icon>

      <!-- title on toolbar -->
      <v-toolbar-title>Aergo to Ethereum Merkle Bridge</v-toolbar-title>

      <v-spacer></v-spacer>
      <!-- aergo accoount chip -->
      <v-menu bottom right transition="scale-transition" origin="top left">
        <template v-slot:activator="{ on }">
          <v-chip pill outlined v-on="on">
            <v-avatar left>
              <v-img :src="require('../assets/aergoicon.png')"></v-img>
            </v-avatar>
          </v-chip>
        </template>
        <v-card>
          <!-- not logged in to aergo connect -->
          <v-list v-if="this.aergoaccount === null">
            <v-list-item>
              <v-list-item-avatar>
                <v-img :src="require('../assets/aergoicon.png')"></v-img>
              </v-list-item-avatar>
              <v-list-item-content>
                <v-list-item-title>Aergo Connect</v-list-item-title>
                <v-btn color="primary" @click="getAergoActiveAccount">Login</v-btn>
              </v-list-item-content>
            </v-list-item>
          </v-list>
          <!-- on logged in to aergo connect -->
          <v-list v-else>
            <v-list-item>
              <v-list-item-avatar>
                <v-img :src="require('../assets/aergoicon.png')"></v-img>
              </v-list-item-avatar>
              <v-list-item-content>
                <v-list-item-title>Logged In</v-list-item-title>
                <v-list-item-subtitle>{{this.aergoaccount.address}}</v-list-item-subtitle>
              </v-list-item-content>
            </v-list-item>
          </v-list>
        </v-card>
      </v-menu>

      <!-- ethereum accoount chip -->
      <v-menu bottom right transition="scale-transition" origin="top left">
        <template v-slot:activator="{ on }">
          <v-chip pill outlined v-on="on">
            <v-avatar left>
              <v-img :src="require('../assets/metamask.png')"></v-img>
            </v-avatar>
          </v-chip>
        </template>
        <v-card>
          <!-- not logged in to aergo connect -->
          <v-list>
            <v-list-item>
              <v-list-item-avatar>
                <v-img :src="require('../assets/metamask.png')"></v-img>
              </v-list-item-avatar>
              <v-list-item-content>
                <span v-if="this.etheraccount === null">
                  <v-list-item-title>Logged Out</v-list-item-title>
                  <v-list-item-subtitle>Login to Metamask</v-list-item-subtitle>
                </span>
                <span v-else-if="this.etheraccount.isUnlocked === false">
                  <v-list-item-title>Locked</v-list-item-title>
                  <v-list-item-subtitle>Unlock Metamask</v-list-item-subtitle>
                </span>
                <span v-else-if="this.etheraccount.selectedAddress === null">
                  <v-list-item-title>Metamask</v-list-item-title>
                  <v-btn color="primary" @click="connectMetamask">Connect DApp</v-btn>
                </span>
                <!-- on logged in to metamask-->
                <span v-else>
                  <v-list-item-title>Logged In</v-list-item-title>
                  <v-list-item-subtitle>{{this.etheraccount.selectedAddress}}</v-list-item-subtitle>
                </span>
              </v-list-item-content>
            </v-list-item>
          </v-list>
        </v-card>
      </v-menu>
    </v-app-bar>
  </div>
</template>


<script>
//web3.currentProvider.publicConfigStore.on('update', callback);
// if account.selectedAddress is null, go to account configuration -> connection  -> allow local host

export default {
  name: "AccountToolBar",
  components: {},
  data: () => ({
    etheraccount: null,
    aergoaccount: null,
    web3: null,
    aergoapi: null,
    drawer: null
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
      this.web3 = new Web3(
        new Web3.providers.HttpProvider("http://localhost:8545")
      );
    }
    // set ethereum account change listener
    this.web3.currentProvider.publicConfigStore.on("update", account => {
      this.etheraccount = account;
      this.$emit("login_ethereum", account);
    });

    // set aergo account event change listener
    window.addEventListener("AERGO_ACTIVE_ACCOUNT", event => {
      this.aergoaccount = event.detail.account;
      this.$emit("login_aergo", event.detail.account);
    });
  },
  methods: {
    getAergoActiveAccount() {
      window.postMessage({
        type: "AERGO_REQUEST",
        action: "ACTIVE_ACCOUNT"
      });
    },
    connectMetamask() {
      ethereum.enable();
    }
  }
};
</script>