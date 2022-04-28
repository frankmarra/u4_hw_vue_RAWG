<template>
  <div class="card platform-card">
    <div class="image-wrapper">
      <!-- Image Goes Here -->
      <img :src="this.platformImage" :alt="this.platformName" />
    </div>
    <div class="info-wrapper flex-col">
      <!-- Game Name Goes Here -->
      <h4>{{ this.platformName }}</h4>
      
    </div>
  </div>
</template>

<script>
  export default {
    name: 'GameCard',
    props: {
      platformName: null,
      platformImage: null,
      
    }
  }
</script>