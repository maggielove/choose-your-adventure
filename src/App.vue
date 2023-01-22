<template>
  <div
    class="app"
     v-bind:style="{ backgroundColor: this.frames[selectedIndex].colors.bg }"
>
    <StoryFrame
        v-bind:frames="this.frames"
        v-bind:selectedIndex="this.selectedIndex"
    />
  </div>
</template>

<script>
import axios  from 'axios';
import StoryFrame from './components/StoryFrame.vue'

export default {
  name: 'App',
  components: {
    StoryFrame
  },
  data() {
    return {
        frames: [],
        selectedIndex: 1
    }
  },
  async created() {
    try {
        const res = await axios.get('http://localhost:3000/api/frames');
        this.frames = res.data;
    } catch (error) {
        console.log(error);
    }
  }
}
</script>

<style>
.app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  padding: 60px 0 60px 0;
}
</style>
