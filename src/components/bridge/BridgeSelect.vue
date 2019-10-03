

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
                  <v-card-text class="pa-1 ">
                    <span class="text--primary">
                      {{item.bridge1.net.label}}
                      <v-icon>mdi-arrow-right</v-icon>
                      {{item.bridge2.net.label}}
                    </span>
                    <v-container fluid pa-0>
                      <v-row>
                        <v-col class="px-0">
                          <v-icon>mdi-sack</v-icon>
                          <v-icon large>mdi-bank-transfer-in</v-icon>
                          <br />
                          <v-btn color="primary" text @click="$emit('select-operation', 'send', item.bridge1, item.bridge2)">
                            <small>
                              Transfer
                              <br />
                              {{item.bridge1.asset.label}}
                            </small>
                          </v-btn>
                        </v-col>
                        <v-col class="px-0">
                          <v-icon large>mdi-weather-cloudy-arrow-right</v-icon>
                          <br />
                          <v-btn color="primary" text @click="$emit('select-operation', 'view', item.bridge1, item.bridge2)">
                            <small>
                              View
                              <br />Progress
                            </small>
                          </v-btn>
                        </v-col>
                        <v-col class="px-0">
                          <v-icon large>mdi-bank-transfer-out</v-icon>
                          <v-icon>mdi-sack</v-icon>
                          <br />
                          <v-btn color="primary" text @click="$emit('select-operation', 'receive', item.bridge1, item.bridge2)">
                            <small>
                              Get Swapped
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
                    <span class="text--primary">
                      {{item.bridge2.net.label}}
                      <v-icon>mdi-arrow-right</v-icon>
                      {{item.bridge1.net.label}}
                    </span>
                    <v-container fluid class="pa-0">
                      <v-row>
                        <v-col class="px-0">
                          <v-icon>mdi-sack</v-icon>
                          <v-icon large>mdi-bank-transfer-in</v-icon>
                          <br />
                          <v-btn color="primary" text @click="$emit('select-operation', 'send', item.bridge2, item.bridge1)">
                            <small>
                              Transfer
                              <br />
                              {{item.bridge2.asset.label}}
                            </small>
                          </v-btn>
                        </v-col>
                        <v-col class="px-0">
                          <v-icon large>mdi-weather-cloudy-arrow-right</v-icon>
                          <br />
                          <v-btn color="primary" text @click="$emit('select-operation', 'view', item.bridge2, item.bridge1)">
                            <small>
                              View
                              <br />Progress
                            </small>
                          </v-btn>
                        </v-col>
                        <v-col class="px-0">
                          <v-icon large>mdi-bank-transfer-out</v-icon>
                          <v-icon>mdi-sack</v-icon>
                          <br />
                          <v-btn color="primary" text @click="$emit('select-operation', 'receive', item.bridge2, item.bridge1)">
                            <small>
                              Get Swapped
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
      net: { label: "Aergo testnet", type: "aergo", chainid: "testnet.aergo.io", endpoint: "127.0.0.1:3000" },
      contract: { id: "fixmetodo" },
      asset: {
        label: "native aergo",
        type: assetType.native,
        isPegged: false,
        contractId: "addresTODO"
      }
    },
    bridge2: {
      net: { label: "Ethereum testnet", type: "ethereum", chainid: "0x2", endpoint: "127.0.0.2:3000" },
      contract: { id: "fixmetodo2" },
      asset: {
        label: "erc20 aergo",
        type: assetType.erc20,
        isPegged: false,
        contractId: "addresTODO2"
      }
    }
  },
  {
    bridge1: {
      net: { label: "Aergo testnet", type: "aergo", chainid: "testnet.aergo.io", endpoint: "127.0.0.1:3000" },
      contract: { id: "fixmetodo" },
      asset: {
        label: "arc1 gotchu",
        type: assetType.arc1,
        isPegged: true,
        contractId: "addresTODO"
      }
    },
    bridge2: {
      net: { label: "Ethereum testnet", type: "ethereum", chainid: "0x2", endpoint: "127.0.0.2:3000" },
      contract: { id: "fixmetodo2" },
      asset: {
        label: "erc20 gotchu",
        type: assetType.erc20,
        isPegged: false,
        contractId: "addresTODO2"
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
    bridges: null
  }),
  created() {
    localStorage.clear(); //FIXME remove this

    // set initail bridge configuration
    if (localStorage.getItem("_bridges") === null) {
      localStorage.setItem("_bridges", JSON.stringify(defaultBridges));
    }
    this.bridges = JSON.parse(localStorage.getItem("_bridges"));
  }
};
</script>


<style>
</style>