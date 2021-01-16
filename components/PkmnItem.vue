<template>
  <div class="pkmn-item--info">
    <span class="pkmn-item--info-num">#{{ pkmnId }}</span>
    <img v-bind:src="pkmnImg" alt="image">
  </div>
</template>

<script>
import axios from 'axios';

export default {
  name: 'PkmnItem',

  data () {
    return {
      pkmnId: null,
      pkmnImg: null,
    }
  },

  props: {
      pkmnId: Number,
  },

  mounted () {
    axios.get('https://pokeapi.co/api/v2/pokemon/' + this.pkmnId).then(resp => {
      this.pkmnId = resp.data.id;
      this.pkmnImg = resp.data.sprites.front_default;
    });
  }
}
</script>

<style>

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
