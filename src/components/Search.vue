<template>
  <div>
    <input v-model="inputValue" type="text" @input="search" />
  </div>
</template>

<script>
export default {
  name: "Search",
  data() {
    return {
      inputValue: "",
    };
  },
  methods: {
    search() {
      this.$emit("search", this.inputValue.toLowerCase());
    },
  },
};
</script>

<style scoped>
</style>