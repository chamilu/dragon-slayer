<template>
  <div>
    <div id="content-wrapper">
      <player ref="player" v-on:addToCommentary="addToCommentary"></player>
      <dragon ref="dragon" v-on:addToCommentary="addToCommentary" ></dragon>
    </div>

    <hr>
    <actions 
      v-on:giveup="givingUp"
      v-on:heal="healing"
      v-on:powerAttack="powerAttacking"
      v-on:attack="attacking">
    </actions>
    <hr>
    <commentary ref="commentary"></commentary>
  </div>
</template>

<script>
import Actions from "./Actions.vue";
import Player from "./Player.vue";
import Dragon from "./Dragon.vue";
import Commentary from "./Commentary.vue";

export default {
  components: {
    actions: Actions,
    player: Player,
    dragon: Dragon,
    commentary: Commentary
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
    givingUp() {},
    addToCommentary(record) {
      console.log("=============", record);
      this.$refs.commentary.add(record);
    }
  }
};
</script>

<style>
#content-wrapper {
  display: table;
  width: 100%;
  padding: 10px;
  box-sizing: border-box;
  background-color: #ccc;
}

.progress-bar {
  width: 201px;
  border: 1px solid #555;
  margin: 0 auto;
}
.progress-bar .health {
  height: 21px;
  width: 100%;
  transition: all 0.5s ease;
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

