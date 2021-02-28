<template>
<div class="container">
  <section class="section">
    <!-- https://github.com/BulmaTemplates/bulma-templates/blob/master/templates/cards.html#L65 -->
    <!-- https://bulmathemes.com/ -->
    <!-- https://bulmatemplates.github.io/bulma-templates/templates/cards.html -->
    <div id="app" class="container has-text-centered">
      <div class="column is-half is-offset-one-quarter">
        <h2 id="poke-title">Poke list</h2>
        <input type="text" name="" placeholder="Buscar poke pelo nome" v-model="busca" class="input is-rounded">
        <button class="button is-fullwidth is-success" id="buscaBtn" @click="buscar">Buscar</button>
        <div v-for="(poke,index) in filteredPokes" :key="poke.url">
          <!-- <h1>{{ index + 1 }} {{ poke.name }}</h1> -->
          <Poke :name="poke.name" :url="poke.url" :num="index + 1" />
        </div>
      </div>
    </div>
  </section>  
</div>
</template>

<script>
import axios from 'axios';
import Poke from './components/Poke';

export default {
  name: 'App',
  data() {
    return {
      pokes: [],
      filteredPokes: [],
      busca: ''
    }
  },
  created: function() {
    axios.get('https://pokeapi.co/api/v2/pokemon?limit=151&offset=0').then(res => {
      this.pokes = res.data.results;
      this.filteredPokes = res.data.results;
      // console.log(this.pokes);
    })
  },
  components: {
    Poke
  },
  methods: {
    buscar: function(){
      this.filteredPokes = this.pokes;
      if(this.busca == '' || this.busca == ' ') {
        this.filteredPokes = this.pokes;
      } else {
        this.filteredPokes = this.pokes.filter(poke => poke.name == this.busca);
      }

    }
  },
  computed: {
    /*
    resultadoBusca: function(){
      if(this.busca == '' || this.busca == ' '){
        return this.pokes;
      } else {
        return this.pokes.filter(poke => poke.name == this.busca);
      }
    }
    */
  }
}
</script>

<style>
  .navbar {
    background: var(--card-bg);
  }

  .navbar-item {
    color: ghostwhite;
  }

  #app {
    font-family: Avenir, Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    text-align: center;
    color: #2c3e50;
    margin-top: 60px;
  }

  #poke-title {
    font-size: 35px;
    font-weight: bold;
  }

  #buscaBtn {
    margin-top: 2%;
  }

</style>
