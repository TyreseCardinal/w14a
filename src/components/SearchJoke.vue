<template>
  <div class="container">
    <h2>Search for a Joke</h2>
    <input v-model="query" placeholder="Enter a word" />
    <button @click="searchJoke">Search Joke</button>
    <p v-if="joke">{{ joke }}</p>
  </div>
</template>

<script>
import axios from 'axios';

export default {
  data() {
    return {
      query: '',
      joke: ''
    };
  },
  methods: {
    async searchJoke() {
      try {
        const response = await axios.get(`https://v2.jokeapi.dev/joke/Any?contains=${this.query}`);
        if (response.data.type === 'twopart') {
          this.joke = `${response.data.setup} ... ${response.data.delivery}`;
        } else {
          this.joke = response.data.joke;
        }
      } catch (error) {
        console.error(error);
      }
    }
  }
};
</script>

<style scoped>
input {
  display: block;
  margin: 0 auto;
}

p {
  background-color: #C3E0E5;
  padding: 15px;
  border-radius: 5px;
  font-family: 'Courier New', Courier, monospace;
  font-size: 16px;
  color: #333;
  margin-bottom: 10px;
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
  margin-top: 1rem;
}

/* Hover effect */
button:hover {
  background-color: #C3E0E5;
  /* Secondary color on hover */
  color: #274472;
  /* Text color changes on hover */
  transform: scale(0.95);
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
