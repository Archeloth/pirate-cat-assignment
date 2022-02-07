<template>
  <div class="mb-4">
    <h1>Check out this Pirate Cat application!</h1>
    <p class="mb-4">
      Such wow! Much surprise! <br>
      Let the cat tell you a fun fact about itself!
    </p>
    <CatImage :catFact="$data.catFact" :isPirate="$data.isPirate"/>
    <div class="controls">
      <button class="mr-1" @click="piratify" ref="btnToggle">Piratify</button>
      <button @click="getCatFact">Get a new fact</button>
    </div>
  </div>
</template>

<script>
import CatImage from '../components/CatImage.vue'

export default {
  name: 'Index',
  components: {
    CatImage
  },
  data() {
    return {
      catFact: '',
      oldFact: '',
      isPirate: false
    }
  },
  methods: {
    piratify() {
      if(this.isPirate === false) {
        //this.catFact = "th' goddess o' love, beauty, and fertility in Norse mythology, Freyja were bein' th' first cat wench.  The winsome lass be depicted in stories as ridin' a chariot that were bein' drawn by cats.";
        
        fetch(`https://api.funtranslations.com/translate/pirate.json?text=${this.catFact}`)
          .then(response => response.json())
          .then(data => (this.catFact = data.contents.translated));
      } else {
        this.catFact = this.oldFact;
      }
      this.isPirate = !this.isPirate;
      this.$refs.btnToggle.innerText = this.isPirate ? 'Depiratify' : 'Piratify';
      
    },
    getCatFact() {
      //this.catFact = "The goddess of love, beauty, and fertility in Norse mythology, Freyja was the first cat lady. She is depicted in stories as riding a chariot that was drawn by cats.";
      //this.oldFact = "The goddess of love, beauty, and fertility in Norse mythology, Freyja was the first cat lady. She is depicted in stories as riding a chariot that was drawn by cats.";
      
      fetch('https://cat-fact.herokuapp.com/facts/random?animal_type=cat&amount=1')
        .then(response => response.json())
        .then(data => {
          this.catFact = data.text;
          this.oldFact = data.text;
          this.isPirate = false;
        });
    },
  },
  mounted() {
    this.getCatFact();
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
  .mb-4 {
    margin-bottom: 4em;
  }
  .mr-1 {
    margin-right: 1em;
  }
  button {
    background: black;
    transition: background .3s ease-in-out;
    color: white;
    border: none;
    padding: .5em 1em;
    font-size: 1.25em;
    border-radius: 10px;
  }
  button:hover {
    background: #545454;
    cursor: pointer;
  }
</style>
