<template>
  <v-btn @click="login">Spotify Login</a></v-btn>
</template>

<script>
import qs from "qs";
export default {
  props: ["token"],
  methods: {
    login() {
      // var cors = require("cors");

      // app.use(cors());
      window.axios = require("axios");
      var cliendId = "ee7dd3a0044c4fedabb0bfbfca16e783";
      var redirectUri = "http://localhost:3000/index.vue";
      axios({
        method: "get",
        url: "https://accounts.spotify.com/authorize",
        // data: qs.stringify({
        //   response_type: "code",
        //   client_id: cliendId,
        //   redirect_uri: redirectUri
        // }),
        headers: {
          "content-type": "application/x-www-form-urlencoded",
          Authorization: this.token,
          // "Access-Control-Allow-Headers":
          //   "X-Requested-With,content-type",
          //   "Access-Control-Allow-Methods":'GET, POST, OPTIONS, PUT, PATCH, DELETE',
          // "Access-Control-Allow-Origin": "http://localhost:3000",
          // "Access-Control-Allow-Credentials": true
        }
      });
    }
    // login() {
    //   window.axios = require("axios");
    //   var cliendId = "ee7dd3a0044c4fedabb0bfbfca16e783";
    //   var scopes = "user-read-private user-read-email";
    //   var redirect_uri = "http://localhost:3000/index.vue";

    //   var URL =
    //     "https://accounts.spotify.com/authorize?client_id=" +
    //     cliendId +
    //     "&response_type=code&redirect_uri=" +
    //     encodeURIComponent(redirect_uri) +
    //     "&scope=user-read-private%20user-read-email&state=34fFs29kd09";
    //   //////////////////////

    //   var url =
    //     "https://api.spotify.com/authorize" +
    //     "?response_type=code" +
    //     "&client_id=" +
    //     cliendId +
    //     (scopes ? "&scope=" + encodeURIComponent(scopes) : "") +
    //     "&redirect_uri=" +
    //     encodeURIComponent(redirect_uri);

    //   axios
    //     .get("https://api.spotify.com/authorize", {
    //       headers: {
    //         "Content-Type": "application/json",
    //         Authorization: this.token
    //       },
    //       paramsSerializer: function(params) {
    //         var result =
    //           "?response_type=code&client_id=" +
    //           cliendId +
    //           (scopes ? "&scope=" + encodeURIComponent(scopes) : "") +
    //           "&redirect_uri=" +
    //           encodeURIComponent(redirect_uri);
    //         return result;
    //       }
    //     })
    //     // axios
    //     //   .get(url, {
    //     //     headers: {
    //     //       "Content-Type": "application/x-www-form-urlencoded;charset=utf-8",
    //     //       Authorization: this.token
    //     //     }
    //     //   })
    //     .then(response => {
    //       console.log(response);
    //       alert(response.description);
    //       this.info = response.data.description;
    //     })
    //     .catch(err => {
    //       console.log("this is the error");
    //       console.log(err.response);
    //     });
    // }
  }
};
</script>
