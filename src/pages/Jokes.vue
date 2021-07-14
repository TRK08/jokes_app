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
      likedJokes: [],
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
            if (joke.isLiked) {
              this.likedJokes.push(joke.id);
            } else {
              this.likedJokes.forEach((item, index) => {
                if (item === joke.id) {
                  this.likedJokes.splice(index, 1);
                }
              });
            }
            localStorage.setItem("likes", JSON.stringify(this.likedJokes));
          }

          return joke;
        });
      } else {
        return this.jokesByTitle.map((joke, i) => {
          if (i === index) {
            joke.isLiked = !joke.isLiked;
            console.log(joke.isLiked);
            if (joke.isLiked) {
              this.likedJokes.push(joke.id);
            } else {
              this.likedJokes.forEach((item, index) => {
                if (item === joke.id) {
                  this.likedJokes.splice(index, 1);
                }
              });
            }
            localStorage.setItem("likes", JSON.stringify(this.likedJokes));
          }

          return joke;
        });
      }
    },
    getJokes() {
      axios
        .get("https://v2.jokeapi.dev/joke/Any?amount=10")
        .then((res) => {
          let likes = JSON.parse(localStorage.getItem("likes"));
          this.likedJokes = likes;

          res.data.jokes.map((joke) => {
            joke.isOpen = false;
            joke.isLiked = false;
            this.likedJokes.forEach((item) => {
              if (joke.id === item) {
                joke.isLiked = true;
              }
            });
          });

          this.jokes = res.data.jokes;
        })
        .catch((err) => {
          console.log(err);
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
    this.getJokes();
  },
};
</script>

<style scoped>
h1 {
  text-align: center;
  margin-bottom: 15px;
}
</style>