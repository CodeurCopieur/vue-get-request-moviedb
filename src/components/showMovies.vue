<template lang="pug">
  #show-movies
    h1 Liste des films populaires actuels sur TMDb
    input(type="text", v-model="searchValue", placeholder="Search Movies", id="inputSearch")
    ul.card-list
      li#movie-card.movie(v-for="movie in filteredMovies")
        .movie__data
          .movie__poster
            span.movie__poster--fill
              img(:src=`link+movie.poster_path`, alt="")
            span.movie__poster--featured
              img(:src=`link+movie.poster_path`, alt="")
          .movie_details
            h2.movie__title {{ movie.title }}
            p 
              strong Vote average : 
              | {{ movie.vote_average }}
            p 
              strong Popularity : 
              | {{ movie.popularity }}

</template>

<script>
 export default {
   data: () => {
     return {
       link: 'https://image.tmdb.org/t/p/w300_and_h450_bestv2',
       movies: [],
       searchValue: ''
     }
   },
   methods: {

   },
   mounted() {
     this.$http.get('https://api.themoviedb.org/3/movie/popular?api_key=cc4c125990f5777406886df6fdb3e266').then((data) => {
       this.movies = data.body.results;
       console.log(this.movies);
     })
   },
   computed: {
     filteredMovies: function() {
       return this.movies.filter((movie) => {
         return movie.title.toLowerCase().includes(this.searchValue.toLowerCase());
       })
     }
   }
  }
</script>

<style lang="scss" scoped>
  @import url('../assets/scss/index.scss');
  @import url('https://fonts.googleapis.com/css?family=Lato:400,900');
  #show-movies {
    max-width: 1200px;
    margin: 0 auto;
    padding: 0px 20px;

    h1 {
      color: #2B2D42;
      font-weight: 700;
      margin:30px 0px;
      text-transform: uppercase;
    }

    #inputSearch {

    }

    .card-list {
      display: flex;
      flex-wrap: wrap;
      flex-direction: row;
      .movie {
        overflow: hidden;
        cursor: pointer;
        width: 100%;
        margin-bottom: 20px;

        &:hover {
          box-shadow: 0 0 0 1px rgba(0, 0, 0, 0.15), 0 2px 3px rgba(0, 0, 0, 0.2);
          .movie__data {
            .movie__poster {

              .movie__poster--featured{
                img {
                  transform: translate(2.5rem, 0.5rem);
                }
              }
            }
          }
        }

        @media screen and (min-width: 640px) {
          width: 24%;
          
          transition: all 480ms
        }

        .movie__data {


          .movie__poster {
            position: relative;

              .movie__poster--fill {
                position: absolute;
                overflow: hidden;
                width: 150%;
                height: 150%;
                top: -80%;
                bottom: -20%;
                left: -20%;
                transform: rotate(5deg);

                img {
                  filter: blur(6px);
                  object-fit: cover;
                  width: 100%;
                  height: 100%;
                  transform: scale(1.4);
                }

              }
 
              .movie__poster--featured {
                position: relative;
                display: block;
                align-self: center;
                margin-top: 84px;
                margin-left: 24px;
                width: 140px;
                border-radius: 2px;
                z-index: 1;

                img {
                  filter: drop-shadow(5px 10px 15px rgba(8, 9, 13, 0.4));
                  transition: all .5s;
                }

            }
          }

          .movie_details {
            color: #272D40;
            text-align: left;
            padding: 24px;
            .movie__title {
              font-family: "Lato", sans-serif;
              font-size: 1.25em;
              font-weight: 600;
              margin-bottom: 12px;
            }
            .movie__plot {
              font-size: 0.9em;
              line-height: 1;
              margin-bottom: 12px;
              
            }
          }
        }
      }
    }

    
  }
</style>