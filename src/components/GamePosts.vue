<template>
  <div class="game-post-wrapper">
  <div class="card" @click="openPost">
    <div class="post-image">
      <img :src="this.postImage" :alt="this.postName"/>
    </div>
    <div class="post-name">
      <h4>{{postName}}</h4>
    </div>
  </div>
  </div>
</template>

<script>
  export default {
    name: 'GamePosts',
    props: {
      postUserName: null,
      postName: null,
      postImage: null,
      postUrl: null
    },
    methods: {
      openPost(){
        window.open(this.postUrl)
      }
    }
  }
</script>

<style>
.game-post-wrapper {
  margin: 10px;
}
  .post-image img {
    height: 150px;
    width: 180px;
  }
  .post-name {
    height: 125px;
    width: 180px;
    font-size: 1rem;
    overflow-wrap: break-word;
    text-align: center;
    overflow-y: scroll;
  }
</style>