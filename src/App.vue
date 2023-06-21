<script>
import Cat from './components/Cat.vue'

export default {
  name: 'DemoApp',
  components: {
    Cat
  },
  data() {
    return {
      activeCat: null,
      activeCatIndex: 0,
      catFacts: null,
    }
  },
  computed: {
    catData() {
      return [
        {
          id: '020fbb37-3785-47d7-9412-04a31ea8efb0',
          name: 'Mittens',
          picture: 'http://placekitten.com/200/200',
        },
        {
          id: 'beff6763-67ce-4ae5-ac86-80310fde7154',
          name: 'Bella',
          picture: 'http://placekitten.com/300/300',
        },
        {
          id: '616b318b-755b-41bf-a7d7-10f50bc91f78',
          name: 'Charlie',
          picture: 'http://placekitten.com/250/250',
        },
        {
          id: '7337c0bd-b33f-4da6-9782-5104c904a649',
          name: 'Daisy',
          picture: 'http://placekitten.com/275/275',
        },
        {
          id: '7475466a-bdd0-47bc-aa9d-bfd303ba17f2',
          name: 'Billy',
          picture: 'http://placekitten.com/350/350',
        }
      ]
    }
  },
  methods: {
    async fetchCatFacts() {
      const response = await fetch('https://cat-fact.herokuapp.com/facts')
      const jsonData = await response.json()
      this.catFacts = jsonData
    },
    async setCat(data, index) {
      await this.fetchCatFacts()
      this.activeCat = data
      this.activeCatIndex = index
    }
  }
}
</script>

<template>
  <div id="app">
    <span class="big-text">Cat Browser</span>

    <div class="cats">
      <Cat v-for="(cat, index) in catData" :key="index" :cat="cat" :active="activeCat" @set-cat="setCat($event, index)" />
    </div>

    <div v-if="activeCat" class="active-cat">
      <img :src="activeCat.picture" >
      <span class="medium-text">Random Cat Fact</span>
      <span>{{ catFacts[activeCatIndex].text }}</span>
    </div>
  </div>
</template>

<style scoped>

  #app {
    text-align: center;
  }

  .big-text {
    font-size: 2.5em;
    font-weight: bold;
    text-align: center;
    display: block;
    margin: 0 0 .5em;
  }

  .medium-text {
    font-size: 1.25em;
    font-weight: bold;
    display: block;
    margin: 1em 0;
  }

  .cats {
    overflow: auto;
    display: inline-block;
  }

  .cats:after {
    content: '';
    clear: both;
    display: block;
  }

  .cat {
    text-align: center; 
  }

  .active-cat {
    width: 400px;
    margin: 2rem auto 0;
    text-align: center;
  }

  .active-cat img {
    max-width: 200px;
    display: block;
    margin: 0 auto 1rem;
    object-fit: cover;
    object-position: center;
    border-radius: 10px;
  }

  .inactive {
    opacity: .4;
  }
</style>