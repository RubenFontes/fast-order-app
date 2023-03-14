<template>
  <div id="main-banner">
    <h1>Pulcher Code</h1>
    <p>A modern web app built with Node.js and Vue.js</p>
  </div>
</template>

<script>
  export default {
    name: "Banner"
  }
</script>

<style scoped>

  #main-banner {
    background-color: #E6E8FF;
    height: 40vh;
    display: flex;
    flex-direction: column;
    text-align: center;
    justify-content: center;
  }

  #main-banner h1 {
    text-align: center;
    font-size: 60px;
    color: black;
  }

  #main-banner p{
    font-size: 26px;
    color: #2f365f;
  }

</style>