<template>
  <div class="pkmn-list">
    
    <div v-for="(result, index) in pkmnName" :key="result.value" class="pkmn-list--item">
        <nuxt-link :to="{path: '/pokemon/' + (index+1)}" rel="canonical">
            <PkmnItem v-bind:pkmnId="index+1"/>
        </nuxt-link>
    </div>
    
  </div>
</template>

<script>
import axios from 'axios';
import PkmnItem from "~/components/PkmnItem";

export default {
  components: {PkmnItem},

  data () {
    return {
      pkmnName: null,
      pkmnInfo: null,
      index: null,
    }
  },


  mounted () {
    axios.get('https://pokeapi.co/api/v2/pokemon?limit=898&offset=0/').then(resp => {
      this.pkmnName = resp.data.results;
      console.log(this.pkmnName);
    });
  }
}
</script>

<style>
  .pkmn-list{
    background: #1d1d1d;
    min-height: 100vh;
  }

  .pkmn-list--item{
    display: inline-block;
  }

  .pkmn-list--item a{
    text-decoration: none;
    margin: 1rem;
    border: 1px solid #616161;
    padding: 1rem;
    border-radius: 6px;
    display: block;
    transition: 0.25s;
  }

  .pkmn-list--item a:hover{
      background: rgb(39, 39, 39);
  }
</style>
