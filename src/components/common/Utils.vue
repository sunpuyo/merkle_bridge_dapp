<script>

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

export function loadReceivers() {
  const jsonItems = localStorage.getItem("savedReceivers");
  if (jsonItems) {
    return JSON.parse(jsonItems);
  }
  return [];
}

export function saveReceiver(receiver) {
  let parsedItems = [];
  const jsonItems = localStorage.getItem("savedReceivers");

  if (jsonItems) {
     parsedItems = JSON.parse(jsonItems);
  }
  //TODO prevent duplicate
  // push item to first
  parsedItems.unshift(receiver);

  // remove oldest history item
  if(parsedItems.length > 5) {
    parsedItems.pop();
  }

  localStorage.setItem("savedReceivers", JSON.stringify(parsedItems));
}

export default {};
</script>