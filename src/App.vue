<template>
  <div id="app">
    <input
      type="text"
      v-model="token"
      name="token"
      placeholder="Enter access token"
    />
    <button type="button" @click="getUser">GET /user</button>
    <div id="result">
      {{ result }}
    </div>
    <div id="error">
      {{ error }}
    </div>
  </div>
</template>

<script>
import axios from "axios";

export default {
  name: "app",
  data() {
    return {
      apiURL: "https://api-dev.endpass.com/v1",
      token: "",
      result: null,
      error: null
    };
  },
  methods: {
    getUser() {
      axios({
        method: "GET",
        url: `${this.apiURL}/user`,
        headers: {
          Authorization: `Bearer ${this.token}`,
          "X-Requested-With": "XMLHttpRequest"
        }
      })
        .then(response => {
          this.result = response;
        })
        .catch(error => {
          console.log(error);
          this.error = error;
        });
    }
  }
};
</script>

<style></style>
