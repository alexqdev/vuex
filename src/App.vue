<template>
  <div>
    <Nav />
    <Content v-bind:deck="deck" />
    <Footer />
  </div>
</template>

<script>
import Nav from "./components/Nav.vue";
import Content from "./components/Content.vue";
import Footer from "./components/Footer.vue";

export default {
  name: "App",
  components: {
    Nav,
    Content,
    Footer,
  },
  data() {
    return {
      deck: [
        {
          id: 1,
          name: "Ace",
          img: "https://i.imgur.com/PeZh1Bn.png",
        },
        {
          id: 2,
          name: "King",
          img: "https://i.imgur.com/z3jeQyB.png",
        },
        {
          id: 3,
          name: "Queen",
          img: "https://i.imgur.com/zS6C4wB.png",
        },
        {
          id: 4,
          name: "Jack",
          img: "https://i.imgur.com/Q95bAr6.png",
        },
        {
          id: 5,
          name: "Joker",
          img: "https://i.imgur.com/Y8DVYe6.png",
        },
        {
          id: 6,
          name: "Ace",
          img: "https://i.imgur.com/KEHzRYN.png",
        },
        {
          id: 7,
          name: "King",
          img: "https://i.imgur.com/BNWeHzU.png",
        },
        {
          id: 8,
          name: "Queen",
          img: "https://i.imgur.com/Y8ErS8Z.png",
        },
        {
          id: 9,
          name: "Jack",
          img: "https://i.imgur.com/CH7Crmf.png",
        },
      ],
    };
  },
};
</script>

<style lang="less">
@import "./styles/_variables.less";

* {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
  font-family: "Source Sans Pro", "Helvetica Neue", Arial, sans-serif;
  // z-index: -1;
}
body {
  // width: 100vw;
  // height: 100vh;
  background: @primary-color-dark;
  #app {
    position: relative;
    width: 100vw;
    height: 100vh;
    color: @text-color;
    font-size: 1.1em;
    text-transform: uppercase;
    button {
      background: @primary-color-dark;
      color: @text-color;
      text-transform: uppercase;
      border: 1px solid @primary-color;
      padding: 3px;
      cursor: pointer;
    }
    .modal-container {
      position: absolute;
      display: none;
      top: 25%;
      left: 50%;
      transform: translate(-50%);
      background: @primary-color-dark;
      max-width: 500px;
      width: 100%;
      min-height: 30vh;
      border: 1px solid @primary-color;
      padding: 10px;
      margin: 0 auto;
      z-index: 1;
      .modal {
        display: flex;
        flex-direction: column;
        justify-content: space-evenly;
        align-items: center;
        border: 1px solid @text-color;
        margin: 0 auto;
        width: 100%;
        // height: 100%;
        text-align: center;
        padding: 10px;
        gap: 10px 0;
        button {
          width: 50%;
        }
      }
    }
    #coinflip-modal {
      display: flex;
    }
  }
}
@media screen and(min-width:768px) {
  #app {
    button {
      font-size: 1.5em;
      width: 100px;
    }
  }
}
</style>
