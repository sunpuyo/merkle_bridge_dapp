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

export default {}
</script>