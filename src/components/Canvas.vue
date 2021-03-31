<template>
   <div class="canvas">
       <span id="duration"></span>
   </div>
</template>

<script>

// import P5 from 'p5'
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
    name: 'Canvas',
    // props: ['query'],
    apollo: {
        songs: {
            query: GET_ALL_SONGS_QUERY
        }
    },
    // mounted(){
    //     getDuration(src,cb){
    //         var audio = new.
    //     }
    // }

}

</script>