<script>
export const etherBridgeAbi = [
  {
    constant: true,
    inputs: [],
    name: "_anchorRoot",
    outputs: [
      {
        internalType: "bytes32",
        name: "",
        type: "bytes32"
      }
    ],
    payable: false,
    stateMutability: "view",
    type: "function"
  },
  {
    constant: true,
    inputs: [
      {
        internalType: "address",
        name: "",
        type: "address"
      }
    ],
    name: "_mintedTokens",
    outputs: [
      {
        internalType: "string",
        name: "",
        type: "string"
      }
    ],
    payable: false,
    stateMutability: "view",
    type: "function"
  },
  {
    constant: true,
    inputs: [
      {
        internalType: "bytes",
        name: "",
        type: "bytes"
      }
    ],
    name: "_locks",
    outputs: [
      {
        internalType: "uint256",
        name: "",
        type: "uint256"
      }
    ],
    payable: false,
    stateMutability: "view",
    type: "function"
  },
  {
    constant: false,
    inputs: [
      {
        internalType: "address",
        name: "receiver",
        type: "address"
      },
      {
        internalType: "uint256",
        name: "balance",
        type: "uint256"
      },
      {
        internalType: "string",
        name: "tokenOrigin",
        type: "string"
      },
      {
        internalType: "bytes32[]",
        name: "mp",
        type: "bytes32[]"
      },
      {
        internalType: "bytes32",
        name: "bitmap",
        type: "bytes32"
      },
      {
        internalType: "uint8",
        name: "leafHeight",
        type: "uint8"
      }
    ],
    name: "mint",
    outputs: [
      {
        internalType: "bool",
        name: "",
        type: "bool"
      }
    ],
    payable: false,
    stateMutability: "nonpayable",
    type: "function"
  },
  {
    constant: true,
    inputs: [
      {
        internalType: "string",
        name: "mapName",
        type: "string"
      },
      {
        internalType: "bytes",
        name: "accountRef",
        type: "bytes"
      },
      {
        internalType: "uint256",
        name: "balance",
        type: "uint256"
      },
      {
        internalType: "bytes32[]",
        name: "mp",
        type: "bytes32[]"
      },
      {
        internalType: "bytes32",
        name: "bitmap",
        type: "bytes32"
      },
      {
        internalType: "uint8",
        name: "leafHeight",
        type: "uint8"
      }
    ],
    name: "verifyMp",
    outputs: [
      {
        internalType: "bool",
        name: "",
        type: "bool"
      }
    ],
    payable: false,
    stateMutability: "view",
    type: "function"
  },
  {
    constant: true,
    inputs: [
      {
        internalType: "bytes",
        name: "",
        type: "bytes"
      }
    ],
    name: "_unlocks",
    outputs: [
      {
        internalType: "uint256",
        name: "",
        type: "uint256"
      }
    ],
    payable: false,
    stateMutability: "view",
    type: "function"
  },
  {
    constant: false,
    inputs: [
      {
        internalType: "address[]",
        name: "validators",
        type: "address[]"
      },
      {
        internalType: "uint256[]",
        name: "signers",
        type: "uint256[]"
      },
      {
        internalType: "uint8[]",
        name: "vs",
        type: "uint8[]"
      },
      {
        internalType: "bytes32[]",
        name: "rs",
        type: "bytes32[]"
      },
      {
        internalType: "bytes32[]",
        name: "ss",
        type: "bytes32[]"
      }
    ],
    name: "validatorsUpdate",
    outputs: [],
    payable: false,
    stateMutability: "nonpayable",
    type: "function"
  },
  {
    constant: true,
    inputs: [
      {
        internalType: "bytes",
        name: "",
        type: "bytes"
      }
    ],
    name: "_burns",
    outputs: [
      {
        internalType: "uint256",
        name: "",
        type: "uint256"
      }
    ],
    payable: false,
    stateMutability: "view",
    type: "function"
  },
  {
    constant: true,
    inputs: [
      {
        internalType: "bytes32",
        name: "bits",
        type: "bytes32"
      },
      {
        internalType: "uint8",
        name: "i",
        type: "uint8"
      }
    ],
    name: "bitIsSet",
    outputs: [
      {
        internalType: "bool",
        name: "",
        type: "bool"
      }
    ],
    payable: false,
    stateMutability: "pure",
    type: "function"
  },
  {
    constant: true,
    inputs: [],
    name: "_nonce",
    outputs: [
      {
        internalType: "uint256",
        name: "",
        type: "uint256"
      }
    ],
    payable: false,
    stateMutability: "view",
    type: "function"
  },
  {
    constant: false,
    inputs: [
      {
        internalType: "uint256",
        name: "tFinal",
        type: "uint256"
      },
      {
        internalType: "uint256[]",
        name: "signers",
        type: "uint256[]"
      },
      {
        internalType: "uint8[]",
        name: "vs",
        type: "uint8[]"
      },
      {
        internalType: "bytes32[]",
        name: "rs",
        type: "bytes32[]"
      },
      {
        internalType: "bytes32[]",
        name: "ss",
        type: "bytes32[]"
      }
    ],
    name: "tFinalUpdate",
    outputs: [],
    payable: false,
    stateMutability: "nonpayable",
    type: "function"
  },
  {
    constant: true,
    inputs: [
      {
        internalType: "bytes",
        name: "",
        type: "bytes"
      }
    ],
    name: "_mints",
    outputs: [
      {
        internalType: "uint256",
        name: "",
        type: "uint256"
      }
    ],
    payable: false,
    stateMutability: "view",
    type: "function"
  },
  {
    constant: true,
    inputs: [],
    name: "_tFinal",
    outputs: [
      {
        internalType: "uint256",
        name: "",
        type: "uint256"
      }
    ],
    payable: false,
    stateMutability: "view",
    type: "function"
  },
  {
    constant: true,
    inputs: [],
    name: "_anchorHeight",
    outputs: [
      {
        internalType: "uint256",
        name: "",
        type: "uint256"
      }
    ],
    payable: false,
    stateMutability: "view",
    type: "function"
  },
  {
    constant: true,
    inputs: [
      {
        internalType: "string",
        name: "",
        type: "string"
      }
    ],
    name: "_bridgeTokens",
    outputs: [
      {
        internalType: "contract MintedERC20",
        name: "",
        type: "address"
      }
    ],
    payable: false,
    stateMutability: "view",
    type: "function"
  },
  {
    constant: false,
    inputs: [
      {
        internalType: "uint256",
        name: "tAnchor",
        type: "uint256"
      },
      {
        internalType: "uint256[]",
        name: "signers",
        type: "uint256[]"
      },
      {
        internalType: "uint8[]",
        name: "vs",
        type: "uint8[]"
      },
      {
        internalType: "bytes32[]",
        name: "rs",
        type: "bytes32[]"
      },
      {
        internalType: "bytes32[]",
        name: "ss",
        type: "bytes32[]"
      }
    ],
    name: "tAnchorUpdate",
    outputs: [],
    payable: false,
    stateMutability: "nonpayable",
    type: "function"
  },
  {
    constant: true,
    inputs: [],
    name: "_contractId",
    outputs: [
      {
        internalType: "bytes32",
        name: "",
        type: "bytes32"
      }
    ],
    payable: false,
    stateMutability: "view",
    type: "function"
  },
  {
    constant: true,
    inputs: [],
    name: "getValidators",
    outputs: [
      {
        internalType: "address[]",
        name: "",
        type: "address[]"
      }
    ],
    payable: false,
    stateMutability: "view",
    type: "function"
  },
  {
    constant: true,
    inputs: [
      {
        internalType: "bytes32",
        name: "message",
        type: "bytes32"
      },
      {
        internalType: "uint256[]",
        name: "signers",
        type: "uint256[]"
      },
      {
        internalType: "uint8[]",
        name: "vs",
        type: "uint8[]"
      },
      {
        internalType: "bytes32[]",
        name: "rs",
        type: "bytes32[]"
      },
      {
        internalType: "bytes32[]",
        name: "ss",
        type: "bytes32[]"
      }
    ],
    name: "validateSignatures",
    outputs: [
      {
        internalType: "bool",
        name: "",
        type: "bool"
      }
    ],
    payable: false,
    stateMutability: "view",
    type: "function"
  },
  {
    constant: false,
    inputs: [
      {
        internalType: "contract IERC20",
        name: "token",
        type: "address"
      },
      {
        internalType: "uint256",
        name: "amount",
        type: "uint256"
      },
      {
        internalType: "string",
        name: "receiver",
        type: "string"
      }
    ],
    name: "lock",
    outputs: [
      {
        internalType: "bool",
        name: "",
        type: "bool"
      }
    ],
    payable: false,
    stateMutability: "nonpayable",
    type: "function"
  },
  {
    constant: false,
    inputs: [
      {
        internalType: "bytes32",
        name: "root",
        type: "bytes32"
      },
      {
        internalType: "uint256",
        name: "height",
        type: "uint256"
      },
      {
        internalType: "uint256[]",
        name: "signers",
        type: "uint256[]"
      },
      {
        internalType: "uint8[]",
        name: "vs",
        type: "uint8[]"
      },
      {
        internalType: "bytes32[]",
        name: "rs",
        type: "bytes32[]"
      },
      {
        internalType: "bytes32[]",
        name: "ss",
        type: "bytes32[]"
      }
    ],
    name: "newAnchor",
    outputs: [],
    payable: false,
    stateMutability: "nonpayable",
    type: "function"
  },
  {
    constant: true,
    inputs: [],
    name: "_tAnchor",
    outputs: [
      {
        internalType: "uint256",
        name: "",
        type: "uint256"
      }
    ],
    payable: false,
    stateMutability: "view",
    type: "function"
  },
  {
    constant: false,
    inputs: [
      {
        internalType: "string",
        name: "receiver",
        type: "string"
      },
      {
        internalType: "uint256",
        name: "amount",
        type: "uint256"
      },
      {
        internalType: "contract MintedERC20",
        name: "mintAddress",
        type: "address"
      }
    ],
    name: "burn",
    outputs: [
      {
        internalType: "bool",
        name: "",
        type: "bool"
      }
    ],
    payable: false,
    stateMutability: "nonpayable",
    type: "function"
  },
  {
    constant: false,
    inputs: [
      {
        internalType: "address",
        name: "receiver",
        type: "address"
      },
      {
        internalType: "uint256",
        name: "balance",
        type: "uint256"
      },
      {
        internalType: "contract IERC20",
        name: "token",
        type: "address"
      },
      {
        internalType: "bytes32[]",
        name: "mp",
        type: "bytes32[]"
      },
      {
        internalType: "bytes32",
        name: "bitmap",
        type: "bytes32"
      },
      {
        internalType: "uint8",
        name: "leafHeight",
        type: "uint8"
      }
    ],
    name: "unlock",
    outputs: [
      {
        internalType: "bool",
        name: "",
        type: "bool"
      }
    ],
    payable: false,
    stateMutability: "nonpayable",
    type: "function"
  },
  {
    constant: true,
    inputs: [
      {
        internalType: "uint256",
        name: "num",
        type: "uint256"
      }
    ],
    name: "uintToString",
    outputs: [
      {
        internalType: "string",
        name: "",
        type: "string"
      }
    ],
    payable: false,
    stateMutability: "pure",
    type: "function"
  },
  {
    constant: true,
    inputs: [
      {
        internalType: "uint256",
        name: "",
        type: "uint256"
      }
    ],
    name: "_validators",
    outputs: [
      {
        internalType: "address",
        name: "",
        type: "address"
      }
    ],
    payable: false,
    stateMutability: "view",
    type: "function"
  },
  {
    inputs: [
      {
        internalType: "address[]",
        name: "validators",
        type: "address[]"
      },
      {
        internalType: "uint256",
        name: "tAnchor",
        type: "uint256"
      },
      {
        internalType: "uint256",
        name: "tFinal",
        type: "uint256"
      }
    ],
    payable: false,
    stateMutability: "nonpayable",
    type: "constructor"
  },
  {
    anonymous: false,
    inputs: [
      {
        indexed: true,
        internalType: "string",
        name: "origin",
        type: "string"
      },
      {
        indexed: true,
        internalType: "contract MintedERC20",
        name: "addr",
        type: "address"
      }
    ],
    name: "newMintedERC20",
    type: "event"
  },
  {
    anonymous: false,
    inputs: [
      {
        indexed: true,
        internalType: "contract IERC20",
        name: "tokenAddress",
        type: "address"
      },
      {
        indexed: true,
        internalType: "string",
        name: "receiver",
        type: "string"
      },
      {
        indexed: false,
        internalType: "uint256",
        name: "amount",
        type: "uint256"
      }
    ],
    name: "lockEvent",
    type: "event"
  },
  {
    anonymous: false,
    inputs: [
      {
        indexed: true,
        internalType: "contract IERC20",
        name: "tokenAddress",
        type: "address"
      },
      {
        indexed: true,
        internalType: "address",
        name: "receiver",
        type: "address"
      },
      {
        indexed: false,
        internalType: "uint256",
        name: "amount",
        type: "uint256"
      }
    ],
    name: "unlockEvent",
    type: "event"
  },
  {
    anonymous: false,
    inputs: [
      {
        indexed: true,
        internalType: "contract MintedERC20",
        name: "tokenAddress",
        type: "address"
      },
      {
        indexed: true,
        internalType: "address",
        name: "receiver",
        type: "address"
      },
      {
        indexed: false,
        internalType: "uint256",
        name: "amount",
        type: "uint256"
      }
    ],
    name: "mintEvent",
    type: "event"
  },
  {
    anonymous: false,
    inputs: [
      {
        indexed: true,
        internalType: "contract MintedERC20",
        name: "tokenAddress",
        type: "address"
      },
      {
        indexed: true,
        internalType: "string",
        name: "receiver",
        type: "string"
      },
      {
        indexed: false,
        internalType: "uint256",
        name: "amount",
        type: "uint256"
      }
    ],
    name: "burnEvent",
    type: "event"
  },
  {
    anonymous: false,
    inputs: [
      {
        indexed: false,
        internalType: "bytes32",
        name: "root",
        type: "bytes32"
      },
      {
        indexed: false,
        internalType: "uint256",
        name: "height",
        type: "uint256"
      }
    ],
    name: "anchorEvent",
    type: "event"
  },
  {
    anonymous: false,
    inputs: [
      {
        indexed: false,
        internalType: "address[]",
        name: "validators",
        type: "address[]"
      }
    ],
    name: "newValidatorsEvent",
    type: "event"
  },
  {
    anonymous: false,
    inputs: [
      {
        indexed: false,
        internalType: "uint256",
        name: "tAnchor",
        type: "uint256"
      }
    ],
    name: "newTAnchorEvent",
    type: "event"
  },
  {
    anonymous: false,
    inputs: [
      {
        indexed: false,
        internalType: "uint256",
        name: "tFinal",
        type: "uint256"
      }
    ],
    name: "newTFinalEvent",
    type: "event"
  }
];

