<template>
  <v-app>
    <v-toolbar
      app
      :clipped-left="clipped"
    >
      <v-toolbar-title v-text="title"></v-toolbar-title>
    </v-toolbar>
    <v-content>
      <Search/>
    </v-content>
    <v-footer :fixed="fixed" app>
      <span>&copy;2018 sonora-mellow</span>
    </v-footer>
  </v-app>
</template>

<script>
import Search from './components/Search'

export default {
  name: 'App',
  components: {
    Search
  },
  data () {
    return {
      clipped: false,
      fixed: false,
      title: 'vue-imas-search'
    }
  }
}
</script>
