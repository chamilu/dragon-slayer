<template>
  <div id="wrapper">
    <div class="inner-wrapper">
      <button @click="attack">Attack</button>
      <button @click="powerAttack">Power Attack</button>
      <button @click="heal">Heal</button>
      <button @click="giveup">Give up</button>
    </div>
  </div>
</template>

<script>
export default {
  methods: {
    attack() {
      this.$emit("attack");
    },
    powerAttack() {
      this.$emit("powerAttack");
    },
    heal() {
      this.$emit("heal");
    },
    giveup() {
      this.$emit("giveup");
    }
  }
};
</script>

<style scoped>
#wrapper {
  text-align: center;
  background-color: #ccd1d7;
  height: 8vh;
  display: table;
  width: 100%;
}

.inner-wrapper {
  display: table-cell;
  vertical-align: middle;
}

button {
  font-family: "Cabin", sans-serif;
  font-size: 13px;
  margin: 5px;
  width: 100px;
  cursor: pointer;
  height: 31px;
}

@media only screen and (max-width: 500px) {
  button {
    width: auto;
  }
}
</style>
