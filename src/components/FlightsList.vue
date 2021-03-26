<template>
  <ul>
    <FlightsListItem
      v-for="(flight, index) of flightsList"
      :key="index"
      v-bind:flight="flight"
    />
  </ul>
</template>

<script>
import FlightsListItem from "@/components/FlightsListItem";

export default {
  props: ["flightsList"],
  components: { FlightsListItem },

};
</script>