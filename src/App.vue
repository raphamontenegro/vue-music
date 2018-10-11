<template lang="pug">
  #app
    img(src='./assets/logo.png')
    h1 Vue Music
    select(v-model="selectedCountry")
      option(v-for="country in countries" v-bind:value="country.value") {{country.name}}
    spinner(v-show="loading")
    ul
      artist(v-for="artist in artists" v-bind:artist="artist" v-bind:key="artist.mbid")
</template>

<script>
import artist from './components/Artist'
import spinner from './components/Spinner'
import getArtists from "./api";
export default {
  name: 'app',
  data () {
    return {
      artists: [],
      countries: [
        {name: 'Brazil', value: 'brazil'},
        {name: 'Spain', value: 'spain'},
        {name: 'Argentina', value: 'argentina'},
        {name: 'Portugal', value: 'portugal'}
      ],
      selectedCountry: 'brazil',
      loading: true
    }
  },
  components: {
    artist: artist,
    spinner: spinner
  },
  methods: {
    refreshArtists() {
      const self = this
      this.loading = true;
      this.artists = []
      getArtists(this.selectedCountry)
        .then(function (artists) {
          self.loading = false;
          self.artists = artists;
        })
    }
  },
  mounted: function () {
   this.refreshArtists()
  },
  watch: {
    selectedCountry: function () {
      this.refreshArtists()
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
      color: blue;

  ul
      list-style-type none
      padding 0

  li
      display inline-block
      margin 0 10px

  a
      color #42b983
</style>
