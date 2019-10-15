<script>
export const assetType = {
  native: "native",
  erc20: "erc20",
  arc1: "arc1"
};

export const defaultBridges = [
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

import { Address } from "@herajs/client";
import Web3 from "web3";

var web3local;

// load ethereum web3
// Modern dapp browsers...
if (window.ethereum) {
  web3local = new Web3(ethereum);
}
// Legacy dapp browsers...
else if (window.web3) {
  web3local = new Web3(web3.currentProvider); //window.web3 = new Web3(web3.currentProvider);
}
// Non-dapp browsers...
else {
  /* eslint-disable no-console */
  console.error("no metamask");
  web3local = new Web3(
    new Web3.providers.HttpProvider("http://localhost:8545")
  );
}

export const web3 = web3local;

export function validateAddress(netType, address) {
  if (netType == "aergo") {
    try {
      var addr = new Address(address);
      return true; // no error
    } catch (error) {
      return error.message;
    }
  } else if (netType == "ethereum") {
    try {
      web3.utils.toChecksumAddress(address);
      return true; // no error
    } catch (error) {
      return error.message;
    }
  }
  return "unknown network type " + netType;
}

export default {};
</script>