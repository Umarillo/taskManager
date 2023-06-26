<template>
  <nav class="filter-nav">
    <button @click="updateFilter('all')" :class="{ active: current == 'all' }">
      View all
    </button>
    <button
      @click="updateFilter('complate')"
      :class="{ active: current == 'complate' }">
      Completed
    </button>
    <button
      @click="updateFilter('process')"
      :class="{ active: current == 'process' }">
      Process
    </button>
  </nav>
</template>

<script>
export default {
  props: ["current"],
  methods: {
    updateFilter(by) {
      this.$emit("updateProject", by);
    },
  },
};
</script>

<style scoped>
.filter-nav button {
  background: none;
  border: none;
  outline: none;
  margin-left: 15px;
  font-size: 16px;
  text-transform: uppercase;
  margin-right: 15px;
  letter-spacing: 1px;
  font-weight: bold;
  cursor: pointer;
  padding: 5px;
}
.filter-nav button.active {
  color: blue;
}
</style>
