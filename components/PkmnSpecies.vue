<template>
  <div class="pkmn-item--desc">
    <b>Description :</b>
    <div v-for="result in pkmnDesc" :key="result.value">
        <div v-if="result.language.name === 'en' && result.version.name === 'sword'">
            {{ result.flavor_text }}
        </div>
    </div>
  </div>
</template>

<script>
import axios from 'axios';

export default {
  name: 'PkmnSpecies',

  data () {
    return {
      pkmnDesc: null,
    }
  },

  props: {
      pkmnId: Number,
  },

  mounted () {
    axios.get('https://pokeapi.co/api/v2/pokemon-species/' + window.location.pathname.split("/").pop()).then(resp => {
        this.pkmnDesc = resp.data.flavor_text_entries;
        console.log(this.pkmnDesc);
    });
  }
}
</script>

<style>
.pkmn-item--desc{
    margin-top: 2.5rem;
}

.pkmn-item--desc b{
    margin-bottom: 1rem;
    display: block;
}

.pkmn-item--info{
  position: relative;
}

.pkmn-item--info-num{
  color: #616161;
  position: absolute;
  top: -10px;
  left: -5px;
}

.pkmn-item--info-name::first-letter{
 text-transform: uppercase;
}
</style>
