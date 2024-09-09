<template>
  <div>
    <label for="place-select">Selecciona un lugar</label>
    <select v-model="selectPlace" id="place-select">
      <option
        v-for="place in places"
        :key="place.cca3"
        :value="place.name.common"
      >
        {{ place.name.common }}
      </option>
    </select>
    <button @click="addPlace">Añadir un lugar</button>
  </div>
</template>

<script>
import axios from "axios";
export default {
  data() {
    return {
      places: [],
      selectPlace: null,
    };
  },
  methods: {
    fetchPlaces() {
      axios.get("https://restcountries.com/v3.1/all").then((response) => {
        this.places = response.data;
      });
    },

    addPlace() {
      this.$emit("add-place", this.selectPlace);
    },
  },
  mounted() {
    this.fetchPlaces();
  },
};
</script>
