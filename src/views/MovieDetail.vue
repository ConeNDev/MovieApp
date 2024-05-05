<template>
    <div class="movie-detail">
        <h2>{{movie.Title}}</h2>
        <p>{{ movie.Year }}</p>
        <img :src="movie.Poster" alt="Movie Poster" class="featured-img">
        <p>{{ movie.Plot }}</p>
    </div>
</template>

<script>
import {useRoute} from 'vue-router';
import env from '@/env.js';
export default{
    data(){
        return{
            movie:[],
            route:useRoute()
        }
    },
    beforeMount(){
        fetch(`http://www.omdbapi.com/?apikey=${env.apikey}&i=${this.route.params.id}&plot=full`)
        .then(response=>response.json())
        .then(data=>{
            this.movie=data;
        })
    }
}
</script>

<style lang="scss">
.movie-detail {
  padding: 16px;

  h2 {
    color: #FFF;
    font-size: 28px;
    font-weight: 600;
    margin-bottom: 16px;
  }

  .featured-img {
    display: block;
    max-width: 200px;
    margin-bottom: 16px;
  }

  p {
    color: #FFF;
    font-size: 18px;
    line-height: 1.4;
  }
}
</style>