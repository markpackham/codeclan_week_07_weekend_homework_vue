<template>
  <div>
    <div v-if="person">
      <h2>{{person.name}}</h2>
      <ul>
        <li>Gender: {{person.gender}}</li>
        <li>Age: {{person.age}}</li>
        <li>Eye Color: {{person.eye_color}}</li>
        <li>Hair Color: {{person.hair_color}}</li>
      </ul>
    </div>
  </div>
</template>

<script>
import { eventBus } from "@/main.js";

export default {
  name: "person-detail",
  data() {
    return {
      person: null
    };
  },
  props: ["people"],
  methods: {},
  mounted() {
    eventBus.$on("person-selected", person => {
      this.person = person;
    });
  }
};
</script>

<style>
</style>