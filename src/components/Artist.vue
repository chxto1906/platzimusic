<template>
  <li>
    <h2>
      <a :href="artist.url" target="_blank">
        {{ artist.name }}
      </a>
    </h2>
    <img :src="artist.image[2]['#text']">
  </li>
</template>

<script>

import getArtists from '../api'

export default {
  name: 'artist',
  props: [ 'artist' ]
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="stylus">
li
  display block
  margin 10px 0

</style>
