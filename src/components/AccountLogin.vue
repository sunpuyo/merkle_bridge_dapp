<template>
  <div>
    login or unlock your walllet
    <br />
    <div v-if="bridge !== null">
     <div  v-if="bridge.net.type==='aergo'">
       {{aergoaccount}}
      aergo
    </div>
    
    <div v-else-if="bridge.net.type==='ethereum'">
      {{etheraccount}}
      ethereum
      You are currently logged in as xxxx.
      Do you want to process using this account?
    </div>

    <div v-else>BUG: Unsupported Network Type {{bridge.net.type}}</div>
    </div>
    <br />

    <br />
  </div>
</template>

<script>
export default {
  name: "AccountLogin",
  props: ["bridge", "etheraccount", "aergoaccount"],
  components: {
    //
  },
  data: () => ({
    //
  })
};
</script>


<style>
</style>