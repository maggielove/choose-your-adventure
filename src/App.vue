<template>
  <div id="app">
    <StoryFrame msg="Welcome Stranger"/>
  </div>
</template>

<script>
import StoryFrame from './components/StoryFrame.vue'

export default {
  name: 'App',
  components: {
    StoryFrame
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
