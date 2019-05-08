<template>
  <v-app>
    <v-toolbar color="white" app flat class="elevation-1">
      <template v-if="$store.state.content.title">
        <v-btn color="primary" fab flat @click="goBack">
          <v-icon>arrow_back</v-icon>
        </v-btn>
      </template>
      <template v-else>
        <v-toolbar-title 
          class="primary--text pr-3 heading"
          @click="$router.push('/')"
          style="cursor: pointer">
          Navbar
        </v-toolbar-title>
        <v-toolbar-items>
          <v-btn flat>Home</v-btn>
          <v-btn flat>Blogs</v-btn>
          <v-btn flat>About</v-btn>
        </v-toolbar-items>
      </template>
    </v-toolbar>
    <v-content>
      <v-container>
        <nuxt />
      </v-container>
    </v-content>
    <v-footer app clas="white">
      <span>&copy; 2019</span>
    </v-footer>
  </v-app>
</template>

<script>
export default {
  methods: {
    goBack() {
      this.$store.commit('setContent', {})

      this.$router.replace('/')
    }
  }
}
</script>
