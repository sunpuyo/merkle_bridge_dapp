
<template>
  <v-row align="center">
    <v-expansion-panels focusable accordion>
      <v-expansion-panel v-for="(item,i) in bridges" :key="i">
        <v-expansion-panel-header>{{item.bridge1.net.label}}({{item.bridge1.asset.label}}) - {{item.bridge2.net.label}}({{item.bridge2.asset.label}})</v-expansion-panel-header>
        <v-expansion-panel-content>
          <v-container fluid class="pa-0">
            <v-row>
              <v-col sm12 md6>
                <v-card class="mx-auto" min-width="350px">
                  <v-card-text class="pa-1">
                    <v-container fluid pa-0>
                      <v-row>
                        <v-col class="py-0">
                          <v-btn text @click="showFromMeta=!showFromMeta">
                            {{item.bridge1.net.label}}
                            <v-icon small>mdi-arrow-right</v-icon>
                            {{item.bridge2.net.label}}
                            <v-icon>mdi-menu-down</v-icon>
                          </v-btn>
                        </v-col>
                      </v-row>
                      <v-row>
                        <v-col class="py-0">
                          <p v-show="showFromMeta === true" align="left" class="px-5">
                            From Asset:
                            <a>{{item.bridge1.asset.id}}</a>
                            <br />From Bridge:
                            <a>{{item.bridge1.contract.id}}</a>
                            <br />To Asset:
                            <a>{{item.bridge2.asset.id}}</a>
                            <br />To Bridge:
                            <a>{{item.bridge2.contract.id}}</a>
                          </p>
                        </v-col>
                      </v-row>
                      <v-row>
                        <v-col class="px-0">
                          <v-icon>mdi-sack</v-icon>
                          <v-icon large>mdi-bank-transfer-in</v-icon>
                          <br />
                          <v-btn
                            color="primary"
                            text
                            @click="$emit('update_bridge', item.bridge1, getOpType('in', item.bridge1), item.bridge2, getOpType('out', item.bridge2)); $emit('stepping', 'next');"
                          >
                            <small>
                              1. {{getOpType('in', item.bridge1)}}
                              <br />
                              {{item.bridge1.asset.label}}
                            </small>
                          </v-btn>
                        </v-col>
                        <v-col class="px-0">
                          <v-icon large>mdi-weather-cloudy-arrow-right</v-icon>
                          <br />
                          <v-btn
                            color="primary"
                            text
                            @click="$emit('update_bridge', item.bridge1, getOpType('in', item.bridge1), item.bridge2, getOpType('out', item.bridge2)); $emit('stepping', 3);"
                          >
                            <small>
                              2. Wait
                              <br />Validation
                            </small>
                          </v-btn>
                        </v-col>
                        <v-col class="px-0">
                          <v-icon large>mdi-bank-transfer-out</v-icon>
                          <v-icon>mdi-sack</v-icon>
                          <br />
                          <v-btn
                            color="primary"
                            text
                            @click="$emit('update_bridge', item.bridge1, getOpType('in', item.bridge1), item.bridge2, getOpType('out', item.bridge2)); $emit('stepping', 3);"
                          >
                            <small>
                              3. {{getOpType('out', item.bridge2)}}
                              <br />
                              {{item.bridge2.asset.label}}
                            </small>
                          </v-btn>
                        </v-col>
                      </v-row>
                    </v-container>
                  </v-card-text>
                </v-card>
              </v-col>

              <v-col xs12 sm6>
                <v-card class="mx-auto" min-width="350px">
                  <v-card-text class="pa-1">
                    <v-row>
                      <v-col class="py-0">
                        <v-btn text @click="showToMeta=!showToMeta">
                          {{item.bridge2.net.label}}
                          <v-icon small>mdi-arrow-right</v-icon>
                          {{item.bridge1.net.label}}
                          <v-icon>mdi-menu-down</v-icon>
                        </v-btn>
                      </v-col>
                    </v-row>
                    <v-row>
                      <v-col class="py-0">
                        <p v-show="showToMeta === true" align="left" class="px-5">
                          From Asset:
                          <a>{{item.bridge2.asset.id}}</a>
                          <br />From Bridge:
                          <a>{{item.bridge2.contract.id}}</a>
                          <br />To Asset:
                          <a>{{item.bridge1.asset.id}}</a>
                          <br />To Bridge:
                          <a>{{item.bridge1.contract.id}}</a>
                        </p>
                      </v-col>
                    </v-row>

                    <v-container fluid class="pa-0">
                      <v-row>
                        <v-col class="px-0">
                          <v-icon>mdi-sack</v-icon>
                          <v-icon large>mdi-bank-transfer-in</v-icon>
                          <br />
                          <v-btn
                            color="primary"
                            text
                            @click="$emit('update_bridge', item.bridge2, getOpType('in', item.bridge2), item.bridge1, getOpType('out', item.bridge1)); $emit('stepping', 'next');"
                          >
                            <small>
                              1. {{getOpType('in', item.bridge2)}}
                              <br />
                              {{item.bridge2.asset.label}}
                            </small>
                          </v-btn>
                        </v-col>
                        <v-col class="px-0">
                          <v-icon large>mdi-weather-cloudy-arrow-right</v-icon>
                          <br />
                          <v-btn
                            color="primary"
                            text
                            @click="$emit('update_bridge', item.bridge2, getOpType('in', item.bridge2), item.bridge1, getOpType('out', item.bridge1)); $emit('stepping', 3);"
                          >
                            <small>
                              2. Wait
                              <br />Validation
                            </small>
                          </v-btn>
                        </v-col>
                        <v-col class="px-0">
                          <v-icon large>mdi-bank-transfer-out</v-icon>
                          <v-icon>mdi-sack</v-icon>
                          <br />
                          <v-btn
                            color="primary"
                            text
                            @click="$emit('update_bridge', item.bridge2, getOpType('in', item.bridge2), item.bridge1, getOpType('out', item.bridge1)); $emit('stepping', 3);"
                          >
                            <small>
                              3. {{getOpType('out', item.bridge1)}}
                              <br />
                              {{item.bridge1.asset.label}}
                            </small>
                          </v-btn>
                        </v-col>
                      </v-row>
                    </v-container>
                  </v-card-text>
                </v-card>
              </v-col>
            </v-row>
          </v-container>
        </v-expansion-panel-content>
      </v-expansion-panel>
      <v-expansion-panel>
        <v-expansion-panel-header>( ... or Add/Remove Custom Bridge)</v-expansion-panel-header>
        <v-expansion-panel-content>add/remove bridge button</v-expansion-panel-content>
      </v-expansion-panel>
    </v-expansion-panels>
  </v-row>
