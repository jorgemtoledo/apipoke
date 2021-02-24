<template>
  <div id="app">
    <div v-for="(poke,index) in pokes" :key="index">
      <!-- <h1>{{ index + 1 }} {{ poke.name }}</h1> -->
      <Poke :name="poke.name" :url="poke.url" :num="index + 1" />
    </div>  
  </div>
</template>

<script>
import axios from 'axios';
import Poke from './components/Poke';

export default {
  name: 'App',
  data() {
    return {
      pokes: []
    }
  },
  created: function() {
    axios.get('https://pokeapi.co/api/v2/pokemon?limit=151&offset=0').then(res => {
      this.pokes = res.data.results;
      console.log(this.pokes);
    })
  },
  components: {
    Poke
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
