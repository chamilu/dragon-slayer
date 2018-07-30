<template>
  <div id="dragon">
    <img src="./assets/dragon.gif">
    <div class="progress-bar">
      <div class="num">{{ health }}%</div>
      <div :class="cssClass" class="health" :style="{width: health + '%'}"></div>
    </div>
    <!-- <span>Dragon </span> -->
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
        `Player attacks dragon for ${reducedHealth}%`
      );
    },
    gotPowerAttacked() {
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
      if (newHealth <= 0) {
        this.health = 0;
        this.$emit("ko", "Hazzaa... Good job warrior. To the next dragon...");
        this.$emit("addToCommentary", "Player wins !");
      }
    }
  }
};
</script>

<style>
#dragon {
  display: table-cell;
  text-align: center;
  vertical-align: middle;
}
#dragon img {
  width: 120px;
}
</style>
