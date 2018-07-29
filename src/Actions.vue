<template>
  <div >
    <button @click="attack">Attack</button>
    <button @click="powerAttack">Power Attack</button>
    <button @click="heal">Heal</button>
    <button @click="giveup">Give up</button>
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

