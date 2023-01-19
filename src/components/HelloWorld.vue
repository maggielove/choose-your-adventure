<template>
  <div id="game-container">
    <h1>{{ msg }}</h1>
    <span id="index">1</span>
    <div id="narrative">
        <p>Gates, like books, are meant to be opened, and you would never be truly content if you did not know what lay on the other side. You pass through the gate and enter into a dark forest. You hesitate for a moment, look back, but the forest stretches behind you as if the garden had never been.</p><p>You continue on. Shadows deepen. An owl calls. Something cries out at a distance and is silenced. You grow chilled, and your feet develop a talent for finding uneven spots of ground, tree roots, and rocks. After the third time you fall, you lean against the very tree whose roots last tangled your feet. The bark prickles and rubs against your back, but it is a welcome distraction from your bruised knees and skinned palms. Your bones are weary and your muscles ache.</p><p>You crave sleep. A brief rest to fortify yourself for your journey. <b>Do you close your eyes?</b></p>
    </div>
    <div id="controls-container">
        <span class="control yes">Yes</span>
        <span class="control no">No</span>
    </div>
  </div>
</template>

<script>
export default {
  name: 'HelloWorld',
  props: {
    msg: String
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
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
