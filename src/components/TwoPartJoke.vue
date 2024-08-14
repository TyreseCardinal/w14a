<template>
  <div class="container">
    <h2>Two Part Joke (Snake Form)</h2>
    <p>{{ snakeSetup }}</p>
    <button @click="toggleDelivery">{{ deliveryVisible ? 'Hide Delivery' : 'Show Delivery' }}</button>
    <p v-if="deliveryVisible">{{ snakeDelivery }}</p>
  </div>
</template>

<script>
export default {
  props: ['setup', 'delivery'],
  data() {
    return {
      deliveryVisible: false,
    };
  },
  computed: {
    snakeSetup() {
      return this.setup.replace(/ /g, '_');
    },
    snakeDelivery() {
      return this.delivery.replace(/ /g, '_');
    }
  },
  methods: {
    toggleDelivery() {
      this.deliveryVisible = !this.deliveryVisible;
    }
  }
};
</script>

<style scoped>
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
