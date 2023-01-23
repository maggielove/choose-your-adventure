<template>
  <div
    class="app"
    v-if="this.frames.length > 0"
    v-bind:style="{ backgroundColor: this.frames[selectedIndex].colors.bg }"
  >
    <StoryFrame
        v-bind:frames="this.frames"
        v-bind:selectedIndex="this.selectedIndex"
        @update_index="(controlIndex) =>
        this.selectedIndex = this.frames[this.selectedIndex].controls[controlIndex].linkindex"
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
        selectedIndex: 0
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
    display: grid;
    text-align: center;
    grid-template-columns: repeat(14, 1fr);
    grid-column-gap: 1%;
    justify-content: space-between;
    padding: 60px 0 60px 0;
    height: 90vh
}
</style>
