<template>
  <div class="detail">
      <h2>Details</h2>
        <div v-if="film">
            <h2>{{film.title}}</h2>
            <p class="film-description">{{film.description}}</p>
            <p>Released: {{film.release_date}}</p>
            </div>
    </div>
</template>

<script>
import { eventBus } from "@/main.js";

export default {
  name: "main-detail",
  data() {
    return {
      film: null,
    };
  },
  props: ["films"],
  methods: {},
  mounted() {
    eventBus.$on("film-selected", film => {
      this.film = film;
    });
  },
};
</script>

<style>
.detail {
  padding: 1rem;
}
.film-description {
  max-width: 60%;
  padding: 0.5rem 0;
}
</style>