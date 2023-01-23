<template>
  <div
    class="app"
    :style="cssProps"
    v-bind:class="{'loading' : this.isLoading === true, 'loaded' : this.isLoading === false }"
  >
    <LoadingFrame v-if="this.isLoading === true" />
    <StoryFrame
        v-else-if="this.isLoading === false"
        v-bind:frames="this.frames"
        v-bind:selectedIndex="this.selectedIndex"
        @update_index="(controlIndex) =>
        this.selectedIndex = this.frames[this.selectedIndex].controls[controlIndex].linkindex" />
  </div>
</template>

<script>
import axios  from 'axios';
import StoryFrame from './components/StoryFrame.vue'
import LoadingFrame from './components/LoadingFrame.vue'

export default {
  name: 'App',
  components: {
    StoryFrame,
    LoadingFrame
  },
  data() {
    return {
        isLoading: true,
        frames: [],
        selectedIndex: 0
    }
  },
  async created() {
    try {
        const res = await axios.get('http://localhost:3000/api/frames');
        this.frames = res.data;
        this.isLoading = false;
    } catch (error) {
        console.log(error);
    }
  },
  computed: {
    cssProps() {
        return {
            '--background-color': this.frames[this.selectedIndex].colors.bg
        }
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
    height: 100%;
}

.app.loading {
    background-color: #ffc100;
    width: 100vw;
    height: 100vh;
}

.app.loaded {
    background-color: var(--background-color);
}

</style>
