<template>
  <div>
    <v-form ref="form" v-model="valid" lazy-validation>
      <v-text-field
        v-model="receiver"
        :rules="receiverRules"
        prepend-inner-icon="mdi-account"
        label="To Address"
        required
        clearable
      ></v-text-field>
      <v-container>
        <v-row>
          <v-col cols="5">
            <v-card class="my-2" sm="1">
              <v-icon>mdi-sack</v-icon>
              <v-icon large>mdi-bank-transfer-in</v-icon>
              <br />
              <span class="display-1 font-weight-bold lime--text blinking">1000</span>
              <br />
              <span class="subtitle-1 grey--text">Erc20 Aergo</span>
              <v-divider class="mx-4"></v-divider>
              <span class="caption">Under Verification</span>
            </v-card>
          </v-col>
          <v-col cols="2">
            <v-card class="my-2" sm="1">
              <v-icon large>mdi-calendar-clock</v-icon>
              <br />
              <span class="display-1 font-weight-bold red--text blinking">10</span>
              <br />
              <span class="subtitle-1 grey--text">Minutes</span>
              <v-divider class="mx-4"></v-divider>
              <span class="caption">Next Verification</span>
            </v-card>
          </v-col>
          <v-col cols="5">
            <v-card class="my-2" sm="1">
              <v-icon large>mdi-weather-cloudy-arrow-right</v-icon>
              <br />
              <span class="display-1 font-weight-bold green--text">{{verifiedAmount}}</span>
              <br />
              <span class="subtitle-1 grey--text">Arc1 Aergo</span>
              <v-divider class="mx-4"></v-divider>
              <span class="overline">Verified</span>
            </v-card>
          </v-col>
        </v-row>
      </v-container>

      <v-btn
        color="primary"
        :disabled="valid === false"
        @click="clickNext"
      >Continue</v-btn>
      <v-btn text @click="$emit('stepping', 1);">Back</v-btn>
    </v-form>
  </div>
</template>

<script>
export default {
  name: "Status",
  components: {
    //
  },
  data: () => ({
    receiver: "",
    receiverRules: [
      v => !!v || "Address is required",
    ],
    valid: false,
    verifiedAmount: 100000,
  }),
   methods: {
    clickNext() {
      this.$emit('update_finalize_info', this.receiver, this.verifiedAmount);
      this.$emit('stepping', 'next');
    }
   }
};
</script>


<style>
.blinking {
  animation: blinkingText 3s infinite;
}
@keyframes blinkingText {
  50% {
    color: transparent;
  }
}
</style>