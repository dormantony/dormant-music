<template lang="pug">
#app
  img(src='https://dormantony.github.io/dormant-music/dist/logo.png')
  h1 Essential Links2  
  select(v-model="selectedCountry")
    option(v-for="country in countries" v-bind:value='country.value') {{country.name}}
  spinner(v-show="loading")
  ul
    artist(v-for="artist in artists" v-bind:artist="artist" v-bind:key="artist.mbid") 
    


</template>

<script>
//li(v-for="artist in artists") {{ artist.name }}
import spinner from './components/spinner.vue'
import artist from './components/artist.vue'
import  getArtist from './api'

export default {
  name: 'app',
  data () {
    return {
     artists:[],
     countries:[
       {name:'argentina',value:'argentina'},
       {name:'colombia',value:'colombia'},
       {name:'mexico',value:'mexico'},
       {name:'spain',value:'spain'}
       ],
       selectedCountry:['mexico'],
       loading:true
    }
  },
  components:{
    artist,spinner
  }
  ,methods:{
    refreshArtist(){
      const self=this
      this.loading=true
    getArtist(this.selectedCountry)
      .then(function(artists){
        self.loading=false
        self.artists=artists
      }) 
    }

  },
  mounted(){
    this.refreshArtist()
  },
  watch:{
    selectedCountry(){
      this.refreshArtist()

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
