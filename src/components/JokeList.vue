<template>
  <div class="joke-list">
    <div class="joke-list__wrap">
      <div class="single-joke" v-for="joke in jokes" :key="joke.id">
        <div class="single-joke-head">{{ joke.setup || joke.joke }}</div>

        <div class="single-joke-body" v-if="joke.delivery">
          {{ joke.delivery }}
        </div>
      </div>
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