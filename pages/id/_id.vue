<template>
  <div>
    <v-row > <nuxt-link to="/"> Home</nuxt-link>/{{ Name }} </v-row>
    <v-row >
      <v-col cols="2">
        <img
            :src="this.$route.params.id.image_url" alt=""/>
      </v-col>
      <v-col cols="8">
        <v-list-item>Score : {{ score }}</v-list-item>
        <v-list-item>Chapter : {{ chapter }}</v-list-item>
        <v-list-item>Start Date : {{ start }}</v-list-item>
        <v-list-item>End Date : {{ end }}</v-list-item>
        <v-list-item>Volume : {{ volume }}</v-list-item>
        <v-list-item>Sysnopsis : {{ synopsis }}</v-list-item>
        
      </v-col>
    </v-row>

    
  </div>
</template>

<style></style>

<script>
import axios from 'axios'
export default {
  components: {},
  data() {
    return {
      tmp: null,
      Name: this.$route.params.id.title,
      score: this.$route.params.id.score,
      chapter: this.$route.params.id.chapters,
      start: this.$route.params.id.start_date,
      end: this.$route.params.id.end_date,
      volume: this.$route.params.id.volumes,
      synopsis: this.$route.params.id.synopsis,
      img: this.$route.params.id.image_url,
      
    }
  },
  methods: {
    handleSearchManga() {
      const url = `https://api.jikan.moe/v3/search/manga?q=${this.query}&page=1`
      axios.get(url).then((res) => {
        console.log(res.data)
        this.results = res.data.results
      })
    }
  }
}
</script>