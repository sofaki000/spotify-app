<template>
  <v-container>
    <v-row justify="center" align="center">
      <v-col cols="6" sm="6" md="6">
        <v-btn
          style="width:200px;"
          depressed
          color="primary"
          @click="getMostPopular"
        >
          Most Popular
        </v-btn>
        <!-- <the-button @click="getMostPopular">Most popular</the-button> -->
      </v-col>
      <!-- <v-col cols="6" sm="6" md="6"> <widget /></v-col> -->
    </v-row>

    <v-row justify="center" align="center">
      <v-col cols="12" sm="8" md="6">
        <v-btn
          style="width:200px;"
          depressed
          color="primary"
          @click="getRandomSearch"
        >
          Get a random search
        </v-btn>
        <v-btn style="width:200px;" depressed color="primary" @click="getLizzo">
          Get a lit lizzo song
        </v-btn>
      </v-col>
    </v-row>
    <v-row justify="center" align="center">
      <v-col cols="12" sm="8" md="6">
        <v-btn style="width:200px;" color="primary" @click="getArtist">
          Get an artist
        </v-btn>
        <v-sheet>{{ artist }}</v-sheet>
      </v-col>
    </v-row>
    <v-row justify="center" align="center">
      <v-col cols="12" sm="8" md="6">
        <authorization :token="token" />
      </v-col>
    </v-row>
  </v-container>
</template>

<script>
import TheButton from "@/components/TheButton.vue";
import Authorization from "../components/Authorization.vue";
import Widget from "../components/Widget.vue";
export default {
  components: { TheButton, Authorization },
  data() {
    return {
      info: "",
      artist: "",
      response: "",
      token:
        "Bearer BQAJRnZt6A10Oq273Kd3-ADMk3bYIsormf6DPM3jL4O6O80qUnwNQo0zSeURVf9_rOwqpMikyUUzH32GIakl9TMrsbyUj2hvzR6JRi-dUIrWAB27gMNRlvA40DaIWjVATzHYNMQJkOA"
    };
  },
  methods: {
    getLizzo() {
      window.axios = require("axios");
      var url = "https://api.spotify.com/v1/tracks/3HWzoMvoF3TQfYg4UPszDq";
      axios
        .get(url, {
          headers: {
            "Content-Type": "application/json",
            Authorization: this.token
          }
        })
        .then(response => {
          console.log(response);
          this.info = response.data.external_urls;
          window.open(this.info.spotify);
          // this.info = response.data.description;
        })
        .catch(err => {
          console.log("this is the error");
          console.log(err);
        });
    },
    getMostPopular() {
      window.axios = require("axios");
      var url = "https://api.spotify.com/v1/playlists/37i9dQZEVXbMDoHDwVN2tF";
      axios
        .get(url, {
          headers: {
            "Content-Type": "application/json",
            Authorization: this.token
          }
        })
        .then(response => {
          console.log(response);
          alert(response.description);
          this.info = response.data.description;
        })
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
        .then(response => {
          console.log(response);
          alert(response.description);
        })
        .catch(err => {
          console.log("this is the error");
          console.log(err);
        });
    },
    getRandomSearch() {
      const characters = "abcdefghijklmnopqrstuvwxyz";
      const randomCharacter = characters.charAt(
        Math.floor(Math.random() * characters.length)
      );
      let randomSearch = "";
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
            Authorization: this.token
          }
        })
        .then(response => {
          console.log(response);
          alert(response.description);
        })
        .catch(err => {
          console.log("this is the error");
          console.log(err);
        });
    }
  }
};
</script>
