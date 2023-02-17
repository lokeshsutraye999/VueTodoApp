<template>
  <headerComponent/>
  <todoComponent/>
  <footerComponent/>
</template>

<script>
import headerComponent from './components/headerComponent.vue'
import footerComponent from './components/footerComponent.vue'
import todoComponent from './components/todoComponent.vue'

export default {
  name: 'App',
  components: {
    headerComponent,
    footerComponent,
    todoComponent
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
