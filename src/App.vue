<template>
  <div>
    <header>
      Dragon Slayer
    </header>
    <modal v-if="showModal" @playAgain="playAgain" :message="modalMessage"></modal>
    <div id="content-wrapper">
      <player ref="player" v-on:addToCommentary="addToCommentary" @ko="endOfGame"></player>
      <dragon ref="dragon" v-on:addToCommentary="addToCommentary" @ko="endOfGame"></dragon>
    </div>

   
    <actions 
      @giveup="givingUp"
      @heal="healing"
      @powerAttack="powerAttacking"
      @attack="attacking">
    </actions>
 
    <commentary ref="commentary"></commentary>
  </div>
</template>

<script>
import Actions from "./Actions.vue";
import Player from "./Player.vue";
import Dragon from "./Dragon.vue";
import Commentary from "./Commentary.vue";
import Modal from "./Modal.vue";

export default {
  data() {
    return {
      showModal: false,
      modalMessage: ""
    };
  },
  components: {
    actions: Actions,
    player: Player,
    dragon: Dragon,
    commentary: Commentary,
    modal: Modal
  },
  methods: {
    attacking() {
      this.$refs.dragon.gotAttacked();
      this.$refs.player.gotAttacked();
    },
    powerAttacking() {
      this.$refs.dragon.gotPowerAttacked();
      this.$refs.player.pronedByPowerAttack();
    },
    healing() {
      this.$refs.player.gotHealed();
      this.$refs.player.gotAttacked();
    },
    givingUp() {
      this.$refs.player.giveUp();
    },
    addToCommentary(record) {
      this.$refs.commentary.add(record);
    },
    endOfGame(message) {
      this.modalMessage = message;
      this.showModal = true;
    },
    playAgain() {
      this.showModal = false;
      this.$refs.dragon.resetHealth();
      this.$refs.player.resetHealth();
    }
  }
};
</script>

<style>
header {
  font-family: "Lobster", cursive;
  background-color: #2c3e50;
  text-align: center;
  color: #fff;
  font-size: 40px;
  line-height: 10vh;
}

#content-wrapper {
  display: table;
  width: 100%;
  box-sizing: border-box;
  height: 32vh;
}

.progress-bar {
  width: 29vw;
  border: 1px solid #555;
  margin: 0 auto;
  padding: 2px;
  position: relative;
}
.progress-bar .health {
  height: 27px;
  width: 100%;
  transition: all 0.5s ease;
}
.progress-bar .num {
  position: absolute;
  text-align: center;
  width: 100%;
  line-height: 27px;
}

.progress-bar .health.best {
  background-color: #6ab04c;
}
.progress-bar .health.good {
  background-color: #f9ca24;
}
.progress-bar .health.average {
  background-color: #f0932b;
}
.progress-bar .health.danger {
  background-color: #eb4d4b;
}
</style>

