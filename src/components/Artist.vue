<template lang="pug">
  .list-artist
    img(:src="artist.image[3]['#text']")
    h2: a(:href="artist.url" target="_blank") {{ artist.name }}
    p.listeners {{ artist.listeners }} {{ artist.listeners | pluralize('oyente') }}

</template>

<script>
export default {
  name:'artist',
  props: ['artist']
}
</script>

<style lang="stylus" scoped>
  .list-artist
    border  2px #42b983 solid
    border-radius 4px
    display inline-block
    margin 20px
    padding 10px
  .list-artist img 
    border-radius 5px
  .listeners
    font-size .8em
    margin 0 0 20px 0 
</style>
