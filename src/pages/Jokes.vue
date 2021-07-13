<template>
  <div class="app__wrap">
    <h1>Список анекдотов</h1>
    <Search @search="getSearchValue" />
    <JokeList
      :jokes="jokesByTitle"
      @openAnswer="toggleAnswer"
      @addLike="addLike"
    />
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
      if (this.inputValue === "") {
        return this.jokes.map((joke, i) => {
          if (i === index && joke.delivery) {
            joke.isOpen = !joke.isOpen;
          }

          return joke;
        });
      } else {
        return this.jokesByTitle.map((joke, i) => {
          if (i === index && joke.delivery) {
            joke.isOpen = !joke.isOpen;
          }

          return joke;
        });
      }
    },
    addLike(index) {
      if (this.inputValue === "") {
        return this.jokes.map((joke, i) => {
          if (i === index) {
            joke.isLiked = !joke.isLiked;
            console.log(joke.isLiked);
          }

          return joke;
        });
      } else {
        return this.jokesByTitle.map((joke, i) => {
          if (i === index) {
            joke.isLiked = !joke.isLiked;
            console.log(joke.isLiked);
          }

          return joke;
        });
      }
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
          joke.isLiked = false;
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
h1 {
  text-align: center;
  margin-bottom: 15px;
}
</style>