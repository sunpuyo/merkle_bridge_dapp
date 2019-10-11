<template>
  <v-text-field v-model="this.msg" label="From Address" disabled required>
    <template v-slot:prepend>
      <v-img v-if="type === 'aergo'" :src="require('../assets/aergoicon.png')" width="24"></v-img>
      <v-img v-else-if="type === 'ethereum'" :src="require('../assets/metamask.png')" width="24"></v-img>
    </template>
  </v-text-field>
</template>

<script>
export default {
  name: "Account",
  props: ["bridge", "etheraccount", "aergoaccount"],
  data: () => ({}),
  computed: {
    type: function() {
      if (this.bridge) {
        return this.bridge.net.type;
      }
      return "";
    },
    msg: function() {
      if (this.bridge) {
        if (this.bridge.net.type === "aergo" && this.aergoaccount) {
          if (this.aergoaccount.chainId === this.bridge.net.chainId) {
            this.$emit("checklogin", true);
            return this.aergoaccount.address;
          }
          this.$emit("checklogin", false);
          return "(The account's chainId is different with the bridge's)";
        } else if (this.bridge.net.type === "ethereum" && this.etheraccount) {
          if (this.etheraccount.selectedAddress) {
            if (this.etheraccount.chainId === this.bridge.net.chainId) {
              this.$emit("checklogin", true);
              return this.etheraccount.selectedAddress;
            }
            this.$emit("checklogin", false);
            return "(The account's chainId is different with the bridge's)";
          } else {
            this.$emit("checklogin", false);
            return "(Click metamask icon at toolbar to connect this DApp)";
          }
        } else {
          // logged out
          if (this.bridge.net.type === "aergo") {
            this.$emit("checklogin", false);
            return "(Login to aergo connect)";
          } else {
            this.$emit("checklogin", false);
            return "(Login to Metamask)";
          }
        }
      } else {
        this.$emit("checklogin", false);
        return "(Not Initialized)";
      }
    }
  }
  /*
    account: function() {
      if (this.bridge) {
        if (this.bridge.net.type === "aergo" && this.aergoaccount) {
          if (this.aergoaccount.chainId === this.bridge.net.chainId) {
            this.$emit(
              "accountchanged",
              this.aergoaccount.address,
              "login",
              this.aergoaccount.address
            );
            return;
          }
          this.$emit(
            "accountchanged",
            this.aergoaccount.address,
            "loginDiffChainId",
            "The account's chainId is different with the bridge's."
          );
          return;
        } else if (this.bridge.net.type === "ethereum" && this.etheraccount) {
          if (this.etheraccount.selectedAddress) {
            if (this.etheraccount.chainId === this.bridge.net.chainId) {
              this.$emit(
                "accountchanged",
                this.etheraccount.selectedAddress,
                "login",
                this.etheraccount.selectedAddress
              );
              return;
            }
            this.$emit(
              "accountchanged",
              this.etheraccount.selectedAddress,
              "loginDiffChainId",
              "The account's chainId is different with the bridge's."
            );
            return;
          } else {
            this.$emit(
              "accountchanged",
              "",
              "lock",
              "Click metamask icon at toolbar to connect this DApp"
            );
            return;
          }
        } else {
          // logged out
          if (this.bridge.net.type === "aergo") {
            this.$emit(
              "accountchanged",
              "",
              "logout",
              "Login to aergo connect"
            );
            return;
          } else {
            this.$emit("accountchanged", "", "logout", "Login to Metamask");
            return;
          }
        }
      } else {
        this.$emit("accountchanged", "", "logout", "");
        return;
      }
    }
  }*/
};
</script>

<style>
</style>

