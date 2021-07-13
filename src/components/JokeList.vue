<template>
  <div class="joke-list">
    <div class="joke-list__wrap">
      <div class="single-joke" v-for="(joke, index) in jokes" :key="joke.id">
        <div class="single-joke-head" @click="openAnswer(index)">
          {{ joke.setup || joke.joke }}
        </div>

        <div
          class="single-joke-body"
          v-if="joke.delivery"
          :class="joke.isOpen ? 'open' : ''"
        >
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
  methods: {
    // openAnswer(i) {
    //   this.jokes = this.jokes.map((joke, index) => {
    //     if (i === index && joke.delivery) {
    //       joke.isOpen = !joke.isOpen;
    //     }

    //     return joke;
    //   });
    // },
    openAnswer(i) {
      this.$emit("openAnswer", i);
    },
  },
  computed: {},
};
</script>

<style scoped>
</style>