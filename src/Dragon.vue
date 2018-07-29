<template>
  <div id="dragon">
    <img src="./assets/dragon.gif">
    <div class="progress-bar">
      <div :class="cssClass" class="health" :style="{width: health + '%'}"></div>
    </div>
    <span>Dragon : {{ health }}% </span>
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
      console.log("dragon got attacked");
      const reducedHealth = getRandomInt(1, 10);
      this.health -= reducedHealth;
      this.$emit(
        "addToCommentary",
        `Player attacks dragon for ${reducedHealth}%`
      );
    },
    gotPowerAttacked() {
      console.log("dragon got power attacked");
      const reducedHealth = getRandomInt(10, 20);
      this.health -= reducedHealth;
      this.$emit(
        "addToCommentary",
        `Dragon got power attacked by player for ${reducedHealth}%`
      );
    },
    resetHealth() {
      this.health = 100;
    }
  },
  watch: {
    health: function(newHealth, oldHealth) {
      console.log("dragon new health: ", newHealth);
      if (newHealth <= 0) {
        this.health = 0;
        console.log("dragon dead");
        this.$emit("ko", "Dragon K.O. Player wins");
        this.$emit("addToCommentary", "Dragon K.O. Player wins");
      }
    }
  }
};
</script>

<style>
#dragon {
  display: table-cell;
  text-align: center;
}
#dragon img {
  height: 150px;
}
</style>
