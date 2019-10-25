<script>
export const erc20Abi = [
  {
    constant: true,
    inputs: [],
    name: "name",
    outputs: [{ name: "", type: "string" }],
    payable: false,
    stateMutability: "view",
    type: "function"
  },
  {
    constant: false,
    inputs: [
      { name: "_spender", type: "address" },
      { name: "_value", type: "uint256" }
    ],
    name: "approve",
    outputs: [{ name: "", type: "bool" }],
    payable: false,
    stateMutability: "nonpayable",
    type: "function"
  },
  {
    constant: true,
    inputs: [],
    name: "totalSupply",
    outputs: [{ name: "", type: "uint256" }],
    payable: false,
    stateMutability: "view",
    type: "function"
  },
  {
    constant: false,
    inputs: [
      { name: "_from", type: "address" },
      { name: "_to", type: "address" },
      { name: "_value", type: "uint256" }
    ],
    name: "transferFrom",
    outputs: [{ name: "", type: "bool" }],
    payable: false,
    stateMutability: "nonpayable",
    type: "function"
  },
  {
    constant: true,
    inputs: [],
    name: "decimals",
    outputs: [{ name: "", type: "uint8" }],
    payable: false,
    stateMutability: "view",
    type: "function"
  },
  {
    constant: false,
    inputs: [],
    name: "unpause",
    outputs: [],
    payable: false,
    stateMutability: "nonpayable",
    type: "function"
  },
  {
    constant: true,
    inputs: [],
    name: "paused",
    outputs: [{ name: "", type: "bool" }],
    payable: false,
    stateMutability: "view",
    type: "function"
  },
  {
    constant: false,
    inputs: [
      { name: "_spender", type: "address" },
      { name: "_subtractedValue", type: "uint256" }
    ],
    name: "decreaseApproval",
    outputs: [{ name: "success", type: "bool" }],
    payable: false,
    stateMutability: "nonpayable",
    type: "function"
  },
  {
    constant: true,
    inputs: [{ name: "_owner", type: "address" }],
    name: "balanceOf",
    outputs: [{ name: "", type: "uint256" }],
    payable: false,
    stateMutability: "view",
    type: "function"
  },
  {
    constant: false,
    inputs: [],
    name: "pause",
    outputs: [],
    payable: false,
    stateMutability: "nonpayable",
    type: "function"
  },
  {
    constant: true,
    inputs: [],
    name: "owner",
    outputs: [{ name: "", type: "address" }],
    payable: false,
    stateMutability: "view",
    type: "function"
  },
  {
    constant: true,
    inputs: [],
    name: "symbol",
    outputs: [{ name: "", type: "string" }],
    payable: false,
    stateMutability: "view",
    type: "function"
  },
  {
    constant: false,
    inputs: [
      { name: "_to", type: "address" },
      { name: "_value", type: "uint256" }
    ],
    name: "transfer",
    outputs: [{ name: "", type: "bool" }],
    payable: false,
    stateMutability: "nonpayable",
    type: "function"
  },
  {
    constant: false,
    inputs: [
      { name: "_spender", type: "address" },
      { name: "_addedValue", type: "uint256" }
    ],
    name: "increaseApproval",
    outputs: [{ name: "success", type: "bool" }],
    payable: false,
    stateMutability: "nonpayable",
    type: "function"
  },
  {
    constant: true,
    inputs: [
      { name: "_owner", type: "address" },
      { name: "_spender", type: "address" }
    ],
    name: "allowance",
    outputs: [{ name: "", type: "uint256" }],
    payable: false,
    stateMutability: "view",
    type: "function"
  },
  {
    constant: false,
    inputs: [{ name: "newOwner", type: "address" }],
    name: "transferOwnership",
    outputs: [],
    payable: false,
    stateMutability: "nonpayable",
    type: "function"
  },
  {
    inputs: [],
    payable: false,
    stateMutability: "nonpayable",
    type: "constructor"
  },
  { anonymous: false, inputs: [], name: "Pause", type: "event" },
  { anonymous: false, inputs: [], name: "Unpause", type: "event" },
  {
    anonymous: false,
    inputs: [
      { indexed: true, name: "previousOwner", type: "address" },
      { indexed: true, name: "newOwner", type: "address" }
    ],
    name: "OwnershipTransferred",
    type: "event"
  },
  {
    anonymous: false,
    inputs: [
      { indexed: true, name: "owner", type: "address" },
      { indexed: true, name: "spender", type: "address" },
      { indexed: false, name: "value", type: "uint256" }
    ],
    name: "Approval",
    type: "event"
  },
  {
    anonymous: false,
    inputs: [
      { indexed: true, name: "from", type: "address" },
      { indexed: true, name: "to", type: "address" },
      { indexed: false, name: "value", type: "uint256" }
    ],
    name: "Transfer",
    type: "event"
  }
];

