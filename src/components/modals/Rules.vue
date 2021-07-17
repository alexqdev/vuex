<template>
  <div class="modal-container" id="rules-modal">
    <div class="modal">
      <h1 class="modal-title">rules</h1>
      <p>
        OBJECTIVE: Score more points than your opponent by matching cards <br />
        -A coin flip determines who goes first <br />
        -Matched cards = +5 points<br />
        -Joker card = -5 points (do not lose turn)<br />
        -Game is over once all cards are matched or game is ended manually
      </p>
      <button v-on:click="closeModal($event)">close</button>
    </div>
  </div>
</template>
<script>
export default {
  name: "Rules",
  methods: {
    closeModal(e) {
      e.target.parentElement.parentElement.style.display = "none";
    },
  },
};
</script>
<style lang="less" scoped>
@import "../../styles/_variables.less";
.modal {
  p {
    text-align: left;
    text-transform: capitalize;
    font-size: 0.9em;
  }
}
</style>