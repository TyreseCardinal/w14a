<template>
  <div class="container">
    <h1>Random Joke Generator</h1>
    <button @click="getJoke">Get a New Joke</button>
    <p v-if="joke">{{ joke }}</p>
    <div v-if="joke">
      <button @click="modifyJoke('normal')">Normal Joke</button>
      <button @click="modifyJoke('loud')">Loud Joke</button>
      <button @click="modifyJoke('snake')">Snake Joke</button>
    </div>
  </div>
</template>

<script>
import axios from 'axios';

export default {
  data() {
    return {
      joke: '',
      originalJoke: ''
    };
  },
  methods: {
    async getJoke() {
      try {
        const response = await axios.get('https://v2.jokeapi.dev/joke/Programming?blacklistFlags=nsfw,religious,political,racist,sexist,explicit&type=single');
        if (response.data.type === 'twopart') {
          this.originalJoke = `${response.data.setup} ... ${response.data.delivery}`;
        } else {
          this.originalJoke = response.data.joke;
        }
        this.joke = this.originalJoke;
      } catch (error) {
        console.error(error);
      }
    },
    modifyJoke(type) {
      switch (type) {
        case 'loud':
          this.joke = this.originalJoke.toUpperCase();
          break;
        case 'snake':
          this.joke = this.originalJoke.replace(/ /g, '_');
          break;
        default:
          this.joke = this.originalJoke;
      }
    }
  }
};
</script>

<style scoped>
.container {
  text-align: center;
}

p {
  background-color: #C3E0E5;
  padding: 15px;
  border-radius: 5px;
  margin-top: 10px;
}

/* Basic button styling */
button {
  background-color: #274472;
  /* Primary color */
  color: #FFFFFF;
  /* Text color */
  padding: 12px 24px;
  /* Padding */
  font-size: 16px;
  /* Font size */
  border: none;
  /* No border */
  border-radius: 5px;
  /* Rounded corners */
  cursor: pointer;
  /* Pointer cursor on hover */
  transition: background-color 0.3s ease, transform 0.2s ease;
  /* Smooth transition */
  box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
  /* Subtle shadow */
  margin: 0px 1.5rem;
}

/* Hover effect */
button:hover {
  background-color: #C3E0E5;
  /* Secondary color on hover */
  color: #274472;
  /* Text color changes on hover */
  transform: scale(1.05);
  /* Slightly enlarges the button */
}

/* Active button effect */
button:active {
  transform: scale(0.95);
  /* Slightly shrinks the button on click */
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.2);
  /* Changes shadow on click */
}

/* Button focus outline */
button:focus {
  outline: none;
  /* Removes default outline */
  box-shadow: 0 0 0 3px rgba(195, 224, 229, 0.6);
  /* Custom focus outline */
}

button:hover::after {
  transform: scaleX(1);
}
</style>