export const aergoBridgeAbi = {
  version: "0.2",
  language: "lua",
  functions: [
    {
      name: "freeze",
      payable: true,
      arguments: [{ name: "receiver" }, { name: "amount" }]
    },
    {
      name: "constructor",
      arguments: [
        { name: "aergoErc20" },
        { name: "validators" },
        { name: "tAnchor" },
        { name: "tFinal" }
      ]
    },
    { name: "default", payable: true, arguments: [] },
    {
      name: "validatorsUpdate",
      arguments: [
        { name: "validators" },
        { name: "signers" },
        { name: "signatures" }
      ]
    },
    {
      name: "unfreeze",
      arguments: [
        { name: "receiver" },
        { name: "balance" },
        { name: "merkleProof" }
      ]
    },
    {
      name: "unlock",
      arguments: [
        { name: "receiver" },
        { name: "balance" },
        { name: "tokenAddress" },
        { name: "merkleProof" }
      ]
    },
    {
      name: "burn",
      arguments: [
        { name: "receiver" },
        { name: "amount" },
        { name: "mintAddress" }
      ]
    },
    {
      name: "tokensReceived",
      arguments: [
        { name: "operator" },
        { name: "from" },
        { name: "value" },
        { name: "receiver" }
      ]
    },
    {
      name: "mint",
      arguments: [
        { name: "receiver" },
        { name: "balance" },
        { name: "tokenOrigin" },
        { name: "merkleProof" }
      ]
    },
    {
      name: "unfreezeFeeUpdate",
      arguments: [{ name: "fee" }, { name: "signers" }, { name: "signatures" }]
    },
    {
      name: "newAnchor",
      arguments: [
        { name: "root" },
        { name: "height" },
        { name: "signers" },
        { name: "signatures" }
      ]
    },
    {
      name: "tAnchorUpdate",
      arguments: [
        { name: "tAnchor" },
        { name: "signers" },
        { name: "signatures" }
      ]
    },
    {
      name: "tFinalUpdate",
      arguments: [
        { name: "tFinal" },
        { name: "signers" },
        { name: "signatures" }
      ]
    }
  ],
  state_variables: [
    { name: "_unfreezes", type: "map" },
    { name: "_mintedTokens", type: "map" },
    { name: "_validators", type: "map" },
    { name: "_locks", type: "map" },
    { name: "_mints", type: "map" },
    { name: "_bridgeTokens", type: "map" },
    { name: "_aergoErc20Bytes", type: "value" },
    { name: "_tAnchor", type: "value" },
    { name: "_unfreezeFee", type: "value" },
    { name: "_burns", type: "map" },
    { name: "_validatorsCount", type: "value" },
    { name: "_contractId", type: "value" },
    { name: "_anchorRoot", type: "value" },
    { name: "_anchorHeight", type: "value" },
    { name: "_tFinal", type: "value" },
    { name: "_nonce", type: "value" },
    { name: "_unlocks", type: "map" }
  ]
};

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
        endpoint: "http://127.0.0.1:8545",
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
        id: "0xd898383A12CDE0eDF7642F7dD4D7006FdE5c433e",
        abi: erc20Abi
      }
    },
    bridge2: {
      net: {
        label: "Aergo Local",
        type: "aergo",
        chainId: "mainnet",
        endpoint: "http://127.0.0.1:7845",
        scan: ""
      },
      contract: { id: "AmgQqVWX3JADRBEVkVCM4CyWdoeXuumeYGGJJxEeoAukRC26hxmw", abi: aergoBridgeAbi },
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
        endpoint: "http://127.0.0.1:3000",
        scan: "https://testnet.aergoscan.io/account/"
      },
      contract: { id: "AmfzMkaFchxxqg39mcSMkj1rnnBtUZUipDhLBi2H3ewDReJjzLGz", abi: aergoBridgeAbi },
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
      contract: { id: "0xef27c1d9b1464e0edbcc69b429b872eb89877bd9", abi: etherBridgeAbi },
      asset: {
        label: "erc20 aergo",
        type: assetType.erc20,
        isPegged: false,
        id: "0xd898383A12CDE0eDF7642F7dD4D7006FdE5c433e",
        abi: erc20Abi
      }
    }
  },
  {
    bridge1: {
      net: {
        label: "Aergo testnet",
        type: "aergo",
        chainId: "testnet.aergo.io",
        endpoint: "http://127.0.0.1:3000",
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
import { web3 } from "./Web3Loader";
import { utils } from "eth-merkle-bridge-js";

export function validateAddress(netType, address) {
  if (!address) {
    return "Address is required";
  } else if (netType == "aergo") {
    try {
      new Address(address);
      utils.checkAergoAddress(address);
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