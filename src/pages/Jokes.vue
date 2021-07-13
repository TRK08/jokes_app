<template>
  <div class="app__wrap">
    <Search @search="getSearchValue" />
    <JokeList :jokes="jokesByTitle" @openAnswer="toggleAnswer" />
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
    toggleAnswer(index) {
      return this.jokes.map((joke, i) => {
        if (i === index && joke.delivery) {
          joke.isOpen = !joke.isOpen;
          console.log(joke.isOpen);
        }

        return joke;
      });
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
        res.data.jokes.map((joke) => {
          joke.isOpen = false;
        });
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