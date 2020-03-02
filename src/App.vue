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
      <set-inventory :setParts='setParts'></set-inventory>
    </div>
  </div>
</template>

<script>
import SetDetails from './components/SetDetails.vue';
import SetInventory from './components/SetInventory.vue';
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
    "set-details": SetDetails,
    "set-inventory": SetInventory
  },
  // process.env.VUE_APP_EVN_LEGOAPI
  // API_KEY
  methods: {
    handleSearch(){
      fetch(`https://rebrickable.com/api/v3/lego/sets/${this.searchInput}/`, {
        headers: {
          'Authorization': 'key ' + API_KEY
        }})
      .then(res => res.json())
      .then(payload => this.legoSet = payload)
      // console.log(this.legoSet)
    },
    handlePartsRequest(setnum){
      fetch(`https://rebrickable.com/api/v3/lego/sets/${setnum}/parts/`, {
        headers: {
          'Authorization': 'key ' + API_KEY
        }})
      .then(res => res.json())
      .then(payload => this.setParts = payload.results)
      // console.log("Set number:", setnum)
    }
  },
  // ${this.setSelect}/parts/
  mounted() {
    eventBus.$on('request-parts', setnum => this.handlePartsRequest(setnum));
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
  margin-top: 30px;
  display: grid;
  height: 100%;
  grid-template-columns: 3% 25% 69% 3%;
  column-gap: normal;
}

#header {
  grid-column: 2 / 4;
}

h1 {
  padding: 9px;
  border: solid 3px black;
  border-radius: 10px;
  background-color: rgba(255, 255, 255, 0.8);

  /* opacity: 0.6; */
  /* font-size: 50px;
  font-weight: bold;
  color: white; */
  font-family: "Comic Sans MS", cursive, sans-serif;
  font-size: 34px;
  color: #FFFFFF;
  font-weight: 800;
  /* color: #bc2e1e; */
  text-shadow: 0 1px 0px #378ab4, 1px 0 0px #5dabcd, 1px 2px 1px #378ab4, 2px 1px 1px #5dabcd, 2px 3px 2px #378ab4, 3px 2px 2px #5dabcd, 3px 4px 2px #378ab4, 4px 3px 3px #5dabcd, 4px 5px 3px #378ab4, 5px 4px 2px #5dabcd, 5px 6px 2px #378ab4, 6px 5px 2px #5dabcd, 6px 7px 1px #378ab4, 7px 6px 1px #5dabcd, 7px 8px 0px #378ab4, 8px 7px 0px #5dabcd, 0px 0px 0px #CE2E15;
  color: #000000;
}

.search-bar {
  background-color: rgba(255, 255, 255, 0.8);
  border: solid black 3px;
  border-radius: 10px;
  padding: 5px;
  margin: 20px 5px 10px 5px;
  grid-column: 2;
}

.set-details {
  background-color: rgba(255, 255, 255, 0.8);
  /* width: 90%; */
  border: solid black 3px;
  border-radius: 10px;
  padding: 5px;
  margin: 20px 5px 10px 5px;
  grid-column: 2;
}

.parts-inventory {
  background-color: rgba(255, 255, 255, 0.8);
  /* width: 90%; */
  border: solid black 3px;
  border-radius: 10px;
  padding: 5px;
  margin: 20px 5px 10px 5px;
  grid-column: 3;
}

</style>
