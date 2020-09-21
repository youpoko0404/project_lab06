<template>
<body>
  <b-container class="bv-example-row">
    <div class="search">
      <input type="text" class="searchTerm" v-model="textSearch" placeholder="Search" />
      <button type="submit" class="searchButton" :active="active == 0" @click="searchData()">
        <i>Search</i>
      </button>
    </div>
  </b-container>
  <vs-row class="mb-3" align="center" justify="space-around">
    <vs-card class="mt-3" type="2" v-for="list in playlist" :key="list.items">
      <template #title>
        <b-card-body :title="list.snippet.title"></b-card-body>
      </template>
      <template #img>
        <img :src="list.snippet.thumbnails.high.url" />
      </template>
      <template #text>
        <vs-button
          dark
          :active="active == 4"
          @click="active = 4"
          :href="'https://www.youtube.com/watch?v=' + list.id.videoId "
        >Go to Youtube</vs-button>
      </template>
    </vs-card>
  </vs-row>
</body>
</template>

<script>
import axios from "axios";
export default {
  data() {
    return {
      playlist: null,
      taxtsearch: "",
    };
  },

  methods: {
    searchData() {
      axios
        .get(
          "https://www.googleapis.com/youtube/v3/search?part=snippet&maxResults=50&q=" +
            this.textSearch +
            "&type=video&key=AIzaSyCHZ7r0QaHWGK2wCVypNlj7o3p_lrsDsQk"
        )

        .then((Response) => {
          this.playlist = Response.data.items; //.slice(0, 20);
        })
        .catch((err) => {
          console.log(err);
          this.err = true;
        });
    },
  },
};
</script>

<style>
body {
  background-color: #18191c;
}
</style>