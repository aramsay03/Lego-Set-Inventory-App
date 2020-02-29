<template>
  <div id="app">
    <h1 id="header">Lego Set Parts Inventory</h1>
    <div class="search-bar">
      <label for="set-search">Search for set:</label>
      <input v-model="searchInput" type="text" id="set-search" required>
      <button @click="handleSearch" type="button" value="Search">Search</button>
    </div>
    <div class="set-details">
      <set-details :legoSet='legoSet'></set-details>
    </div>
    <div class="parts-inventory">

    </div>
  </div>
</template>

<script>
import SetDetails from './components/SetDetails.vue';
import {eventBus} from './main.js';

const API_KEY='fd0886f85edf712d1b706a3b95a81c30'

export default {
  name: 'App',
    data() {
      return {
        searchInput: null,
        setParts: [],
        legoSet: []
      }
    },
  components: {
    "set-details": SetDetails
  },
  methods: {
    handleSearch(){
      fetch(`https://rebrickable.com/api/v3/lego/sets/${this.searchInput}/`, {
        headers: {
          'Authorization': 'key ' + API_KEY
        }})
      .then(res => res.json())
      .then(payload => this.legoSet = payload)
      console.log(this.legoSet)
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
  display: grid;
  height: 100%;
  grid-template-columns: 5% 45% 45% 5%;
  column-gap: normal;
}

#header {
  grid-column: 2 / 4;
}

.search-bar {
  background-color: white;
  border: solid black 3px;
  border-radius: 10px;
  padding: 5px;
  margin: 20px 5px 10px 5px;
  grid-column: 2;
}

.set-details {
  background-color: white;
  /* width: 90%; */
  border: solid black 3px;
  border-radius: 10px;
  padding: 5px;
  margin: 20px 5px 10px 5px;
  grid-column: 2;
}

.parts-inventory {
  background-color: white;
  /* width: 90%; */
  border: solid black 3px;
  border-radius: 10px;
  padding: 5px;
  margin: 20px 5px 10px 5px;
  grid-column: 3;
}
</style>
