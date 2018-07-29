<template>
  <div id="wrapper">
    <ul v-if="records.length > 0">
      <li :key="index" v-for="(record, index) in records">
        {{ record }}
      </li>
    </ul>
    <p v-if="records.length === 0">No commentary</p>
  </div>
</template>

<script>
export default {
  data() {
    return {
      records: []
    };
  },
  methods: {
    add(newRecord) {
      this.records.unshift(newRecord);
    }
  }
};
</script>

<style>
#wrapper {
  max-height: 300px;
  overflow-y: auto;
}
</style>
