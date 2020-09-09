<template lang="pug">
  #show-blogs
    h1 All Blog Movie

    .single-blog(v-for="movie in movies") 
      span adult: {{ movie.adult }}
      img(:src=`link+movie.poster_path`, alt="")
      p overview : {{ movie.overview }}
      p original title : {{ movie.original_title }}
      p vote average : {{ movie.vote_average }}
      p popularity : {{ movie.popularity }}

</template>

<script>
 export default {
   data: () => {
     return {
       link: 'https://image.tmdb.org/t/p/w300_and_h450_bestv2',
       movies: []
     }
   },
   methods: {

   },
   created() {
     this.$http.get('https://api.themoviedb.org/3/movie/popular?api_key=cc4c125990f5777406886df6fdb3e266').then((data) => {
       this.movies = data.body.results;
       console.log(this.movies);
     })
   }
  }
</script>

<style lang="scss" scoped>
  
</style>