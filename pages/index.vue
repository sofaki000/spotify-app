<template>
  <v-container>
    <v-row justify="center" align="center">
      <v-col cols="12" sm="8" md="6">
        <v-btn depressed color="primary" @click="getMostPopular">
          Most Popular
        </v-btn>
      </v-col>
      <v-col cols="12" sm="8" md="6">
        <v-btn depressed color="primary" @click="getRandomSearch">
          Get a random search
        </v-btn>
        <v-sheet>{{ info }}</v-sheet>
      </v-col>
      <v-btn color="primary" @click="getArtist">
        Get an artist
      </v-btn>
      <v-sheet>{{ artist }}</v-sheet>
    </v-row>
  </v-container>
</template>

<script>
export default {
  data() {
    return {
      info: "",
      artist: "",
      response: "",
      token:
        "Bearer BQD9lVAK2MvxTncfA8bme3ZF9lEzjeWE6siOTJvfR6-OH0Ve0HGyzdG3JSQvRQtrQoGAPj0HXL41tk-V_XbADWNC71s7DvWwpXVpbhAg-c1IoQNS5jm1z4T0LJa6tISP6DJcjOF2B0A"
    };
  },
  methods: {
    getMostPopular() {
      window.axios = require("axios");
      axios
        .get(
          "https://api.spotify.com/v1/me/top/artists?time_range=medium_term&limit=10&offset=5",
          {
            headers: {
              "Content-Type": "application/json",
              Accept: "*"
            },
            Authorization: this.token
          }
        )
        .catch(err => {
          console.log("this is the error");
          console.log(err);
        });
    },
    getRandomSearch() {
      window.axios = require("axios");
      var q = this.getRandomSearch();
      var url =
        "https://api.spotify.com/v1/search?q=" +
        q +
        "&type=track%2Cartist&market=US&limit=10&offset=5";
      axios
        .get(url, {
          headers: {
            "Content-Type": "application/json",
            Accept: "*"
          },
          Authorization: this.token
        })
        .then(response => (this.info = response.items))
        .catch(err => {
          console.log("this is the error");
          console.log(err);
        });
    },
    getRandomSearch() {
      // A list of all characters that can be chosen.
      const characters = "abcdefghijklmnopqrstuvwxyz";

      // Gets a random character from the characters string.
      const randomCharacter = characters.charAt(
        Math.floor(Math.random() * characters.length)
      );
      let randomSearch = "";

      // Places the wildcard character at the beginning, or both beginning and end, randomly.
      switch (Math.round(Math.random())) {
        case 0:
          randomSearch = randomCharacter + "%";
          break;
        case 1:
          randomSearch = "%" + randomCharacter + "%";
          break;
      }

      return randomSearch;
    },
    getArtist() {
      window.axios = require("axios");
      var url = "https://api.spotify.com/v1/artists/0TnOYISbd1XYRBk9myaseg";
      axios
        .get(url, {
          headers: {
            "Content-Type": "application/json",
            Accept: "*"
          },
          Authorization: this.token
        })
        .then(response => (this.artist = response.items))
        .catch(err => {
          console.log("this is the error");
          console.log(err);
        });
    }
  }
};
</script>
