<template lang="pug">
  li.artist
    h2
      a(v-bind:href="artist.url" target="blank") {{artist.name}}
    img(v-bind:src="artist.image[2]['#text']")
</template lang="pug">

<script>
export default {
  name: 'artist',
  props: ['artist']
}
</script>

<style lang="stylus" scoped>
li
  display block
  margin 0 auto
 
</style>
