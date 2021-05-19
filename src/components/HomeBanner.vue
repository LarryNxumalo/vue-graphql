<template>
    <div class="home-wrapper">
        <div class="splash">
             <vue-displacement-slideshow
             class="vue-dis"
            :images="images"

            :displacement="require('../assets/posters/displace.jpg')"
            :intensity="0.2"
            :speedIn="1.4"
            :speedOut="1.4"
            ease="expo.out"
            ref="slideshow"
            :isInteractive="true"></vue-displacement-slideshow>
            <!-- <img src="../assets/posters/riky-poster-nbg.png"> -->
            <div class="splash-text">
                <h2>Ungazncishi</h2>
                <h3>Riky Rick</h3>
                <h1>South&nbsp;Africa's Nomber <br>Uno</h1>
            </div>
        </div>
        <div class="bottom-splash">
              <!-- <Canvas/> -->
        </div>
        <!-- <Header/> -->
        <!-- <div class="song" v-for="(song, index) in songs" :key="index"> -->
            <!-- <img :src="song.albumart" @click="gotoSong(song)"/> -->
            <!-- <h3>{{song.author}}</h3> -->
            <!-- <h4>{{song.song}}</h4> -->
            <!-- <a>{{song.json}}</a> -->

            <!-- <audio controls>
                <source :src="song.audio" type="audio/mpeg">
                <source src="horse.oog" type="audio/oog">
            </audio> -->
        <!-- </div> -->
    </div>
</template>

<script>
// import Header from "../global/Header"
//GQL Needed to be able to send graphQL query strings properly parsed to graphql servers

// import Canvas from './Canvas.vue'
 import VueDisplacementSlideshow from "vue-displacement-slideshow";


//Apollo object that allows us to use the apollo object in our vue-comp
export default {
    name: 'SongsList',
    // props: ['query'],
    // apollo: {
    //     songs: {
    //         query: GET_ALL_SONGS_QUERY
    //     }
    // },
    components: {
        VueDisplacementSlideshow,
        // Canvas,
        // Header
    },
    data(){
        return {
            search: "",
        }
    },
    methods:{

      init() {
                //We loop through all our images by calling the 'next' method of our component every 2 seconds
                setInterval(() => {
                    if(this.$refs.slideshow){
                          this.$refs.slideshow.next();
                    }
                }, 2000);
            }
    },
    computed: {
      topfive(){
        // console.log(this.songs)
        let songs = this.songs
        let query = this.search
        let search = query.replace('-[a-z]+', 'g')
        let result = songs.filter(song => song.song ==  search || song.author == search || song.id == search)

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
      },
      images(){
          return [
              require("../assets/posters/1.png"),
              require("../assets/posters/2.jpeg"),
              require("../assets/posters/3.png"),
          ]
      }
    },
    mounted() {
        this.init();
    }
}

</script>