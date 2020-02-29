<template lang="html">
  <div :id="legoSet" class="details">
    <section class="left">
      <ul v-if="legoSet">
        <li>Set Name: {{legoSet.name}}</li>
        <li>Set Number: {{legoSet.set_num}}</li>
        <li>Year of lanch: {{legoSet.year}}</li>
        <li>Number of parts: {{legoSet.num_parts}}</li>
      </ul>
    </section>
    <section class="right">
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

  },
  components: {

  }
}

</script>

<style lang="css" scoped>
img {
  max-width: 200px;
  margin-right: 30px;
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
  /* justify-content: space-around; */
  /* width: 50%; */
}

div {
  display: flex;
  flex-direction: row;
  justify-content: space-around;
  width: 100%;
  padding: 50px;
}

.label {
  text-align: right;
}

.text {
  text-align: right;
}
</style>
