<template>
  <div id="game-container">
      <h1 v-if="frames[selectedIndex]">{{ frames[selectedIndex].title }}</h1>
      <span id="index">{{ selectedIndex + 1 }}</span>
      <div id="narrative" v-html="frames[selectedIndex].content[0].text">
      </div>
      <ul id="controls-container">
          <li><button class="control left" v-if="frames[selectedIndex] && frames[selectedIndex].controls.length === 2" v-on:click="selectIndex(0)">{{ frames[selectedIndex].controls[0].text }}</button></li>
          <li><button class="control right" v-if="frames[selectedIndex] && frames[selectedIndex].controls.length === 2" v-on:click="selectIndex(1)">{{ frames[selectedIndex].controls[1].text }}</button></li>
          <li><button class="control right" v-if="frames[selectedIndex] && frames[selectedIndex].controls.length === 1" v-on:click="selectIndex(0)">{{ frames[selectedIndex].controls[0].text }}</button></li>
      </ul>
  </div>
</template>

<script>

export default {
  name: 'StoryFrame',
  props: {
    frames: Array,
    selectedIndex: Number
  }
}
</script>

<style>
ul {
  list-style-type: none;
  padding: 0;
}
</style>
