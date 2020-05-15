<template>
  <div class="list">
      <h2>Main List</h2>
            <ol>
                <li v-for="(film, index) in films" :film="film" :key="index">{{film.title}}</li>
            </ol>
    </div>
</template>

<script>
export default {
  name: "main-list",
  props: ["films"],
};
</script>

<style>
.list {
  padding: 1rem;
}
</style>