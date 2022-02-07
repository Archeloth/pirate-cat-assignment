<template>
  <div class="cat-container">
    <img src="https://placekitten.com/300/300" alt="Cat picture">
    <div class="speach-bubble" :class="{ 'bg-map': isPirate }">
      {{ catFact }}
      <div class="left-point"></div>
    </div>
    <div v-if="isPirate">
      <img class="pirate-hat" src="../assets/piratehat.png" alt="Pirate Hat">
      <img class="eye-patch" src="../assets/eyepatch.png" alt="Pirate Eye Patch">
    </div>
  </div>
</template>

<script>
export default {
  name: 'CatImage',
  props: {
    catFact: String,
    isPirate: Boolean
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
  .cat-container {
    position: relative;
    display: inline-block;
  }
  .speach-bubble {
    position: absolute;
    top: -50px;
    right: -150px;
    background-color: white;
    border: 1px solid gray;
    border-radius: 10%;
    word-break: break;
    padding: 2em;
    width: 150px;
    font-weight: bold;
    z-index: 10;
  }
  .left-point{
    width: 0;
    height: 0;
    border-left: 2vh solid transparent;
    border-right: 2vh solid transparent;
    border-top: 10vh solid white;
    position: absolute;
    top: 45%;
    left: -10%;
    transform: rotate(60deg);
  }
  .pirate-hat {
    position: absolute;
    top: 0;
    left: 15%;
    width: 200px;
  }
  .eye-patch {
    position: absolute;
    top: 20%;
    right: 35%;
    width: 100px;
  }
  .bg-map {
    background: url('../assets/piratemap.png');
    border: none;
  }
  .bg-map .left-point {
    border-top-color: #e0bc8a;
  }
  @media (max-width: 600px) {
    .cat-container {
      margin-top: 15em;
    }
    .speach-bubble {
      top: -250px;
      right: 0;
    }
    .left-point {
      top: 100%;
      left: 45%;
      transform: rotate(0deg);
    }
  }

</style>
