<template>
  <div id="app">
    <main-header></main-header>
    <div class="main-container">
      <main-list :films="films"></main-list>
      <main-detail></main-detail>
    </div>
    <main-footer></main-footer>
  </div>
</template>

<script>
import MainList from "./components/MainList";
import MainDetail from "./components/MainDetail";
import MainHeader from "./components/MainHeader";
import MainFooter from "./components/MainFooter";

export default {
  name: "app",
  data() {
    return {
      films: []
    };
  },
  computed: {},
  methods: {
    handleError: function(error) {
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
    fetch("https://ghibliapi.herokuapp.com/films")
      .then(res => res.json())
      .then(films => (this.films = films))
      .catch(error => handleError(error));
  },
  components: {
    "main-list": MainList,
    "main-detail": MainDetail,
    "main-header": MainHeader,
    "main-footer": MainFooter
  }
};
</script>

<style>
* {
  margin: 0px;
  padding: 0px;
}
body {
  padding: 2rem;
  font-family: Arial, "Helvetica Neue", Helvetica, sans-serif;
  font-size: 1rem;
  background-color: antiquewhite;
}
h1 {
  text-align: center;
}
h1,
h2,
h3 {
  padding: 1rem;
}
ul {
  list-style: none;
}
.list {
  padding: 1rem;
}
.main-container {
  display: flex;
  justify-content: flex-start;
}
.main-footer {
  text-align: center;
  margin-top: 2rem;
}
</style>