<template>
  <div>
    <v-form ref="form" v-model="valid" lazy-validation>
      <v-text-field
        v-model="aergoAddress"
        :counter="10"
        :rules="aergoAddressRules"
        label="To Address"
        required
      ></v-text-field>
       <v-text-field
        v-model="amount"
        :rules="amountRules"
        label="Amount"
        required
      ><span slot="append" v-if="bridge">{{bridge.asset.label}}</span> </v-text-field>
      <v-text-field
        v-model="gas"
        :rules="gasRules"
        label="Gas"
        required
      ><span slot="append">g-wei</span></v-text-field>
    </v-form>

    <v-btn
      color="primary"
      :disabled="valid === false"
      @click="$emit('stepping', 'next');"
    >Send Tx</v-btn>
    <v-btn text @click="$emit('stepping', 'prev');">Back</v-btn>
  </div>
</template>

<script>
export default {
  name: "Send",
  props: ["bridge"],
  components: {
    //
  },
  data: () => ({
    valid: true,
    aergoAddress: "",
    aergoAddressRules: [
      v => !!v || "Address is required",
      v => (v && v.length <= 10) || "Name must be less than 10 characters"
    ],
    amount: "",
    amountRules:[],
    gas: "",
    gasRules:[],
  })
};
</script>


<style>
</style>