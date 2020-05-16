<template>
  <div>
    <h2>Choose a character</h2>
    <div>
      <form v-on:submit.prevent>
        <input
          class="search"
          type="text"
          v-model="search"
          placeholder="Search for a character"
          v-on:keyup="searchForPerson"
        />
      </form>
      <br />
      <select v-on:change="handleSelect" v-model="selectedPerson">
        <option v-for="(person, index) in people" :key="index" :value="person">{{person.name}}</option>
      </select>
    </div>
  </div>
</template>

<script>
import { eventBus } from "../main.js";

export default {
  name: "people-filter",
  data() {
    return {
      search: "",
      selectedPerson: {}
    };
  },
  props: ["people"],
  methods: {
    searchForPerson() {
      let foundPerson = this.people.find(person => {
        return (
          person.name.toLowerCase().indexOf(this.search.toLowerCase()) > -1
        );
      });
      this.selectedPerson = foundPerson;
      eventBus.$emit("person-selected", this.selectedPerson);
    },
    handleSelect() {
      eventBus.$emit("person-selected", this.selectedPerson);
    }
  }
};
</script>

<style>
</style>