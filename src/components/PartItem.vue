<template lang="html">
    <li v-for="part in setParts" :setParts="setPart">Set No: {{part.set_num}}
      <!-- <p>Name: {{part.part.name}}</p>
      <p>Qty: {{part.quantity}}</p> -->
    </li>
</template>

<script>
export default {
  name: 'part-item',
  props: ['setParts']
}
</script>

<style lang="css" scoped>
</style>
