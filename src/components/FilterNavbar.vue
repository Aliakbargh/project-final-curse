<template>
  <nav class="filter-nav">
    <button @click="updataFilter('all')" :class="{ active: current === 'all' }">
      View all
    </button>
    <button
      @click="updataFilter('copmalete')"
      :class="{ active: current === 'copmalete' }"
    >
      Copmalete
    </button>
    <button
      @click="updataFilter('Ongoing')"
      :class="{ active: current === 'Ongoing' }"
    >
      Ongoing
    </button>
  </nav>
</template>

<script>
export default {
  props: ["current"],
  methods: {
    updataFilter(by) {
      this.$emit("changeFilter", by);
    },
  },
};
</script>

<style>
.filter-nav button {
  display: inline-block;
  text-decoration: none;
  margin: 0 10px;
  color: #afafaf;
  font-size: 18px;
  border: none;
  cursor: pointer;
}
.filter-nav button.active {
  color: #2b2b2b;
}
</style>