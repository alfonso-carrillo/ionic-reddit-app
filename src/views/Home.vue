<template>
  <div>
    <ion-card v-for="post in posts" :key="post.data.id" style="border: 1px solid blue;">
      <ion-card-content>
        <img v-if="post.data.thumbnail.startsWith('https://')" :src="post.data.thumbnail" :alt="post.data.title">
        <ion-label color="light">{{post.data.title}}</ion-label>
        <ion-button color="tertiary" expand="full" @click="viewMore(post.data)">
          View More
        </ion-button>
      </ion-card-content>
    </ion-card> 
  </div>
</template>

<script>
  import axios from 'axios';

  export default {
    data() {
      return {
        posts: []
      }
    },
    mounted() {
      this.loadData();
    },
    methods: {
      async loadData() {
        const response = await axios.get('https://www.reddit.com/r/marvelstudios.json');
        this.posts = response.data.data.children;
      },
      viewMore(post) {
        this.$router.push({name: 'detail', params: { post }})
      }
    }  
  }
</script>