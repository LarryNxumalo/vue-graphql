<template>

        <div class="header">
             <h1>Sang songs</h1>
            <form>
                <input  type="text"
                        placeholder="Search for your songs 2"
                        v-model="search"
                        />
                <button @click.prevent='searchData'>
                    <img src="../assets/icons/header-s.svg" alt="">
                </button>
            </form>
            <h1>Top <sup>{{ search }}</sup></h1>
                <div class="top-five" v-for="(topfive, index) in topfive" :key="index">

                <div class="thumb">
                     <img class="thumb" :src="topfive.albumart" alt="">
                </div>
            </div>
            <!-- <p>Message is: {{ search }}</p> -->
        </div><!--end.header-->

</template>

<script>
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
    }
}`


//Apollo object that allows us to use the apollo object in our vue-comp
export default {
    name: 'SongsList',
    // props: ['query'],
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
    methods:{
         searchData(){
         let data = {
            query: this.search,
            song: this.search.toLowerCase().replace(/ /g, '_')
         };

         if(data.song == this.songs){
           //  this.$router.push(`${data.song}`
           console.log(data.song)
         } else {
           console.log(`'no matches found for'${data.song}`)
         }
        //  this.$router.push(`${data.song}`)

      },
        gotoSong(song){
            console.log(song)
        }
    },
    computed: {
      topfive(){
        // console.log(this.songs)
        let songs = this.songs
        let query = this.search
        let search = query.replace('-[a-z]+', 'g')
        let result = songs.filter(song => song.song ==  search || song.author == search || song.id == search)

        // if (result.length) {
        //    result.length = search
        // }
        // else {
        //     result.length = 5
        // }
        return result;
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
}

</script>