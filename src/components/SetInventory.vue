<template lang="html">
  <div class="">
    <h2>Parts Inventory</h2>
    <ul>
      <li v-for="part in setParts" :setParts="setPart">
        <div class="">
          <img :src="part.part.part_img_url" alt="">
          <p>{{part.part.name}}</p>
          <p>Part no: {{part.inv_part_id}}   Color: {{part.color.name}}</p>
          <p>Qty: {{part.quantity}}</p>
        </div>
      </li>
    </ul>
  </div>
</template>

<script>
// import PartItem from './PartItem.vue';
import {eventBus} from '../main.js';

export default {
  name: 'set-inventory',
  props: ['setParts'],
  methods: {

  },
  components: {
    // "part-item": PartItem
  }
}
</script>

<style lang="css" scoped>
ul {
  display: flex;
  flex-wrap: wrap;
  justify-content: space-around;
  padding: 0;
}

li {
  background-color: white;
  border: solid 1px black;
  border-radius: 10px;
  list-style: none;
  width: 30%;
  margin: 2px;
}

p {
  font-weight: normal;
  font-size: 10px;
  padding-top: 2px;
}

img {
  width: 100px;
}
</style>
