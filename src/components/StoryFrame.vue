<template>
  <div id="game-container">
    <h1 v-if="frames[selectedIndex]">{{ frames[selectedIndex].title }}</h1>
    <span id="index">{{ selectedIndex + 1 }}</span>
    <div id="narrative">
        <p>Gates, like books, are meant to be opened, and you would never be truly content if you did not know what lay on the other side. You pass through the gate and enter into a dark forest. You hesitate for a moment, look back, but the forest stretches behind you as if the garden had never been.</p><p>You continue on. Shadows deepen. An owl calls. Something cries out at a distance and is silenced. You grow chilled, and your feet develop a talent for finding uneven spots of ground, tree roots, and rocks. After the third time you fall, you lean against the very tree whose roots last tangled your feet. The bark prickles and rubs against your back, but it is a welcome distraction from your bruised knees and skinned palms. Your bones are weary and your muscles ache.</p><p>You crave sleep. A brief rest to fortify yourself for your journey. <b>Do you close your eyes?</b></p>
    </div>
    <ul id="controls-container">
        <li><button class="control left" v-if="frames[selectedIndex] && frames[selectedIndex].controls.length === 2" v-on:click="selectIndex(0)">{{ frames[selectedIndex].controls[0].text }}</button></li>
        <li><button class="control right" v-if="frames[selectedIndex] && frames[selectedIndex].controls.length === 2" v-on:click="selectIndex(1)">{{ frames[selectedIndex].controls[1].text }}</button></li>
        <li><button class="control right" v-if="frames[selectedIndex] && frames[selectedIndex].controls.length === 1" v-on:click="selectIndex(0)">{{ frames[selectedIndex].controls[0].text }}</button></li>
    </ul>
  </div>
</template>

<script>
import axios  from 'axios';

export default {
  name: 'StoryFrame',
  data() {
    return {
        frames: [],
        selectedIndex: 1,
        styleObject: {
            backgroundColor: '#ffc100'
        }
    }
  },
  async created() {
    try {
        const res = await axios.get('http://localhost:3000/api/frames');
        this.frames = res.data;
    } catch (error) {
        console.log(error);
    }
  },
  props: {
    msg: String
  },
  methods: {
    selectIndex: function(controlIndex) {
        if (controlIndex === 0) {
            this.selectedIndex = this.frames[this.selectedIndex].controls[0].linkindex;
        } else if (controlIndex === 1) {
            this.selectedIndex = this.frames[this.selectedIndex].controls[1].linkindex;
        }
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
a {
  color: #42b983;
}
</style>
