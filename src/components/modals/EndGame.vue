<template>
  <div class="modal-container" id="endgame-modal">
    <div class="modal">
      <h1 class="modal-title">end game?</h1>
      <button v-on:click="resetGame()">confirm</button>
      <button v-on:click="closeModal($event)">cancel</button>
    </div>
  </div>
</template>
<script>
export default {
  name: "EndGame",
  methods: {
    resetGame(){
      location.reload(true);
    },
    closeModal(e){
      e.target.parentElement.parentElement.style.display = "none";
    },
  },
};
</script>
<style lang="less" scoped>
@import "../../styles/_variables.less";

</style>