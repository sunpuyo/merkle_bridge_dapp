<template>
  <div>
    <v-text-field
      v-model="search"
      clearable
      hide-details
      prepend-inner-icon="mdi-account"
      label="To Address"
    ></v-text-field>
    <v-container>
      <v-row>
        <v-col cols="5">
          <v-card class="my-2" sm="1">
            <v-icon>mdi-sack</v-icon>
            <v-icon large>mdi-bank-transfer-in</v-icon>
            <br />
            <span class="display-1 font-weight-bold lime--text blinking">8334</span>
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
            <span class="display-1 font-weight-bold green--text">23959</span>
            <br />
            <span class="subtitle-1 grey--text">Arc1 Aergo</span>
            <v-divider class="mx-4"></v-divider>
            <span class="overline">Verified</span>
          </v-card>
        </v-col>
      </v-row>
    </v-container>

    <v-btn color="primary" :disabled="valid === false" @click="$emit('stepping', 'next');">Continue</v-btn>
    <v-btn text @click="$emit('stepping', 'prev');">Back</v-btn>
  </div>
</template>

<script>
export default {
  name: "Status",
  components: {
    //
  },
  data: () => ({
    search: "",
    valid: true,
  })
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