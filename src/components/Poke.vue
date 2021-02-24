<template>
  <div id="poke">
    <div class="card">
      <div class="card-image">
        <figure>
          <img :src="currentImag" alt="Placeholder image">
        </figure>
      </div>
      <div class="card-content">
        <div class="media">
          <div class="media-content">
            <p class="title is-4">{{num}} - {{name | upper}}</p>
            <p class="subtitle is-6">{{this.poke.type}}</p>
          </div>
        </div>
        <div class="content">
          <button class="button is-medium is-fullwidth" @click="mudarImagem">Mudar imagem</button>
        </div>
      </div>
    </div>
  </div>
  
</template>

<script>
import axios from 'axios';

export default {
  created: function() {
    axios.get(this.url).then(res=>{
      this.poke.type = res.data.types[0].type.name;
      this.poke.front = res.data.sprites.front_default;
      this.poke.back = res.data.sprites.back_default;
      this.currentImag = this.poke.front;
    })
  },
  data(){
    return {
      isFront: true,
      currentImag: '',
      poke: {
        type: '',
        front: '',
        back: ''
      }
    }
  },
  props: {
    num: Number,
    name: String,
    url: String
  },
  filters: {
    upper: function(value) {
      var newName = value[0].toUpperCase() + value.slice(1);
      return newName;
    }
  },
  methods: {
    mudarImagem: function() {
      if(this.isFront) {
        this.isFront = false;
        this.currentImag = this.poke.back;
      } else {
        this.isFront = true;
        this.currentImag = this.poke.front;
      }
    }
  }
}
</script>

<style>
  #poke{
    margin-top: 2%;
  }

</style>