<template>
  <div id="app">
    <main-header></main-header>
    <div class="main-container">
      <div v-if="!films.length">
        <h1>Content Loading</h1>
      </div>
      <main-list :films="films" class="content-section"></main-list>
      <main-filter :films="films" class="content-section"></main-filter>
      <main-detail class="content-section"></main-detail>
      <locations-list :locations="locations" class="content-section"></locations-list>
      <people-list :people="people" class="content-section"></people-list>
      <people-filter :people="people" class="content-sextion"></people-filter>
      <people-detail class="content-section"></people-detail>
      <vehicles-list :vehicles="vehicles" class="content-section"></vehicles-list>
    </div>
    <main-canvas></main-canvas>
    <main-footer></main-footer>
  </div>
</template>

<script>
import MainList from "./components/MainList";
import MainFilter from "./components/MainFilter";
import MainDetail from "./components/details/MainDetail";
import MainHeader from "./components/layouts/MainHeader";
import MainFooter from "./components/layouts/MainFooter";
import MainCanvas from "./components/layouts/MainCanvas";
import LocationsList from "./components/LocationsList";
import PeopleList from "./components/PeopleList";
import PeopleFilter from "./components/PeopleFilter";
import PeopleDetail from "./components/details/PeopleDetail";
import VehiclesList from "./components/VehiclesList";

export default {
  name: "app",
  data() {
    return {
      films: [],
      locations: [],
      people: [],
      vehicles: []
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
    getVehicles: function() {
      fetch("https://ghibliapi.herokuapp.com/vehicles?limit=250")
        .then(res => res.json())
        .then(vehicles => (this.vehicles = vehicles))
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
    this.getVehicles();
  },
  components: {
    "main-list": MainList,
    "main-detail": MainDetail,
    "main-header": MainHeader,
    "main-footer": MainFooter,
    "main-canvas": MainCanvas,
    "main-filter": MainFilter,
    "locations-list": LocationsList,
    "people-list": PeopleList,
    "people-filter": PeopleFilter,
    "people-detail": PeopleDetail,
    "vehicles-list": VehiclesList
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
canvas {
  background: yellow;
}
.main-container {
  display: flex;
  flex-direction: row;
  align-content: flex-start;
  flex-wrap: wrap;
}
.content-section {
  padding: 2rem;
  max-width: 35%;
}
.main-footer {
  text-align: center;
  margin: 2rem 0 1rem 0;
  font-style: italic;
}
.film-description {
  padding: 0.5rem 0;
}
.search,
select {
  padding: 0.2rem;
}

@media (max-width: 600px) {
  .main-container {
    display: flex;
    flex-direction: column;
    padding: 1rem;
  }
  .content-section {
    max-width: 85%;
  }
  canvas {
    width: 0;
    height: 0;
    display: none;
  }
}
</style>