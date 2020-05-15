<template>
  <div class="list">
    <h2>Select a film</h2>
    <div>
      <select v-on:change="handleSelect" v-model="selectedFilm">
        <option v-for="(film, index) in films" :key="index" :value="film">{{film.title}}</option>
      </select>
    </div>
    <h3>All Films</h3>
    <div>
      <ol>
        <li v-for="(film, index) in films" :film="film" :key="index">{{film.title}}</li>
      </ol>
    </div>
  </div>
</template>

<script>
import { eventBus } from "../main.js";

export default {
  name: "main-list",
  data() {
    return {
      selectedFilm: {}
    };
  },
  props: ["films"],
  methods: {
    handleSelect() {
      eventBus.$emit("film-selected", this.selectedFilm);
    }
  }
};
</script>

<style>
</style>