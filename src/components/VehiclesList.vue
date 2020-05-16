<template>
  <div>
    <h3>Vehicles</h3>
    <div>
      <ul>
        <li v-for="(vehicle, index) in vehicles" :vehicle="vehicle" :key="index">
          <strong>{{vehicle.name}}:</strong>
          {{vehicle.description}} - {{vehicle.vehicle_class}}
        </li>
      </ul>
    </div>
  </div>
</template>

<script>
export default {
  name: "vehicles-list",
  data() {
    return {};
  },
  props: ["vehicles"]
};
</script>

<style>
</style>