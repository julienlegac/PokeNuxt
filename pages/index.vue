<template>
  <div class="pokenuxt">
    <Loading/>

    <h1>PokéNuxt</h1>
    <PkmnList/>
  </div>
</template>

<script>
import PkmnList from "~/components/PkmnList";
import Loading from "~/components/Loading";

export default {
  components: {PkmnList, Loading}
}
</script>

<style>
  .pokenuxt{
    background: #1d1d1d;
    padding: 1rem;
    min-height: 100vh;
  }

  .pokenuxt > h1 {
    color: #ffffff;
  }
</style>
