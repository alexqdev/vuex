<template>
    <div class="modal-container" id="winner-modal">
    <div class="modal">
      <h1 class="modal-title">Winner!</h1>
      <span id="winner-display">winner</span>
      <button v-on:click="resetGame()">play</button>
      <button v-on:click="closeModal($event)">quit</button>
    </div>
  </div>
</template>
<script>
  export default {
    name:'Winner',
      methods: {
    resetGame(){
      location.reload(true);
    },
    closeModal(e){
      e.target.parentElement.parentElement.style.display = "none";
    },
  },
  }
</script>
<style lang="less" scoped>
@import "../../styles/_variables.less";
</style>