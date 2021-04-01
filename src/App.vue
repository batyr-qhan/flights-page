<template>
  <div id="app">
    <div class="filters">
      <FlightOptions @clicked="onCheckboxClick" />
      <Airlines v-bind:airlinesList="airlinesList" />
    </div>
    <div class="flightsList">
      <FlightsList v-bind:flightsList="filteredFlightsList" />
    </div>
  </div>
</template>

<script>
import FlightOptions from "@/components/FlightOptions";
import Airlines from "@/components/Airlines";
import FlightsList from "@/components/FlightsList";

export default {
  name: "App",
  components: {
    FlightOptions,
    Airlines,
    FlightsList,
  },
  data() {
    return {
      flightsList: [],
      airlinesList: {},
      optionsFilters: [],
    };
  },
  mounted() {
    this.getFlightsList();
  },
  methods: {
    onCheckboxClick(value) {
      this.optionsFilters = value;
      console.log(value);
    },
    getFlightsList() {
      fetch("results.json")
        .then((res) => res.json())
        .then((data) => {
          this.airlinesList = data.airlines;
          this.flightsList = data.flights;
        })
        .catch((err) => console.error("Error", err));
    },
  },
  computed: {
    filteredFlightsList() {
      if (!this.optionsFilters.length) return this.flightsList;

      let result = this.flightsList;

      console.log("before loop", result);

      this.optionsFilters.forEach((item) => {
        if (item === "onlyDirect") {
          result = result.filter((flight) => {
            return flight.itineraries[0][0].stops === 0;
          });
        }
        // if (item === 'withBaggage') {
        //   console.log('catched with baggage')
        // }
        if (item === "onlyReturn") {
          result = result.filter((flight) => {
            return flight.refundable === true;
          });
        }
      });
      return result;
    },
  },
};
</script>

<style>
#app {
  padding: 40px 150px 0 150px;
  display: flex;
  font-family: "Open Sans", sans-serif;
  /* font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px; */
}
.filters {
  width: 240px;
  margin-right: 20px;
}
.flightsList {
  flex: 1;
}
</style>
