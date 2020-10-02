<template lang="html">
  <div>
    <div class="mt-2 mb-5"> <h2>Name of Manga ( eg .Naruto , Onepiece)</h2></div>
    <v-row>
      <v-col cols="10">
        <v-text-field v-model="query" solo label="Search"> </v-text-field>
      </v-col>
      <v-col cols="2">
        <v-btn large @click="handleSearchManga"><v-icon>mdi-magnify</v-icon>search</v-btn>
      </v-col>
    </v-row>
    
    <v-divider class="mt-2 mb-2"></v-divider>
    <div class="d-flex flex-wrap">
      <v-card v-for="manga in results" :key="manga.mal_id" class="ma-2" max-width="344" outlined @click="handleMangaClick()">
        <nuxt-link :to="{ name: 'id-id', params: { id:manga } }">
          <v-list-item single-line>   
            <v-list-item-title class="headline mt-1">
              {{ manga.title }}
            </v-list-item-title>
           <img :src="manga.image_url" alt="":style="{ width: '80px', marginTop: '10px', marginBottom: '10px'}"/>
          </v-list-item>
        </nuxt-link>
      </v-card>
    </div>
  </div>
</template>

<script>
import axios from 'axios'
export default {
  data() {
    return {
      query: '',
      results: []
    }
  },
  methods: {
    handleSearchManga() {
      const url = `https://api.jikan.moe/v3/search/manga?q=${this.query}&page=1`
      axios.get(url).then((res) => {
        console.log(res.data)
        this.results = res.data.results
      })
    },
    handleMangaClick(manga) {
      console.log('MANGA', manga)
    }
  }
}
</script>

<style lang="css" scoped></style>