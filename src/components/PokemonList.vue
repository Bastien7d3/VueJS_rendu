<template>
  <div class="list">
    <article v-for="pokemon in pokemonsFiltered" v-bind:key="pokemon.name" v-on:click="openDetail(pokemon.url)">
      <img :src="imageURL + pokemon.name +'.png'" alt="">
      <h3>{{pokemon.name}}</h3>
    </article>
  </div> 
</template>

<script>

import axios from '../../node_modules/axios'
import config from '../config/config.json'

export default {
  beforeMount(){

    axios.get(config.API_URL)
      .then((e)=>{
        this.list_pokemons = e.data.results;
      })
  } ,   
  props:['imageURL',"recherche"],
  data: function () {
    return {
      list_pokemons: []
    };
  },
  methods:{
    //emition pour louverture de la fenetre
    openDetail: function(pokemon){
      // console.log('open');
      this.$emit("openDetail",pokemon);
    }
  },
  computed: {
    //recherche
    pokemonsFiltered: function(){     
      if (this.recherche === ""){
        return this.list_pokemons
      }
      else{
        let filteredStories = this.list_pokemons.filter((pokemon) => {
        return pokemon.name.includes(this.recherche);
       })
       return filteredStories
      }

    }     
  }
}

</script>

<style lang="scss" scoped>
.list {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(150px, 1fr));
  grid-gap: 10px;
  width: 100%;
  max-width: 510px;
}
article {
  height: 150px;
  background-color: #efefef;
  text-align: center;
  text-transform: capitalize;
  border-radius: 5px;
  cursor: pointer;
  box-shadow: 0 15px 30px rgba(0, 0, 0, 0.2), 0 10px 10px rgba(0, 0, 0, 0.2);
}
h3 {
  margin: 0;
}
#scroll-trigger {
  display: flex;
  justify-content: center;
  align-items: center;
  width: 100%;
  height: 150px;
  font-size: 2rem;
  color: #efefef;
}

img {
  width: 96px;
  height: 96px;
}
</style>

