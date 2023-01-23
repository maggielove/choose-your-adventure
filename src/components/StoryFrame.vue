<template>
  <div id="game-container" :style="cssProps">
      <h1 v-if="frames[selectedIndex]">{{ frames[selectedIndex].title }}</h1>
      <span id="index">{{ selectedIndex + 1 }}</span>
      <div v-if="frames[selectedIndex].content.length === 1" class="narrative text-only"
        v-html="frames[selectedIndex].content[0].text"
      >
      </div>
      <div v-if="frames[selectedIndex].content.length === 2" class="narrative illustrated">
        <div id="text" v-html="frames[selectedIndex].content[0].text">
        </div>
        <div id="illustration">
            <img v-bind:src="require('../assets/' + frames[selectedIndex].content[1].src)" />
        </div>
      </div>
      <ul class="controls-container" v-bind:class="{ 'single-button':
          frames[selectedIndex] && frames[selectedIndex].controls.length === 1 }"
      >
          <li v-if="frames[selectedIndex] && frames[selectedIndex].controls.length === 2"><button class="control left"
            v-on:click="$emit('update_index', 0)">{{ frames[selectedIndex].controls[0].text }}
            </button></li>
          <li v-if="frames[selectedIndex] && frames[selectedIndex].controls.length === 2"><button class="control right"
            v-on:click="$emit('update_index', 1)">{{ frames[selectedIndex].controls[1].text }}
          </button></li>
          <li v-if="frames[selectedIndex] && frames[selectedIndex].controls.length === 1"><button class="control right"
            v-on:click="$emit('update_index', 0)">{{ frames[selectedIndex].controls[0].text }}
        </button></li>
      </ul>
  </div>
</template>

<script>

export default {
  name: 'StoryFrame',
  props: {
    frames: Array,
    selectedIndex: Number
  },
  computed: {
    cssProps() {
        return {
            '--background-color': this.frames[this.selectedIndex].colors.bg,
            '--font-color': this.frames[this.selectedIndex].colors.text
        }
    }
  }
}
</script>

<style>
@font-face {
    font-family: "Basis Grotesque Pro";
    src: url("../assets/fonts/woff/sans-black.woff");
}

@font-face {
    font-family: "Graebenbach Mono";
    src: url("../assets/fonts/woff/mono-regular.woff");
    font-weight: regular;
}

@font-face {
    font-family: "Graebenbach Mono";
    src: url("../assets/fonts/woff/mono-black.woff");
    font-weight: bold;
}

#game-container {
    display: grid;
    grid-template-columns: repeat(11, 1fr);
    justify-content: center;
    border: 1rem solid var(--font-color);
    grid-column: 2 / 14;
    background-color: var(--background-color);
    color: var(--font-color);
}

h1, #index, .control {
    font-family: "Basis Grotesque Pro", sans-serif;
}

h1 {
    display: grid;
    text-transform: uppercase;
    grid-column: 2 / 11;
    font-size: 3.75rem;
    white-space: nowrap;
    color: var(--font-color);
}

#index {
    display: grid;
    grid-column: 13 / 14;
    font-size: 6.25rem;
    padding: 0 0 0 0.25em;
    line-height: 1;
    transform: translate(1rem, -1.5rem);
}

.narrative {
    display: grid;
    grid-column: 3 / 11;
    grid-auto-flow: column;
    grid-column-gap: 1fr;
    text-align: left;
    font-family: "Graebenbach Mono", sans-serif;
    font-weight: regular;
}

.narrative.text-only {
    display: block;
    columns: 2;
    column-gap: 10%;
}

.narrative.text-only p:first-child {
    margin-top: 0;
}

.narrative.illustrated {
    grid-template-columns: repeat(7, 1fr);
}

.narrative.illustrated #text {
    grid-column: 1 / 4;
}

.narrative.illustrated #illustration {
    display: grid;
    grid-auto-flow: column;
    grid-column: 5 / 8;
}

.narrative.illustrated img {
    max-width: 100%;
    max-height: 100%;
}

.controls-container {
    margin: 0;
    display: flex;
    justify-content: space-between;
    grid-column: 1 / 14;
    transform: translateY(1rem);
}

.controls-container.single-button {
    justify-content: end;
}

ul {
  list-style-type: none;
  padding: 0;
}

#index, .control, ul li {
  background-color: var(--background-color);
}

.control {
    margin: 0;
    font-size: 3rem;
    display: flex;
    padding: 0 0.5em;
    border: none;
    line-height: 1;
    background-color: var(--background-color);
    color: var(--font-color);
}

.control:hover {
    cursor: pointer;
}
</style>
