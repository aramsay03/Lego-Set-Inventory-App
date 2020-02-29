<template>
  <div id="app">
    <h1>Lego Set Parts Inventory</h1>
    <div class="search-bar">
      <label for="set-search">Search for set:</label>
      <input v-model="searchInput" type="text" id="set-search" required>
      <button @click="handleSearch" type="button" value="Search"></button>
    </div>
    <div class="set-details">

    </div>
    <div class="parts-inventory">

    </div>
  </div>
</template>

<script>
// import SetSearch from './components/SetSearch.vue';
import {eventBus} from './main.js';

const API_KEY='fd0886f85edf712d1b706a3b95a81c30'

export default {
  name: 'App',
    data() {
      return {
        searchInput: null,
        setParts: [],
        setDetails: []
      }
    },
  components: {

  },
  methods: {
    handleSearch(){
      fetch(`https://rebrickable.com/api/v3/lego/sets/${this.searchInput}/`, {
        headers: {
          'Authorization': 'key ' + API_KEY
        }})
      .then(res => res.json())
      .then(payload => this.setDetails = payload)
      console.log(this.setDetails)
    }
  },
  // ${this.setSelect}/parts/
  mounted() {

  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
