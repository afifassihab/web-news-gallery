<template>
  <div>
    <v-container>
      <v-layout justify-center row wrap>
        <v-flex xs12 sm10 md8>
          <img :src="content.urlToImage" width="100%">
          <span class="grey--text caption">{{ content.publishedAt }} - {{ content.author }} - {{ content.source.name }}</span>
          <h2 clss="my-1">{{ content.title }}</h2>
          <p>{{ content.content }}</p>
        </v-flex>
      </v-layout>
    </v-container>
  </div>
</template>

<script>
export default {
  computed: {
    content() {
      return this.$store.state.content
    }
  }
}
</script>
