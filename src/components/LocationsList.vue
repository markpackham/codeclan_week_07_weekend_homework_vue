<template>
  <div>
    <h3>Studio Ghibli Locations</h3>
    <div>
      <ul>
        <li
          v-for="(location, index) in locations"
          :location="location"
          :key="index"
        >{{location.name}}</li>
      </ul>
    </div>
  </div>
</template>

<script>
export default {
  name: "locations-list",
  data() {
    return {};
  },
  props: ["locations"]
};
</script>

<style>
</style>