<template>
    <div class="songs-wrapper">
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
            <!-- test search output -->
            <h1>Top <sup>{{ search }}</sup></h1>
            <!-- .... -->
            <div class="top-five" v-for="(five, index) in topfive | search" :key="index">

                <div class="thumb">
                     <img class="thumb-img" :src="five.albumart" alt="">
                </div>
            </div>


            <!-- <p>Message is: {{ search }}</p> -->
        </div><!--end.header-->
        <div   class="song" v-for="(song, index) in songs" :key="index">
            <img :src="song.albumart" @click="gotoSong(song)" />
            <div class="text">
                <h3>{{song.author}}</h3>
             <h4 >{{song.song}}</h4>
            </div>

            <!-- <a>{{song.json}}</a> -->

            <!-- <audio id="myAudio" controls>
                <source :src="song.audio" type="audio/mpeg">
                <source src="horse.oog" type="audio/oog">
            </audio> -->
        </div>
    </div>
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
        // skipAllQueries(){
        //     return this.lazyload === false
        // },
        songs: {
            query: GET_ALL_SONGS_QUERY
        }
    },
    data(){
        return {
            search: "",
            lazyload: true
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
            var x = document.getElementById("myAudio")
            var audio = document.getElementById("myAudio").duration;
            // document.getElementById("demo").innerHTML = x;
        //    let song = song.x
            console.log(x)
            console.log(song)
            console.log(audio)
        },
        lazyLoader(){
             if(this.songs.length >= 0){
                return this.lazyload = false
            }
        }
    },
    computed: {
      topfive(){
        // console.log(this.songs)
        let songs = this.songs
        let query = this.search
        let search = query.replace('-[A-Z]+', 'g');
        let song = songs.filter(song => song.song ==  search || song.author == search || song.id == search)
        // console.log(song.audio)
        // if (result.length) {
        //    result.length = search
        // }
        // else {
        //     result.length = 5
        // }
        return song;
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
    mounted() {
        // this.lazyLoader()

    },
}

</script>