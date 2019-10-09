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
      currentPlace: {}
    };
  },
  created: function() {
    axios.get("api/places").then(response => {
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
  }
};
</script>
