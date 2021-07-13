<template>
  <div>
    <Search />
    <JokeList />
  </div>
</template>

<script>
import JokeList from "../components/JokeList.vue";
import Search from "../components/Search";
export default {
  components: { Search, JokeList },
  name: "JokeList",
};
</script>

<style scoped>
</style>