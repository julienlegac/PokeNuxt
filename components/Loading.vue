<template>
  <div class="loading" id="loading" v-if="loading">
      TESSSST
      <div class="loading__content">
          <div class="loading__content--info">
              <img src="~/assets/pokeball.gif"/>
          </div>
      </div>
  </div>
</template>

<script>
export default {
  data: () => ({
    loading: false
  }),
  methods: {
    start () {
      this.loading = true
    },
    finish () {
      this.loading = false
    }
  }
}
</script>

<style>
  .loading{
    background: #1d1d1d;
    display: block;
    position: fixed;
    height: 100vh;
    width: 100vw;
  }

  .loading__content--info img{
      position: absolute;
      top: 50%;
      left: 50%;
      transform: translate(-50%, -50%);
  }
</style>

