<template>
  <div id="app">
    <h1>Title</h1>
    <main-detail></main-detail>
    <main-list></main-list>
  </div>
</template>

<script>
import { eventBus } from "@/main.js";
import MainList from "./components/MainList";
import MainDetail from "./components/MainDetail";


export default {
  name: "app",
  data() {
    return {
      data: {}
    };
  },
  computed: {},
  methods: {
    handleError(error) {
      if (error.status == "404") {
        console.log("Page not found", error.status);
      } else if (error.status == "401") {
        console.log("Page forbidden");
      } else if ((error.status == "500", error.status)) {
        console.log("Server down", error.status);
      } else {
        console.log(error.status);
      }
    }
  },
  mounted() {
    fetch()
      .then(res => res.json())
      .then(data => (this.data = data))
      .catch(error => handleError(error));
  },
  components: {
    "main-list" : MainList,
    "main-detail" : MainDetail
  }
};
</script>

<style>
*{
  margin: 0px;
  padding: 0px;
}
body{
  padding: 1rem;
  font-family: Arial, "Helvetica Neue", Helvetica, sans-serif;
  font-size: 1rem;
  background-color: antiquewhite;
}
h1{
  text-align: center;
}
ul{
  list-style: none;
}

</style>