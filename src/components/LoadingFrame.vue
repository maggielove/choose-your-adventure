<template>
  <div id="text-wrapper">
      <h1>loading</h1>
  </div>
</template>

<script>

export default {
  name: 'LoadingFrame',
}
</script>

<style scoped>
@font-face {
    font-family: "Basis Grotesque Pro";
    src: url("../assets/fonts/woff/sans-black.woff");
}

body {
    margin: 0 auto;
    position: absolute;
    width: 100%;
    height: 100%;
}

#text-wrapper {
    display: flex;
    grid-column: 2 / 14;
    flex-direction: row;
    align-items: center;
    justify-content: center;
    background-color: #916f04;
}

h1 {
    margin-top: 0;
    font-family: "Basis Grotesque Pro", sans-serif;
    color: #ffc100;
    text-transform: uppercase;
}

</style>
