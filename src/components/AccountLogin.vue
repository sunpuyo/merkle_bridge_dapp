<template>
  <div>
    <br />
    <div v-if="bridge">
      <div v-if="this.status === 'logout'">
        login to
        <span v-if="bridge.net.type==='aergo'">aergo-connect</span>
        <span v-else>metamask</span>
        or unlock your account.
      </div>
      <div v-else-if="this.status === 'login'">
        You are logged in
        <br />
        <span v-if="bridge.net.type==='aergo'">{{aergoaccount.address}}</span>
        <span v-else>{{etheraccount.selectedAddress}}</span>
        <br />Do you want to continue using this account?
      </div>
      <div
        v-else-if="this.status === 'loginDiffChainId'"
      >The account's chainId is different with the bridge's. Check your account.</div>
    </div>
    <br />
    <v-btn
      color="primary"
      :disabled="status !== 'login'"
      @click="$emit('stepping', 'next');"
    >Continue</v-btn>
    <v-btn text @click="$emit('stepping', 'prev');">Back</v-btn>
  </div>
</template>

<script>
export default {
  name: "AccountLogin",
  props: ["bridge", "etheraccount", "aergoaccount"],
  components: {
    //
  },
  data: () => ({
    //
  }),
  computed: {
    // a computed getter
    status: function() {
      if (this.bridge) {
        if (
          this.bridge.net.type === "aergo" &&
          this.aergoaccount &&
          this.aergoaccount.address
        ) {
          if (this.aergoaccount.chainId === this.bridge.net.chainId) {
            return "login";
          }
          return "loginDiffChainId";
        } else if (
          this.bridge.net.type === "ethereum" &&
          this.etheraccount &&
          this.etheraccount.selectedAddress
        ) {
          if (this.etheraccount.chainId === this.bridge.net.chainId) {
            return "login";
          }
          return "loginDiffChainId";
        }
      }
      return "logout";
    }
  }
};
</script>

<style>
</style>

