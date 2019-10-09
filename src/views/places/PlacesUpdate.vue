<template>
  <div class="places-index">
    <h1>All Places</h1>
    <div v-for="place in places">
      <h2>
        <b>Name:</b>
        {{ place.name }}
      </h2>
      <div>
        <button v-on:click="showPlace(place)">More Info</button>
      </div>
      <div v-if="place === currentPlace">
        <p>
          <b>Address:</b>
          {{ place.address }}
        </p>

        <h4>Edit Place</h4>
        <div>
          Name:
          <input type="text" v-model="place.name" />
          {{ place.name }}
          <br />
          Address:
          <input type="text" v-model="place.address" />
          {{ place.address }}
          <br />
          <button v-on:click="updatePlace()">Update</button>
          <br />
          <button v-on:click="destoryPlace()">Destroy</button>
        </div>
      </div>
    </div>
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

  created: function() {
    axios.get("/api/places").then(response => {
      this.places = response.data;
      console.log(this.places);
    });
  },

  methods: {
    showPlace: function(place) {
      if (this.currentPlace === place) {
        this.currentPlace = {};
      } else {
        this.currentPlace = place;
      }
    }
  },

  updatePlace: function(place) {
    var params = {
      name: place.name,
      address: place.address
    };
    axios
      .patch("/api/places/" + place.id, params)
      .then(response => {
        console.log("Success", response.data);
      })
      .catch(error => {
        console.log(error.response.data.errors);
      });
  },
  destroyPlace: function(place) {
    axios.delete("/api/places" + place.id).then(response => {
      console.log("Success", response.data);
      var index = this.places.indexOf(place);
      console.log(index);
      this.places.splice(index, 1);
    });
  }
};
</script>
