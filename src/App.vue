<template lang="pug">
  #app
    img(src='./assets/logo.png')
    h1 PlatziMusic
    select(v-model='selectedCountry')
      option(v-for="country in countries" v-bind:value="country.value") {{ country.name }}
    spinner(v-show="loading")
    ul(v-show="!loading")
      artist(v-for='artist in artists' :key='artist.mbid' :artist="artist")

</template>

<script>
import getArtists from './api';
import artist from './components/artist';
import spinner from './components/spinner'

export default {
  name: 'app',
  data () {
    return {
      artists:[],
      countries:[
        {name:'Argentina', value: 'argentina'},
        {name:'Colombia', value: 'colombia'},
        {name:'Espania', value: 'spain'},
        {name:'Brasil', value: 'brazil'}
        ],
        selectedCountry:'argentina',
        loading:true   
      }
  },
  components:{
    artist: artist,
    spinner: spinner,
  },
  methods:{
    refreshArtists(){
      const self = this;
      this.loading = true
      getArtists(this.selectedCountry)
      .then(function(artists){
        self.artists=artists;
        self.loading = false
    })
    }
  },
  mounted(){
    this.refreshArtists()
  },
  watch: {
    selectedCountry(){
      this.refreshArtists()
  }
}
}
</script>

<style lang="stylus" >
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
	display block
	margin 0 10px
a
	color #42b983

</style>