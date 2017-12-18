<template lang="pug">
#app
  img(src='./assets/logo.png')
  h1 PlatziMusic
  select(v-model="selectedCountry")
    option(v-for="country in countries" v-bind:value="country.value") {{ country.name }}
  spinner(v-show="loading")  
  ul
    artist(v-for="artist in artists" v-bind:artist="artist" v-bind:key="artist.mbid")
  <!--li(v-for="artist in artists") {{ artist.name }}-->

  <!--h1 {{ msg }}
  h2 Essential Links
  ul
    li
      a(href='https://vuejs.org', target='_blank') Core Docs
    li
      a(href='https://forum.vuejs.org', target='_blank') Forum
    li
      a(href='https://chat.vuejs.org', target='_blank') Community Chat
    li
      a(href='https://twitter.com/vuejs', target='_blank') Twitter
  h2 Ecosystem
  ul
    li
      a(href='http://router.vuejs.org/', target='_blank') vue-router
    li
      a(href='http://vuex.vuejs.org/', target='_blank') vuex
    li
      a(href='http://vue-loader.vuejs.org/', target='_blank') vue-loader
    li
      a(href='https://github.com/vuejs/awesome-vue', target='_blank') awesome-vue-->
</template>

<script>
import Artist from './components/Artist.vue'
import Spinner from './components/Spinner.vue'
import getArtists from './api'

export default {
  name: 'app',
  data () {
    return {
      artists: [],
      countries:[
        {name:'Argentina', value:'argentina'},
        {name:'Colombia', value:'colombia'},
        {name:'España', value:'españa'},
      ],
      selectedCountry:'argentina',
      loading: true
    }
  },
  components:{
    Artist,
    Spinner
  },
  methods:{
    refresArtists(){
    const self = this
    this.artists = []
    this.loading = true
    getArtists(this.selectedCountry)
      .then(function (artists) {
        self.loading = false
        self.artists = artists
      })
    }
},
  mounted(){
    this.refresArtists()
},
  watch:{
    selectedCountry(){
      this.refresArtists()
    }
  }
}


/*export default {
  name: 'app',
  data () {
    return {
      msg: 'Welcome to Your Vue.js App'
    }
  }
}*/
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
