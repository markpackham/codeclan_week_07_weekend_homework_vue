<template>
  <div id="app">
    <main-header></main-header>
    <div class="main-container">
      <main-list :films="films"></main-list>
      <main-detail></main-detail>
    </div>
    <div class="locations-list">
      <locations-list :locations="locations"></locations-list>
    </div>
    <div class="people-list">
      <people-list :people="people"></people-list>
    </div>
    <main-footer></main-footer>
  </div>
</template>

<script>
import MainList from "./components/MainList";
import MainDetail from "./components/MainDetail";
import MainHeader from "./components/MainHeader";
import MainFooter from "./components/MainFooter";
import LocationsList from "./components/LocationsList";
import PeopleList from "./components/PeopleList";

export default {
  name: "app",
  data() {
    return {
      films: [],
      locations: [],
      people: []
    };
  },
  computed: {},
  methods: {
    getFilms: function() {
      fetch("https://ghibliapi.herokuapp.com/films?limit=250")
        .then(res => res.json())
        .then(films => (this.films = films))
        .catch(error => handleError(error));
    },
    getLocations: function() {
      fetch("https://ghibliapi.herokuapp.com/locations?limit=250")
        .then(res => res.json())
        .then(locations => (this.locations = locations))
        .catch(error => handleError(error));
    },
    getPeople: function() {
      fetch("https://ghibliapi.herokuapp.com/people?limit=250")
        .then(res => res.json())
        .then(people => (this.people = people))
        .catch(error => handleError(error));
    },
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
    this.getFilms();
    this.getLocations();
    this.getPeople();
  },
  components: {
    "main-list": MainList,
    "main-detail": MainDetail,
    "main-header": MainHeader,
    "main-footer": MainFooter,
    "locations-list": LocationsList,
    "people-list": PeopleList
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
h3,
h4 {
  padding: 1rem;
}
button {
  padding: 0.3rem;
  margin: 0.5rem;
  border-radius: 5px;
}
button:hover {
  font-size: 1.1rem;
  border-width: 0.2rem;
}
.btn-danger {
  background-color: red;
  color: white;
  font-weight: bold;
}
ul {
  list-style: none;
}
.list {
  padding: 1rem;
  min-width: 40%;
}
.main-container {
  display: flex;
  justify-content: flex-start;
}
.main-footer {
  text-align: center;
  margin-top: 2rem;
}
.detail {
  padding: 1rem;
}
.film-description {
  max-width: 60%;
  padding: 0.5rem 0;
}
</style>