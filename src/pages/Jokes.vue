<template>
  <div>
    <Search @search="getSearchValue" />
    <JokeList :jokes="jokesByTitle" />
  </div>
</template>

<script>
import axios from "axios";
import JokeList from "../components/JokeList";
import Search from "../components/Search";
export default {
  components: { Search, JokeList },
  name: "Jokes",
  data() {
    return {
      jokes: [],
      inputValue: "",
    };
  },
  methods: {
    getSearchValue(data) {
      this.inputValue = data;
    },
  },
  computed: {
    jokesByTitle() {
      return this.jokes.filter((joke) => {
        if (joke.setup) {
          return joke.setup.toLowerCase().indexOf(this.inputValue) !== -1;
        } else if (joke.joke) {
          return joke.joke.toLowerCase().indexOf(this.inputValue) !== -1;
        }
      });
    },
  },

  mounted() {
    axios
      .get("https://v2.jokeapi.dev/joke/Any?amount=10")
      .then((res) => {
        console.log(res.data);
        this.jokes = res.data.jokes;
      })
      .catch((err) => {
        console.log(err);
      });
  },
};
</script>

<style scoped>
</style>