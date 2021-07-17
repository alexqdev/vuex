<template>
  <nav>
    <img src="https://i.imgur.com/gNBe10H.png" alt="vue logo" />
    <select>
      <option disabled>game type</option>
      <option selected>vs player</option>
    </select>
    <div id="score-display">
      <p id="p1-display">p1:<span id="p1-score-display">0</span></p>
      <span> | </span>
      <p id="p2-display">p2:<span id="p2-score-display">0</span></p>
    </div>
    <div id="nav-btns">
      <button id="rules-btn">rules</button>
      <button id="end-btn">end</button>
    </div>
  </nav>
</template>
<script>
const root = document.getElementById("app");
root.addEventListener("click", (e) => {
  switch (e.target.value) {
    case "vs player":
      location.reload(true);
      document.getElementById("coinflip-modal").style = "display:flex";
      break;
    default:
      break;
  }
  switch (e.target.textContent) {
    case "rules":
      document.getElementById("rules-modal").style = "display:flex";
      break;
    case "end":
      document.getElementById("endgame-modal").style = "display:flex";
      break;
    default:
      break;
  }
});

export default {
  name: "Nav",
};
</script>
<style lang="less">
@import "../styles/_variables.less";

nav {
  position: relative;
  top: 0;
  left: 0;
  height: 60px;
  display: flex;
  // justify-content: center;
  align-items: center;
  padding: 10px 5px;
  margin-bottom: 2px;
  border-bottom: 1px solid @primary-color;
  background: @primary-color-dark;
  width: 100%;
  img {
    width: 40px;
  }

  select {
    padding: 5px;
    margin: 5px;
    background: @primary-color-dark;
    border: 1px solid @primary-color;
    color: @text-color;
    text-transform: uppercase;
  }

  #score-display {
    display: flex;
    margin: 0 auto;
    gap: 0 15px;
  }

  #nav-btns {
    display: flex;
    flex-direction: column;
    gap: 5px;
  }
}
@media screen and(min-width:768px) {
  nav {
    height: 80px;
    img {
      width: 75px;
    }
    #score-display {
      font-size: 2.1em;
      gap: 0 35px;
    }
    #nav-btns {
      flex-direction: row;
      gap: 5px;
    }
  }
}
@media screen and(min-width:1440px) {
  nav {
    #nav-btns {
      flex-direction: row;
    }
  }
}
</style>
