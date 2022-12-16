<template>
  <div class="container">
    <PokemonSearch v-on:searchPokemon="searchPokemon"/>
    <PokemonList v-on:openDetail="ShowPokemonDetail" :imageURL="imageURL" :recherche="recherche"/>
    <PokemonDetail v-if="showPokemon" v-on:closeDetail="HidePokemonDetail" :pokemonUrl="pokemonUrl" :imageURL="imageURL" />
    
  </div>
</template>

<script>
import PokemonDetail from "../components/PokemonDetail.vue";
import PokemonList from "../components/PokemonList.vue";
import PokemonSearch from "../components/PokemonSearch.vue";
import config from "../config/config.json";

export default {
  data: ()=>{
    return{
      imageURL: config.IMG_URL, //url de l image
      pokemonUrl: "", //selection du pokemon
      showPokemon: false, //bool si le pokemon est affiché
      recherche: "", //chaine pour la barre de recherche
    }
  },
  components: {
    PokemonDetail,
    PokemonList,
    PokemonSearch,
  },
  methods: {

    //ouverture de la fenetre
    ShowPokemonDetail(pokemon){
      this.showPokemon = true;
      this.pokemonUrl = pokemon;
      // console.log(this.pokemonUrl);
    },

    //fermeture de la fenetre
    HidePokemonDetail(){
      this.showPokemon = false;
      this.pokemonUrl = "";
      // console.log("Hide pokemon");
    },

    //recherche
    searchPokemon(recherche){
      this.recherche = recherche;
    }
    
  }
};
</script>

<style lang="scss" scoped>
.container {
  display: flex;
  justify-content: center;
  align-items: center;
  flex-direction: column;
  padding: 10px;
  width: calc(100% - 20px);
  min-height: calc(100vh - 20px);
  //background: radial-gradient(#ffbf0b, #e20000);

  font-family: "Acme", arial;
  font-size: 1rem;
  font-weight: normal;
}

h1 {
  color: #efefef;
}
</style>