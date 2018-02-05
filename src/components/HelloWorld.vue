<template>
  <div class="hello">
    <h1>Platzi Music</h1>
    <select v-model="selectedCountry">
      <option v-for="country in countries" :key="country.id" :value="country.value">
        {{ country.name }}
      </option>
    </select>
    <spinner v-show="loading"></spinner>
    <ul v-show="!loading">
      <!--<li v-for="artist in artists">
        {{ artist.name }}
      </li>-->
      <artist v-for="artist in artists" :artist="artist" :key="artist.mbid"></artist>
    </ul>
  </div>
</template>

<script>


import Artist from './Artist.vue'
import Spinner from './Spinner.vue'
import getArtists from '../api'

export default {
  name: 'HelloWorld',
  data () {
    return {
      artists: [],
      countries: [{
        name: "Argentina",
        value: "argentina",
        id: "arg001"
      },
      {
        name: "Colombia",
        value: "colombia",
        id: "col001"
      },
      {
        name: "España",
        value: "spain",
        id: "esp001"
      }],
      selectedCountry: 'argentina',
      loading: false
    }
  },
  components:{
    Artist,
    Spinner// === Artist: Artist
  },
  mounted: function() {
    this.refreshArtists()
  },

  methods: {
    refreshArtists (){
      const self = this;
      this.loading = true
      getArtists(this.selectedCountry)
        .then(function(artists){
          self.loading = false
          self.artists = artists;
        })
    }
  },

  watch: {
    selectedCountry (){
      this.refreshArtists()
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="stylus">

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
