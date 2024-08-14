<template>
  <div id="app">
    <JokeButton />
    <TwoPartJoke setup="Why did the chicken cross the road?" delivery="To get to the other side!" />
    <SearchJoke />
  </div>
</template>

<script>
import JokeButton from './components/JokeButton.vue';
import TwoPartJoke from './components/TwoPartJoke.vue';
import SearchJoke from './components/SearchJoke.vue';

export default {
  components: {
    JokeButton,
    TwoPartJoke,
    SearchJoke
  }
};
</script>

<style>
#app {
  text-align: center;
  background-color: #f4f4f4;
  min-height: 100vh;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
}

.container {
  margin-bottom: 20px;
}
</style>
