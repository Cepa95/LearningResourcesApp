<template>
  <div>
    <ul>
      <li v-for="res in deletedResources" :key="res.id">
        <base-card>
          <h3>{{ res.title }}</h3>
          <p>{{ res.description }}</p>
          <nav>
            <a :href="res.link">View Resource</a>
          </nav>
        </base-card>
      </li>
    </ul>
    <div class="button-container">
      <button @click="clearHistory">Clear History</button>
    </div>
  </div>
</template>

<script>
export default {
  inject: ['deletedResources'],
  methods: {
    clearHistory() {
      this.deletedResources.splice(0, this.deletedResources.length);
    },
  },
};
</script>

<style scoped>
button {
  padding: 0.75rem 1.5rem;
  font-family: inherit;
  background-color: #3a0061;
  border: 1px solid #3a0061;
  color: white;
  cursor: pointer;
}

button:hover,
button:active {
  background-color: #00b8c0;
  border-color: #270041;
}

.button-container {
  display: flex;
  justify-content: center;
  margin-top: 1rem;
}

ul {
  list-style: none;
  margin: 0;
  padding: 0;
  margin: auto;
  max-width: 40rem;
}

a {
  text-decoration: none;
  color: #b25203;
}

a:hover,
a:active {
  color: #533c02;
}
</style>
