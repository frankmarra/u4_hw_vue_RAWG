<template>
  <div class="platform-content" v-if="platformDetails">
    <section class="image-container">
      <div><img :src="platformDetails.image_background" :alt="platformDetails.name"/></div>
    </section>
    <section class="details">
      <div class="flex-row space"></div>
      <div class="platform-title">
        <h3>{{platformDetails.name}}</h3>
        <h4 v-html="platformDetails.description"></h4>
      </div>
    </section>
  </div>
  <div class="platform-content" v-else>
    <h3>Loading...</h3>
  </div>
</template>

<script>
  import axios from 'axios'
  const API_KEY = process.env.VUE_APP_RAWG_KEY
  export default {
    name: 'PlatformDetails',
    data: () => ({
      platformDetails: null
    }),
    mounted() {
      this.getPlatformDetails(this.$route.params.platform_id)
    },
    methods: {
      async getPlatformDetails(platformId) {
        const res = await axios.get(`https://api.rawg.io/api/platforms/${platformId}?key=${API_KEY}`)
        this.platformDetails = res.data
      }
    }
  }
</script>
