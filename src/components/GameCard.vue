<template>
  <div class="card game-card">
    <div class="image-wrapper">
      <!-- Image Goes Here -->
      <img :src="this.gameImage" :alt="this.gameName" />
    </div>
    <div class="info-wrapper flex-col">
      <!-- Game Name Goes Here -->
      <h4>{{ this.gameName }}</h4>
      <h4>Rating: {{ this.gameRating }}</h4>
    </div>
  </div>
</template>

<script>
  export default {
    name: 'GameCard',
    props: {
      gameName: null,
      gameImage: null,
      gameRating: null
    }
  }
</script>
