<template>
  <div id="player">
    <img src="./assets/warrior.gif">
    <div class="progress-bar">
      <div class="num">{{ health }}%</div>
      <div :class="cssClass" class="health" :style="{width: health + '%'}"></div>
    </div>
    <!-- <span>Player</span> -->
  </div>
</template>

<script>
function getRandomInt(min, max) {
  return Math.floor(Math.random() * (max - min + 1)) + min;
}
export default {
  data() {
    return {
      health: 100
    };
  },
  computed: {
    cssClass() {
      const health = this.health;
      if (health >= 75 && health <= 100) {
        return "best";
      } else if (health >= 50 && health < 75) {
        return "good";
      } else if (health >= 25 && health < 50) {
        return "average";
      } else {
        return "danger";
      }
    }
  },
  methods: {
    gotAttacked() {
      const reducedHealth = getRandomInt(1, 10);
      this.health -= reducedHealth;
      this.$emit(
        "addToCommentary",
        `Dragon attacks player for ${reducedHealth}%`
      );
    },
    pronedByPowerAttack() {
      const reducedHealth = getRandomInt(10, 20);
      this.health -= reducedHealth;
      this.$emit(
        "addToCommentary",
        `Player proned by power attack for ${reducedHealth}%`
      );
    },
    gotHealed() {
      if (this.health < 100) {
        const gainedHealth = getRandomInt(1, 10);
        this.health += gainedHealth;
        this.$emit(
          "addToCommentary",
          `Player gained health by ${gainedHealth}%`
        );
      }
    },
    giveUp() {
      this.health = 0;
      this.$emit("addToCommentary", `Player gave up.`);
    },
    resetHealth() {
      this.health = 100;
    }
  },
  watch: {
    health: function(newHealth, oldHealth) {
      if (newHealth < 0) {
        this.health = 0;
      } else if (newHealth === 0) {
        this.$emit("ko", "Dragon wins");
        this.$emit("addToCommentary", "Dragon wins !");
      }
    }
  }
};
</script>

<style>
#player {
  display: table-cell;
  text-align: center;
  vertical-align: middle;
}
#player img {
  width: 120px;
  margin-bottom: 15px;
}
</style>
