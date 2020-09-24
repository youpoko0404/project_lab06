<template>
  <div>
    <b-container class="bv-example-row" align="center" justify="space-around"
      ><img src="../assets/img/pic.png" />
      <div class="search">
        <input
          type="text"
          class="searchTerm"
          v-model="textSearch"
          placeholder="Search"
        />
        <button type="submit" class="searchButton" @click="searchData()">
          <i>Search</i>
        </button>
      </div>
    </b-container>
    <vs-row class="mb-3" align="center" justify="space-around">
      <vs-card class="mt-3" type="2" v-for="list in playlist" :key="list.items">
        <template #img>
          <img :src="list.snippet.thumbnails.high.url" />
        </template>
        <template #title>
          <b-card-body :title="list.snippet.title"></b-card-body>
        </template>
        <template #text>
          <template>
            <div class="center">
              <vs-button
                block
                dark
                @click="active = 4"
                :href="'https://www.youtube.com/watch?v=' + list.id.videoId"
              >
                <i class="bx bxs-paint-roll"></i>Go to Youtube
              </vs-button>
            </div>
          </template>
        </template>
      </vs-card>
    </vs-row>
  </div>
</template>

<script>
import axios from "axios";
export default {
  data() {
    return {
      playlist: null,
      textSearch: "",
    };
  },

  methods: {
    searchData() {
      axios
        .get(
          "https://www.googleapis.com/youtube/v3/search?part=snippet&maxResults=50&q=" +
            this.textSearch +
            "&type=video&key=AIzaSyBpEC6Dg0LMO3oglU8RH_449KcsYMsOpCU"
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