<template>
  <div>
    <CoinFlip />
    <Rules />
    <Winner />
    <EndGame />
    <div id="content">
      <div class="img-container" v-bind:key="card.id" v-for="card in deck">
        <img
          class="content-card"
          v-on:click="cardHandler($event)"
          v-bind:id="card.id"
          v-bind:name="card.name"
          src="https://i.imgur.com/Ib4BQ6K.png"
          alt="card"
        />
      </div>
    </div>
  </div>
</template>
<script>
import CoinFlip from "./modals/CoinFlip.vue";
import EndGame from "./modals/EndGame.vue";
import Rules from "./modals/Rules.vue";
import Winner from "./modals/Winner.vue";

export default {
  name: "Content",
  components: {
    CoinFlip,
    Rules,
    Winner,
    EndGame,
  },
  props: {
    deck: Array,
  },
  data() {
    return {
      storedCards: [],
      activePlayer: "p1",
      gameData: [{ p1Score: 0 }, { p2Score: 0 }],
      contentCardCount: this.deck.length,
      ranDeck: this.deck.sort((a, b) => 0.5 - Math.random()),
    };
  },
  methods: {
    cardHandler(e) {
      if (e.target.name == "Joker") {
        this.jokerHandler(e);
      } else {
        if (this.storedCards.length < 2) {
          this.showCard(e);
          this.storeCard(e);
          this.compareStoredCards();
        } else {
          this.storedCards = [];
          this.showCard(e);
          this.storeCard(e);
        }
      }
    },
    jokerHandler(e) {
      if (this.storedCards.length == 0) {
        this.showCard(e);
        //
        if (this.activePlayer == "p1") {
          this.gameData[0].p1Score -= 5;
        } else {
          this.gameData[1].p2Score -= 5;
        }
        //
        setTimeout(() => {
          e.target.style.visibility = "hidden";
          e.target.src = "https://i.imgur.com/Ib4BQ6K.png";
          this.updateScoreDisplay();
        }, 1500);
        //
        this.contentCardCount -= 1;
      } else {
        this.showCard(e);
        this.storedCards = [];
        //
        this.contentCardCount -= 1;
        //
        if (this.activePlayer == "p1") {
          this.gameData[0].p1Score -= 5;
        } else {
          this.gameData[1].p2Score -= 5;
        }
        //
        const contentCards = Array.from(
          document.querySelectorAll(".content-card")
        );
        contentCards.forEach((card) => {
          if (
            card.src != "https://i.imgur.com/Ib4BQ6K.png" &&
            card.name != "Joker"
          ) {
            setTimeout(() => {
              card.src = "https://i.imgur.com/Ib4BQ6K.png";
              e.target.style.visibility = "hidden";
              e.target.src = "https://i.imgur.com/Ib4BQ6K.png";
              this.updateScoreDisplay();
            }, 1500);
          }
        });
        //
      }
      //
      if (this.contentCardCount == 0) {
        this.winnerDisplay();
      }
    },
    showCard(e) {
      this.deck.forEach((card) => {
        if (e.target.id == card.id) {
          e.target.src = card.img;
        }
      });
    },
    storeCard(e) {
      this.storedCards.push(e.target.name);
    },
    compareStoredCards() {
      if (this.storedCards.length == 2) {
        if (this.storedCards[0] == this.storedCards[1]) {
          this.matchTrue();
        } else {
          this.matchFalse();
        }
      }
    },
    matchTrue() {
      this.updateScore();
      const contentCards = Array.from(
        document.querySelectorAll(".content-card")
      );
      contentCards.forEach((card) => {
        if (card.src != "https://i.imgur.com/Ib4BQ6K.png") {
          this.contentCardCount -= 1;
          setTimeout(() => {
            card.style.visibility = "hidden";
            card.src = "https://i.imgur.com/Ib4BQ6K.png";
            this.updateScoreDisplay();
          }, 1500);
        }
      });
      if (this.contentCardCount == 0) {
        this.winnerDisplay();
      }
      this.storedCards = [];
    },
    updateScore() {
      if (this.activePlayer == "p1") {
        this.gameData[0].p1Score += 5;
      } else {
        this.gameData[1].p2Score += 5;
      }
    },
    updateScoreDisplay() {
      if (this.activePlayer == "p1") {
        document.querySelector(
          "#p1-score-display"
        ).innerHTML = `${this.gameData[0].p1Score}`;
      } else {
        document.querySelector(
          "#p2-score-display"
        ).innerHTML = `${this.gameData[1].p2Score}`;
      }
    },
    winnerDisplay() {
      document.querySelector("#winner-modal").style.display = "flex";
      if (this.gameData[0].p1Score > this.gameData[1].p2Score) {
        document.querySelector("#winner-display").innerHTML = `
          player 1 with ${this.gameData[0].p1Score} points!`;
      } else if (this.gameData[0].p1Score < this.gameData[1].p2Score) {
        document.querySelector("#winner-display").innerHTML = `
          player 2 with ${this.gameData[1].p2Score} points!`;
      } else {
        document.querySelector("#winner-display").innerHTML = `
          Tie!`;
      }
    },
    matchFalse() {
      setTimeout(() => {
        this.switchTurn();
      }, 1500);
      const contentCards = Array.from(
        document.querySelectorAll(".content-card")
      );
      contentCards.forEach((card) => {
        if (card.src != "https://i.imgur.com/Ib4BQ6K.png") {
          setTimeout(() => {
            card.src = "https://i.imgur.com/Ib4BQ6K.png";
          }, 1500);
        }
      });
      this.storedCards = [];
    },
    switchTurn() {
      this.updateActivePlayerDisplay();
    },
    updateActivePlayerDisplay() {
      if (this.activePlayer == "p1") {
        this.activePlayer = "p2";
        document.querySelector("#p2-display").style.color = "#4FC08D";
        document.querySelector("#p1-display").style.color = "#F6F6F6";
        this.updateScoreDisplay();
      } else {
        this.activePlayer = "p1";
        document.querySelector("#p2-display").style.color = "#F6F6F6";
        document.querySelector("#p1-display").style.color = "#4FC08D";
      }
    },
  },
};
</script>
<style lang="less">
@import "../styles/_variables.less";

#content {
  position: relative;
  display: flex;
  flex-wrap: wrap;
  justify-content: space-evenly;
  // align-items: center;
  .img-container {
    display: flex;
    justify-content: center;
    flex-basis: 31%;
    img {
      width: 100%;
    }
  }
}
@media screen and(min-width:768px) {
  #content {
    top: 2px;
    // gap: 20px 0;
    .img-container {
      img {
        width: 84%;
      }
    }
  }
}
@media screen and(min-width:1024px) {
  #content {
    .img-container {
      img {
        width: 28%;
        transform: rotate(90deg);
      }
    }
  }
}
@media screen and(min-width:1920px) {
  #content {
    .img-container {
      img {
        width: 30%;
      }
    }
  }
}
</style>