<template>
  <div class="modal-container" id="coinflip-modal">
    <div class="modal">
      <h1 class="modal-title">Heads or Tails?</h1>
      <span id="coinflip-results">result</span>
      <button v-on:click="coinFlipHandler()">flip coin!</button>
    </div>
  </div>
</template>
<script>
export default {
  name: "CoinFlip",
  methods: {
    coinFlipHandler() {
      if (Math.floor(Math.random() * 2) < 1) {
        document.querySelector("#coinflip-results").innerHTML = "Heads";
      } else {
        document.querySelector("#coinflip-results").innerHTML = "Tails";
      }
      document.querySelector("#p1-display").style.color = "#4FC08D";
      document.querySelector("#coinflip-results").style.color = "#4FC08D";
      setTimeout(()=>{
        document.querySelector("#coinflip-modal").style.display = "none";
      },3000);
    },
  },
};
</script>
<style lang="less" scoped>
@import "../../styles/_variables.less";
</style>