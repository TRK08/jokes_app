<template>
  <div>
    <div v-for="joke in jokes" :key="joke.id">
      {{ joke.setup || joke.joke }}
    </div>
  </div>
</template>

<script>
export default {
  name: "JokeList",
  props: {
    jokes: {
      type: Array,
      required: true,
    },
  },
};
</script>

<style scoped>
</style>