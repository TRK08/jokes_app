<template>
  <div class="joke-list">
    <div class="joke-list__wrap">
      <div
        class="single-joke"
        v-for="(joke, index) in jokes"
        :key="joke.id"
        :class="joke.isLiked ? 'like' : ''"
      >
        <div class="single-joke-head">
          <p @click="openAnswer(index)">{{ joke.setup || joke.joke }}</p>
          <span @click="addLike(index)">like</span>
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
    openAnswer(i) {
      this.$emit("openAnswer", i);
    },
    addLike(i) {
      this.$emit("addLike", i);
    },
  },
  computed: {},
};
</script>

<style scoped>
</style>