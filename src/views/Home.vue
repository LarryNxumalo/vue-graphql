<template>
  <main class="home">
    <h1>Home</h1>
    <!-- <img alt="Vue logo" src="../assets/logo.png"> -->
    <!-- <HelloWorld msg="Welcome to your vue-graphql app"/> -->
    <SongsList/>
  </main>
</template>

<script>
// @ is an alias to /src
// import HelloWorld from '@/components/HelloWorld.vue'
import SongsList from '@/components/SongsList.vue'

export default {
  name: 'Home',
  components: {
    // HelloWorld
    SongsList
  }
}
</script>
