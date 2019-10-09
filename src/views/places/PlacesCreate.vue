<template>
  <div class="places-create">
    <h1>New Place</h1>
    <div>
      Name:
      <input type="text" v-model="newPlaceName" />
      {{ newPlaceName }}
      <br />
      Address:
      <input type="text" v-model="newPlaceAddress" />
      {{ newPlaceAddress }}
      <br />
    </div>
    <button v-on:click="createPlace()">Create</button>
  </div>
</template>
<style></style>

<script>
import axios from "axios";

export default {
  data: function() {
    return {
      places: [],
      newPlaceName: "",
      newPlaceAddress: "",
      currentPlace: {}
    };
  },

  methods: {
    createPlace: function() {
      var params = {
        name: this.newPlaceName,
        address: this.newPlaceAddress
      };
      axios
        .post("/api/places", params)
        .then(response => {
          console.log("Success", response.data);
          this.places.push(response.data);
          this.newPlaceName;
          this.newPlaceAddress;
        })
        .catch(error => {
          console.log(error.response.data.errors);
        });
    }
  }
};
</script>
