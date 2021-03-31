<template>
  <main class="home">
    <!-- <h1>Home</h1> -->
    <!-- <img alt="Vue logo" src="../assets/logo.png"> -->
    <!-- <HelloWorld msg="Welcome to your vue-graphql app"/> -->
    <HomeBanner/>
  </main>
</template>

<script>
// @ is an alias to /src
import HomeBanner from '@/components/HomeBanner.vue'
// import SongsList from '@/components/SongsList.vue'

export default {
  // name: 'HomeBanner',
  components: {
    HomeBanner
    // SongsList
  }
}
</script>
