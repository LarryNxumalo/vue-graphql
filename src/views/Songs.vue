<template>
  <main class="songs">
    <div class="header isclear">
       <h1 class="ismoving"><strong>Ungazncishi</strong> nice time finally @number#3</h1>
    </div>
    <SongsList />
  </main>
</template>

<script>

import SongsList from '@/components/SongsList.vue'
//###Songs View### -
//GQL Needed to be able to send graphQL query strings properly parsed to graphql servers
import gql from "graphql-tag"

const GET_ALL_SONGS_QUERY = gql`
    query getSongs{
    songs {
        id
        albumart
        author
        audio
        song
        json
        points
    }
}`

export default {
    name: 'Songs',
    components: {
        SongsList
    },
    apollo: {
        songs: {
            query: GET_ALL_SONGS_QUERY
        }
    },
    data(){
      return {
        search: "",
      }
    },
    methods: {
       searchData(){
         let data = {
            query: this.search,
            song: this.search.toLowerCase().replace(/ /g, '_')
         };
         if(data.song == this.data[0].song){
           //  this.$router.push(`${data.song}`
           console.log(data.song)
         } else {
           console.log(`'no matches found for'${data.song}`)
         }
        //  this.$router.push(`${data.song}`)

      }
    },
    computed: {
      topfive(){
        // console.log(this.songs)
        let songs = this.songs
        let result = songs.filter(song => song.id < 6)
        // if (result.length) {
        //   result.length = 5
        // }
        return result
        // songs.length = 5
        // songs.splice(1,0,{
        //     audio:"https://larrynxumalo.github.io/kasioke/music/PhantomSteeze-Stimela.mp3",
        //     author:"Phantom Steeze ft Costa Titch",
        //     id:"1",
        //     json:"https://larrynxumalo.github.io/kasioke/lyrics/PhantomSteeze-Stimela.json",
        //     song:"stimela",
        //   })
        // console.log(this.songs)
      }
    },
    // mounted(){
    //    this.topfive()
    // }

}
</script>