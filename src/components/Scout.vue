<template>
  <div class="root">
    <div class="name">
      {{name}}
    </div>
  </div>
</template>

<script>
export default {
  name: 'Scout',
  props: {
    id: { type: String },
    name: {type: String},
  },
}
</script>

<style scoped>
.root {
  padding: 16px;
  background-color: #d3d3d3;
  margin: 4px 0;
  width: 480px;
}
.name {
  color: #000000;
  text-transform: capitalize;
  font-size: 16px;
}
</style>