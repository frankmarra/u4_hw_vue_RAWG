<template>
  <div className="container-grid">
    <PlatformCard v-for="platform in platforms" :key="platform.id" :platformName="platform.name" :platformImage="platform.image_background" @click="selectPlatform(platform.id)"/>
  </div>
</template>

<script>
  import axios from 'axios'
  import PlatformCard from '../components/PlatformCard.vue'
  const API_KEY = process.env.VUE_APP_RAWG_KEY
  export default {
    name: 'ViewPlatforms',
    components: {
      PlatformCard
    },
    data: () => ({
      platforms: []
    }),
    mounted() {
      this.getPlatforms()
    },
    methods: {
      async getPlatforms(){
        const res = await axios.get(`https://api.rawg.io/api/platforms?key=${API_KEY}`)
        this.platforms = res.data.results
      },
      selectPlatform(platformId){
        this.$router.push(`/platforms/${platformId}`)
      }
    }
  }
  </script>