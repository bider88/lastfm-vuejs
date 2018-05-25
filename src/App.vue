<template lang="pug">
  #app
    .head
      img(src='dist/logo.png')
      h1 Last.fm VueJS
      select(v-model="selectedCountry")
        option(v-for="country in countries" v-bind:value="country.value") {{ country.name }}
      input(v-model="searchArtist" placeholder="Buscar artista...")
    .spinner
      ring-loader(:loading="loading" :color="color" :size="size")
    ul
      artist(v-for="artist in filterBy(artists, searchArtist, 'name')" v-bind:artist="artist" v-bind:key="artist.mbid")

</template>

<script>
import getArtists from './api'
import Artist from './components/Artist'
import RingLoader from 'vue-spinner/src/RingLoader.vue'

export default {
  name: 'app',
  data () {
    return {
      artists: [],
      countries: [
        {name: 'Mexico', value: 'mexico'},
        {name: 'España', value: 'spain'},
        {name: 'Alemania', value: 'germany'},
        {name: 'Francia', value: 'france'},
        {name: 'Brasil', value: 'brazil'},
        {name: 'Argentina', value: 'argentina'}
      ],
      selectedCountry: 'mexico',
      loading: true,
      color: '#42b983',
      size: '60px',
      searchArtist: ''
    }
  },
  components: {
    Artist,
    RingLoader
  },
  methods: {
    getAllArtists() {
      const self = this
      this.loading = true
      this.artists = []
      getArtists(this.selectedCountry)
        .then(function(artists) {
          self.artists = artists
          self.loading = false
        })
    }
  },
  mounted() {
    this.getAllArtists()
  },
  watch: {
    selectedCountry: function() {
      this.getAllArtists()
    }
  }
}
</script>

<style lang="stylus">
body
  margin 0

#app
  font-family 'Avenir', Helvetica, Arial, sans-serif
  -webkit-font-smoothing antialiased
  -moz-osx-font-smoothing grayscale
  text-align center
  color #2c3e50

.head
  background-color #5d6670
  padding 20px 0 40px 0

h1, h2
  font-weight normal
  color white

a
  color #42b983
.spinner
  margin 50px auto
  width 75px
select, input
  background-color white
  color #2c3e50
  font-size 1em
  padding 10px
  width 200px
  border  2px #42b983 solid
  border-radius 4px
input
  width 400px
  display inline-block
  margin-left 20px
  margin-top 20px
</style>
