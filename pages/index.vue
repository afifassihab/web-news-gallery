<template>
  <div>
    <v-container grid-list-lg>
      <v-layout row wrap >
        <v-flex xs12 sm6 md4 v-for="item in posts" :key="item.title" d-flex>
          <v-card @click="sendContent(item)" style="cursor: pointer" 
            >
            <v-img :src="item.urlToImage" :aspect-ratio="2"></v-img>
            <v-card-title>
              <span class="grey--text caption">{{ item.author }} - {{ item.source.name }}</span>
              <h2 class="title py-2">{{ item.title }}</h2>
              <span class="grey--text caption">{{ item.publishedAt }}</span>
            </v-card-title>
          </v-card>
        </v-flex>
      </v-layout>
    </v-container>
    <div class="center">
      <v-btn color="primary" @click="loadMore">Load More</v-btn>
    </div>

  </div>
</template>

<script>
import axios from 'axios'

export default {
  data() {
    return {
      articles: [],
      posts: [],
      current: 9
    }
  },
  methods: {
    loadMore() {
      this.posts = []
      this.current += 9

      this.articles.map(item => {
        if (item.title !== null && this.posts.length < this.current) {
          this.posts.push(item)
        }
      })
    },
    sendContent(item) {
      this.$store.commit('setContent', item)

      this.$router.replace(item.title.replace(/ /gi, '-'))
    }
  },
  mounted() {
    axios.get('https://newsapi.org/v2/everything?q=programming&domains=techcrunch.com,techinasia.com&apiKey=372e67792b314d8299f3186f9da3f385')
          .then(({data}) => {
            this.articles = data.articles

            data.articles.map(item => {
              if (item.title !== null && this.posts.length < 9) {
                this.posts.push(item)
              }
            })
          })

    // console.log(this.posts)
  }
}
</script>

<style scoped>
  .center {
    text-align: center;
  } 
</style>
