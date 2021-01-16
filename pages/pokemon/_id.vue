<template>
  <div class="pkmn-page">
    <div class="pkmn-page--info pkmn-page--info-title">#{{ pkmnId }} - <p class="pkmn-page--info-name">{{ pkmnName }}</p></div>
   
    <div class="pkmn-page--forms">
      <div class="pkmn-page--info-form">
        <b>Form :</b>
        <img v-bind:src="pkmnImgMale" alt="image">
        <img v-bind:src="pkmnImgMaleBack" alt="image">
      </div>

      <div class="pkmn-page--info-form">
        <b>Shiny Form :</b>
        <img v-bind:src="pkmnImgShinyMale" alt="image">
        <img v-bind:src="pkmnImgShinyMaleBack" alt="image">
      </div>
    </div>

    <div class="pkmn-page--forms">
      <div class="pkmn-page--info-form" v-if="pkmnImgFemale">
        <b>Female Form :</b>
        <img v-bind:src="pkmnImgFemale" alt="image">
        <img v-bind:src="pkmnImgFemaleBack" alt="image">
      </div>

      <div class="pkmn-page--info-form" v-if="pkmnImgFemale">
        <b>Shiny Female Form :</b>
        <img v-bind:src="pkmnImgShinyFemale" alt="image">
        <img v-bind:src="pkmnImgShinyFemaleBack" alt="image">
      </div>
    </div>
    
    <PkmnSpecies/>

    <div class="pkmn-page--info"><b>Height :</b> {{ pkmnHeight }}</div>
    <div class="pkmn-page--info">
        <b>Types : </b>
        <div v-for="result in pkmnTypes" :key="result.value" class="type-container">
            <span :class="'type-element type--' + result.type.name">{{ result.type.name }}</span>
        </div>
    </div>
    <div class="pkmn-page--info"><b>Weight :</b> {{ pkmnWeight }}</div>
  </div>
</template>

<script>
import axios from 'axios';
import PkmnSpecies from "~/components/PkmnSpecies";

export default {
  name: 'PkmnItem',

  components: {PkmnSpecies},

  data () {
    return {
        pkmnId: null,
        pkmnName: null,
        pkmnImgMale: null,
        pkmnImgMaleBack: null,
        pkmnImgFemale: null,
        pkmnImgFemaleBack: null,
        pkmnImgShinyMale: null,
        pkmnImgShinyMaleBack: null,
        pkmnImgShinyFemale: null,
        pkmnImgShinyFemaleBack: null,
        pkmnHeight: null,
        pkmnWeight: null,
        pkmnTypes: null,
    }
  },

  mounted () {
    axios.get('https://pokeapi.co/api/v2/pokemon/' + window.location.pathname.split("/").pop()).then(resp => {
      this.pkmnName = resp.data.name;
      this.pkmnId = resp.data.id;
      this.pkmnImgMale = resp.data.sprites.front_default;
      this.pkmnImgMaleBack = resp.data.sprites.back_default;
      this.pkmnImgFemale = resp.data.sprites.front_female;
      this.pkmnImgFemaleBack = resp.data.sprites.back_female;
      this.pkmnImgShinyMale = resp.data.sprites.front_shiny;
      this.pkmnImgShinyMaleBack = resp.data.sprites.back_shiny;
      this.pkmnImgShinyFemale = resp.data.sprites.front_shiny_female;
      this.pkmnImgShinyFemaleBack = resp.data.sprites.back_shiny_female;
      this.pkmnHeight = resp.data.height;
      this.pkmnWeight = resp.data.weight;
      this.pkmnTypes = resp.data.types;
    });
  }
}
</script>

<style>
.pkmn-page{
    background: #1d1d1d;
    padding: 1rem;
    min-height: 100vh;
    color: #ffffff;
}
.pkmn-page .pkmn-page--info{
    display: block;
}
.pkmn-page--info-form {
  border: 1px solid #616161;
  border-radius: 6px;
  margin-top: 1rem;
  margin-right: 1rem;
  padding: 1rem;
}
.pkmn-page--info b{
  display: inline-block;
  margin-top: 1rem;
}
.pkmn-page--forms{
  display: flex;
}
.pkmn-page--info-name{
    display: inline-block;
}
.pkmn-page--info-name::first-letter{
    text-transform: uppercase;
}
.pkmn-page--info-title{
    font-size: 2rem;
    font-weight: 700;
}
.type-container{
  display: inline-block;
}
.type-element{
  display: inline-block;
  background: #000000;
  color: #ffffff;
  padding: 5px 10px;
  border-radius: 6px;
  margin-right: 1rem;
}
.type-element::first-letter{
  text-transform: uppercase;
}
.type--normal{
  background: #cbccce;
}
.type--fire{
  background: #ff0001;
}
.type--water{
  background: #4a85e8;
}
.type--electric{
  background: #fdfc14;
  color: #1d1d1d;
}
.type--grass{
  background: #6ba753;
}
.type--ice{
  background: #00ffff;
  color: #1d1d1d;
}
.type--fighting{
  background: #cc4125;
}
.type--poison{
  background: #694da7;
}
.type--ground{
  background: #ffd762;
  color: #1d1d1d;
}
.type--flying{
  background: #4887e8;
}
.type--psychic{
  background: #c66ac7;
}
.type--bug{
  background: #94c37f;
}
.type--rock{
  background: #be9100;
}
.type--ghost{
  background: #20124e;
}
.type--dragon{
  background: #8f7bba;
}
.type--dark{
  background: #523e00;
}
.type--steel{
  background: #999999;
}
.type--fairy{
  background: #ffafff;
}
.type--light{
  background: #ffffff;
  color: #000000;
}
.type--data{
  background: #2a2a2a;
}
.type--gold{
  background: #feff6e;
  color: #1d1d1d;
}
</style>
