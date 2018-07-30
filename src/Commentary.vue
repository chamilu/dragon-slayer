<template>
  <div id="wrapper">
    <ul v-if="records.length > 0">
      <li :key="index" v-for="(record, index) in records">
        {{ record }}
      </li>
    </ul>
    <!-- <p v-if="records.length === 0">No commentary</p> -->
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

<style scoped>
#wrapper {
  height: 50vh;
  overflow-y: auto;
  padding: 20px;
  box-sizing: border-box;
  background-color: #f1f1f1;
}

#wrapper p {
  text-align: center;
}

ul {
  list-style: none;
  margin: 0;
  padding: 0;
}

li {
  text-align: center;
  padding: 6px 0;
  font-size: 14px;
}
</style>
