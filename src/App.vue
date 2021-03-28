<template>
  <div id="app">
    <div class="nav">
      <div class="exit-fullscreen" v-if="small" @click="closeFS">EXIT</div>
    <img  class="logo" alt="logo" src="./assets/logo.svg" @click="fullScreen">
      <router-link to="/">
        <img alt="logo" src="./assets/icons/home.svg">
        home
      </router-link>
      <router-link to="/search">
        <img alt="logo" src="./assets/icons/search.svg">
        search
      </router-link>
      <router-link to="/songs">
        <img alt="logo" src="./assets/icons/songs.svg">
        your songs
      </router-link>
      <router-link to="/podcasts">
        <img alt="logo" src="./assets/icons/podcasts.svg">
        podcasts
      </router-link>
    </div>
    <router-view/>
  </div>
</template>

<script>
export default {
  data(){
    return {
      small: false
    }
  },
  methods: {
    fullScreen(){
      //full screen code
      document.body.requestFullscreen();
      if(document.body.requestFullscreen.length == 0){
        this.small == true
      }
      // console.log(document.body.requestFullscreen.length)
    },
    closeFS(){
      //exit full screen code
      this.exit = false
       document.body.exitFullscreen();
    }
  },
  mounted() {
     this.fullScreen()
  },
}
</script>

 <style lang="scss">
  @import './assets/scss/style.scss';
</style>


