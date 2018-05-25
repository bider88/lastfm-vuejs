<template lang="pug">
  #app
    img(src='./assets/logo.png')
    h1 Last.fm VueJS
    select(v-model="selectedCountry")
      option(v-for="country in countries" v-bind:value="country.value") {{ country.name }}
    ul
      artist(v-for="artist in artists" v-bind:artist="artist" v-bind:key="artist.mbid")
      //- li(v-for="artist in artists") {{ artist.name }}

</template>

<script>
import getArtists from './api'
import Artist from './components/Artist'
export default {
  name: 'app',
  data () {
    return {
      artists: [],
      countries: [
        {name: 'Mexico', value: 'mexico'},
        {name: 'España', value: 'spain'},
        {name: 'Alemania', value: 'germany'}
      ],
      selectedCountry: 'mexico'
    }
  },
  components: {
    Artist
  },
  methods: {
    getAllArtists() {
      const self = this
      getArtists(this.selectedCountry)
        .then(function(artists) {
          self.artists = artists
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
#app
  font-family 'Avenir', Helvetica, Arial, sans-serif
  -webkit-font-smoothing antialiased
  -moz-osx-font-smoothing grayscale
  text-align center
  color #2c3e50
  margin-top 60px

h1, h2
  font-weight normal

ul
  list-style-type none
  padding 0

li
  display inline-block
  margin 0 10px

a
  color #42b983
</style>
