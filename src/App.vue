<template>
  <div id="app">
    <main-header></main-header>
    <div class="main-container">
      <main-filter :films="films"></main-filter>
      <main-detail></main-detail>
      <main-list :films="films"></main-list>
      <locations-list :locations="locations"></locations-list>
      <people-list :people="people"></people-list>
    </div>
    <main-footer></main-footer>
  </div>
</template>

<script>
import MainList from "./components/MainList";
import MainFilter from "./components/MainFilter";
import MainDetail from "./components/MainDetail";
import MainHeader from "./components/layouts/MainHeader";
import MainFooter from "./components/layouts/MainFooter";
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
      switch (error) {
        case "404":
          console.log("Page not found", error.status);
          break;
        case "401":
          console.log("Page access forbidden");
        case "500":
          console.log("Server down");
          break;
        default:
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
    "main-filter": MainFilter,
    "locations-list": LocationsList,
    "people-list": PeopleList
  }
};
</script>

<style>
* {
  margin: 0;
  padding: 0;
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
main-filter,
main-detail,
main-list,
location-list,
people-list {
  padding: 2rem;
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
.main-container {
  display: flex;
  align-content: space-around;
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