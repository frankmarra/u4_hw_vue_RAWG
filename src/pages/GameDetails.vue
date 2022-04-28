<template>
  <div class="game-content" v-if="gameDetails">
    <section class="image-container">
      <div><img :src="gameDetails.background_image" :alt="gameDetails.name"/></div>
    </section>
    <section class="details">
      <div class="flex-row space"></div>
      <div class="game-title">
        <h3>{{gameDetails.name}}</h3>
      <button @click="goHome">Home</button>
      </div>
      <div class="recent-posts-wrapper">
        <p>Recent posts from games subreddit:</p>
        <div class="recent-posts">
          <GamePosts v-for="post in gamePosts" :key="post.id" :postUserName="post.username" :postName="post.name" :postImage="post.image" :postUrl="post.url" />
        </div>
      </div>
    </section>
  </div>
  <div class="game-content" v-else>
    <h3>Loading...</h3>
  </div>
</template>

<script>
  import axios from 'axios'
  const API_KEY = process.env.VUE_APP_RAWG_KEY 
  import GamePosts from '../components/GamePosts.vue'
  export default {
    name: 'GameDetails',
    components: {
      GamePosts
    },
    data: () => ({
      gameDetails: null,
      gamePosts: []
    }),
    mounted() {
      this.getGameDetails(this.$route.params.game_id)
      this.getGamePosts(this.$route.params.game_id)
    },
    methods: {
      async getGameDetails(gameId) {
        // Get game id from router here
        const res = await axios.get(`https://api.rawg.io/api/games/${gameId}?key=${API_KEY}`)
        this.gameDetails = res.data
      },
      async getGamePosts(gameId) {
        const res = await axios.get(`https://api.rawg.io/api/games/${gameId}/reddit?key=${API_KEY}`)
        this.gamePosts = res.data.results
      },
      goHome() {
        this.$router.push(`/`)
      }
    }
  }
</script>

<style>
  .game-title {
    display: flex;
    justify-content: space-around;
    align-items: center;
  }
  .game-title button {
    height: 30px;
  }
  .recent-posts {
    overflow-x: scroll;
    overscroll-behavior-x: contain;
    scroll-snap-type: x mandatory;
    scroll-snap-align: center;
    scroll-behavior: smooth;
    display: flex;
    justify-content: flex-start;
    padding: 20px 0;
  }
</style>