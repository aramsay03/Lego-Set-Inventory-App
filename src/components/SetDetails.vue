<template lang="html">
  <div :id="legoSet" class="sticky-container">
    <section class="left">
      <ul v-if="legoSet">
        <li>Set Name: {{legoSet.name}}</li>
        <li>Set Number: {{legoSet.set_num}}</li>
        <li>Year of lanch: {{legoSet.year}}</li>
        <li>Number of parts: {{legoSet.num_parts}}</li>
      </ul>
      <button @click="handlePartsClick(legoSet.set_num)"type="button" name="button">View Parts List</button><br>
      <img :src="legoSet.set_img_url" alt="">
    </section>
  </div>
</template>

<script>
import {eventBus} from '../main.js';

export default {
  name: 'set-details',
  props: ['legoSet'],
  methods: {
    handlePartsClick(setnum){
      eventBus.$emit('request-parts', setnum)
    }
  },
  components: {

  }
}

</script>

<style lang="css" scoped>
img {
  max-width: 200px;
  margin: 20px;
  /* max-height: inherit; */
}

section .left {
  width: 50%;
}

section .right {
  width: 50%;
}

li {
  display: flex;
  list-style: none;
  line-height: 20px;
  padding: 0px;
  /* justify-content: space-around; */
  /* width: 50%; */
}

div {
  display: flex;
  flex-direction: row;
  justify-content: center;
  width: 100%;
  /* padding: 50px; */
}

.label {
  text-align: right;
}

.text {
  text-align: right;
}

.sticky-container {
    position: sticky;
    top: 0;
}

</style>
