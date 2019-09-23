<template>
  <div id="app">
    <Scouts
      @onScoutSelected="onSelected"
    />
    <Scout v-for="scout in scouts" v-bind="scout"  :key="scout.id">
      {{scout.name}}
    </Scout>
  </div>
</template>

<script>
import Scouts from './components/Scouts.vue'
import Scout from './components/Scout.vue'

export default {
  name: 'app',
  components: {
    Scouts,
    Scout,
  },
  data: () => ({
    scouts: [],
  }),
  methods: {
    onSelected: function (scout) {
      this.scouts.push(scout);
    }
  }
}
</script>

<style>
body {
  background-color: #31124a;
}
#app {
  font-family: Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #ffffff;
  margin: 16px;
}
</style>
