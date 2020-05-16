<template>
  <div>
    <h3>People List</h3>
    <div>
      <ul>
        <li v-for="(person, index) in people" :person="person" :key="index">{{person.name}}</li>
      </ul>
    </div>
  </div>
</template>

<script>
export default {
  name: "people-list",
  data() {
    return {};
  },
  props: ["people"]
};
</script>

<style>
</style>