export const assetType = {
  native: "native",
  erc20: "erc20",
  arc1: "arc1"
};

export const defaultBridges = [
  {
    bridge1: {
      net: {
        label: "Ethereum Local",
        type: "ethereum",
        networkVersion: "52306",
        endpoint: "127.0.0.1:8545",
        scan: ""
      },
      contract: {
        id: "0x89eD1D1C145F6bF3A7e62d2B8eB0e1Bf15Cb2374",
        abi: etherBridgeAbi
      },
      asset: {
        label: "ERC20 Aergo",
        type: assetType.erc20,
        isPegged: false,
        id: "0xd898383A12CDE0eDF7642F7dD4D7006FdE5c433e"
      }
    },
    bridge2: {
      net: {
        label: "Aergo Local",
        type: "aergo",
        chainId: "mainnet",
        endpoint: "127.0.0.1:7845",
        scan: ""
      },
      contract: { id: "AmgQqVWX3JADRBEVkVCM4CyWdoeXuumeYGGJJxEeoAukRC26hxmw" },
      asset: {
        label: "Native Aergo",
        type: assetType.native,
        isPegged: false,
        id: ""
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
        networkVersion: "3",
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
        networkVersion: "3",
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
  web3local = new Web3(window.ethereum);
}
// Legacy dapp browsers...
else if (window.web3) {
  web3local = new Web3(window.web3.currentProvider); //window.web3 = new Web3(web3.currentProvider);
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
      new Address(address);
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