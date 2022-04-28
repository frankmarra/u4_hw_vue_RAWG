<template>
  <div class ="dropdown-wrapper">
    Sort by Rating:
    <select class="dropdown-menu" v-model="selected" @change="sortGenreGames($event)">
      <option disabled value="">Please Select</option>
      <option value="descending">Highest to Lowest</option>
      <option value="ascending">Lowest to Highest</option>
    </select>
  </div>
  <div className="container-grid">
    <GameCard v-for="game in games" :key="game.id" :gameName="game.name" :gameImage="game.background_image" :gameRating="game.rating" @click="selectGame(game.id)"/>
  </div>
</template>

<script>
  import axios from 'axios'
  import GameCard from '../components/GameCard.vue'
  const API_KEY = process.env.VUE_APP_RAWG_KEY
  export default {
    name: 'ViewGames',
    components: {
      GameCard
    },
    data: () => ({
      games: [],
      selected: ''
    }),
    mounted() {
      this.getGamesByGenre(this.$route.params.genre_id)
    },
    methods: {
      async getGamesByGenre(genreId) {
        // Get Genre Id here
        const res = await axios.get(`https://api.rawg.io/api/games?genres=${genreId}&key=${API_KEY}`)
        this.games = res.data.results
      },
      selectGame(gameId) {
        this.$router.push(`/details/${gameId}`)
      },
      sortGenreGames(event){
        event.preventDefault()
        if(event.target.value === 'ascending'){
          this.games.sort((a, b)=>{
            return a.rating - b.rating
          })
        } else if(event.target.value === 'descending'){
            this.games.sort((a, b) => {
              return b.rating - a.rating
            })
        }
      }
    }
  }
</script>

<style scoped>
  .dropdown-wrapper {
    text-align: center;
  }
</style>