<template>
  <div id="game-container" :style="cssProps">
      <span id="index">{{ selectedIndex + 1 }}</span>
      <h1 v-if="frames[selectedIndex]">{{ frames[selectedIndex].title }}</h1>
      <div v-if="frames[selectedIndex].content.length === 1" class="narrative text-only"
        v-html="frames[selectedIndex].content[0].text"
      >
      </div>
      <div v-if="frames[selectedIndex].content.length === 2" class="narrative illustrated">
        <div id="text" v-html="frames[selectedIndex].content[0].text">
        </div>
        <div id="illustration">
            <img v-bind:src="require('../assets/' + frames[selectedIndex].content[1].src)"
                v-bind:alt="frames[selectedIndex].content[1].alt"
            />
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
    display: flex;
    flex-direction: column;
    grid-row: 2 / 14;
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
    display: flex;
    margin: 0 calc(100% / 11);
    font-size: 3.75rem;
    color: var(--font-color);
    text-transform: uppercase;
    letter-spacing: 0.4rem;
    justify-content: center;
}

#index {
    display: flex;
    align-self: flex-end;
    font-size: 6.25rem;
    padding: 0 0 0.1em 0.2em;
    line-height: 1;
    transform: translate(1rem, -1.5rem);
}


.controls-container {
    margin: 0;
    display: flex;
    justify-content: space-between;
    align-items: flex-end;
    grid-column: 1 / 14;
    grid-row: 11 / 12;
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

.narrative {
    display: grid;
    padding: 20px calc(100% / 11) calc(100% / 11) calc(100% / 11);
    grid-column: 2 / 12;
    grid-row: 4 / 10;
    grid-auto-flow: column;
    text-align: left;
}

.narrative p {
    font-family: "Graebenbach Mono", sans-serif;
    font-weight: normal;
    font-size: 0.8125rem;
    line-height: 1.46;
    letter-spacing: 0;
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
    display: flex;
    flex-direction: row;
    /* keeps 1 column width between frame and bottom of narrative */
    align-items: flex-end;
    justify-content: space-between;
}

.narrative.illustrated #text {
    display: flex;
    flex-direction: column;
    align-self: flex-start;
    max-width: 40%;
}

.narrative.illustrated #illustration {
    display: flex;
    max-width: 40%;
}

.narrative.illustrated img {
    max-width: 100%;
    max-height: 100%;
}

@media only screen and (max-width: 1086px) {
    h1 {
        line-height: 1;
    }

    .narrative {
        margin-top: 1rem;
    }
}

@media only screen and (max-width: 764px) {
    .app.loaded {
        height: 100%;
    }

    #game-container {
        display: flex;
        flex-direction: column;
    }

    #index {
        padding-bottom: 0;
        align-self: flex-end;
    }

    h1 {
        font-size: 2rem;
        letter-spacing: 0.1rem;
    }

    .narrative {
        display: flex;
        grid-row-start: 3;
        text-align: center;
        margin-top: 8px;
        max-width: 80%;
        align-self: center;
    }

    .narrative.illustrated {
        display: flex;
        flex-wrap: wrap;
        flex-direction: column;
        align-content: space-around;
    }

    .narrative.illustrated #text {
        display: flex;
        flex-direction: column;
        max-width: 80%;
    }

    .narrative.illustrated #illustration {
        display: flex;
        max-width: 80%;
        margin-top: 1.5rem;
    }

    .narrative.text-only {
        display: flex;
        flex-direction: column;
    }
}
</style>