</template>

<script>
const assetType = {
  native: "native",
  erc20: "erc20",
  arc1: "arc1"
};

const defaultBridges = [
  {
    bridge1: {
      net: {
        label: "Aergo testnet",
        type: "aergo",
        chainId: "testnet.aergo.io",
        endpoint: "127.0.0.1:3000",
        scan: "https://testnet.aergoscan.io/account/"
      },
      contract: { id: "AmfzMkaFchxxqg39mcSMkj1rnnBtUZUipDhLBi2H3ewDReJjzLGz" },
      asset: {
        label: "native aergo",
        type: assetType.native,
        isPegged: false,
        id: ""
      }
    },
    bridge2: {
      net: {
        label: "Ethereum testnet",
        type: "ethereum",
        chainId: "0x3",
        endpoint: "127.0.0.2:3000",
        scan: "https://ropsten.etherscan.io/address/"
      },
      contract: { id: "0xef27c1d9b1464e0edbcc69b429b872eb89877bd9" },
      asset: {
        label: "erc20 aergo",
        type: assetType.erc20,
        isPegged: false,
        id: "0xd898383A12CDE0eDF7642F7dD4D7006FdE5c433e"
      }
    }
  },
  {
    bridge1: {
      net: {
        label: "Aergo testnet",
        type: "aergo",
        chainId: "testnet.aergo.io",
        endpoint: "127.0.0.1:3000",
        scan: "https://testnet.aergoscan.io/account/"
      },
      contract: { id: "AmfzMkaFchxxqg39mcSMkj1rnnBtUZUipDhLBi2H3ewDReJjzLGz" },
      asset: {
        label: "arc1 gotchu",
        type: assetType.arc1,
        isPegged: true,
        id: "0xef27c1d9b1464e0edbcc69b429b872eb89877bd9"
      }
    },
    bridge2: {
      net: {
        label: "Ethereum testnet",
        type: "ethereum",
        chainId: "0x3",
        endpoint: "127.0.0.2:3000",
        scan: "https://ropsten.etherscan.io/address/"
      },
      contract: { id: "0xef27c1d9b1464e0edbcc69b429b872eb89877bd9" },
      asset: {
        label: "erc20 gotchu",
        type: assetType.erc20,
        isPegged: false,
        id: "0xef27c1d9b1464e0edbcc69b429b872eb89877bd9"
      }
    }
  }
];

export default {
  name: "BridgeSelect",
  components: {
    //
  },
  data: () => ({
    bridges: null,
    showFromMeta: false,
    showToMeta: false
  }),
  created() {
    localStorage.clear(); //FIXME remove this

    // set initail bridge configuration
    if (localStorage.getItem("_bridges") === null) {
      localStorage.setItem("_bridges", JSON.stringify(defaultBridges));
    }
    this.bridges = JSON.parse(localStorage.getItem("_bridges"));
  },
  methods: {
    getOpType(inOut, bridge) {
      if (inOut === "in") {
        if (
          bridge.asset.type === assetType.erc20 ||
          bridge.asset.type === assetType.arc1
        ) {
          if (bridge.asset.isPegged === true) {
            return "burn";
          } else {
            return "lock";
          }
        } else if (bridge.asset.type === assetType.native) {
          return "freeze";
        } else {
          /* eslint-disable no-console */
          console.log("unsuppored asset type", bridge.asset.type);
        }
      } else if (inOut === "out") {
        if (
          bridge.asset.type === assetType.erc20 ||
          bridge.asset.type === assetType.arc1
        ) {
          if (bridge.asset.isPegged === true) {
            return "mint";
          } else {
            return "unlock";
          }
        } else if (bridge.asset.type === assetType.native) {
          return "unfreeze";
        } else {
          /* eslint-disable no-console */
          console.log("unsuppored asset type", bridge.asset.type);
        }
      } else {
        /* eslint-disable no-console */
        console.log("unsuppored inOut value", inOut);
      }
    }
  }
};
</script>


<style>
</style>