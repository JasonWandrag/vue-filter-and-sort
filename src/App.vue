<template>
  <div v-if="filteredPeople">
    <div class="sortBar">
      <label>
        Sort Age:
        <select v-model="age" @change="sortAge(age)">
          <option value="asc">Ascending</option>
          <option value="desc">Descending</option>
        </select>
      </label>
      <label>
        Sort Name:
        <select v-model="name" @change="sortName(name)">
          <option value="asc">Ascending</option>
          <option value="desc">Descending</option>
        </select>
      </label>
      <label>
        Filter Gender:
        <select v-model="gender" @change="filterGender(gender)">
          <option value="">All</option>
          <option value="male">Male</option>
          <option value="female">Female</option>
        </select>
      </label>
    </div>
    <div id="user-list">
      <Card
        v-for="(person, idx) of filteredPeople"
        :key="idx"
        :person="person"
        :idx="idx"
      />
    </div>
  </div>
  <div v-else>
    <h2>Summoning Humans...</h2>
  </div>
</template>

<script>
import Card from "./components/Card.vue";

export default {
  name: "App",
  components: { Card },
  // In the data, people keeps the original array,
  // and filteredPeople is what is used for display.
  // The rest is used for v-model binding
  data() {
    return {
      people: null,
      filteredPeople: null,
      age: "",
      name: "",
      gender: "",
    };
  },
  // Get information from API and write it to data
  mounted() {
    fetch("https://randomuser.me/api/?results=100")
      .then((res) => res.json())
      .then((data) => {
        this.people = data.results;
        this.filteredPeople = data.results;
      })
      .catch((err) => console.log(err));
  },
  methods: {
    // Sorting methods sort the filteredPeople
    // Filter methods check for all results in the people array, and writes the results to filteredPeople
    // This ensures that when sorting by age or name, you are still applying any filters
    sortAge(dir) {
      this.filteredPeople = this.filteredPeople.sort(
        (a, b) => a.dob.age - b.dob.age
      );
      if (dir == "desc") this.filteredPeople.reverse();
    },
    sortName(dir) {
      this.filteredPeople = this.filteredPeople.sort((a, b) => {
        if (a.name.first.toLowerCase() < b.name.first.toLowerCase()) {
          return -1;
        }
        if (a.name.first.toLowerCase() > b.name.first.toLowerCase()) {
          return 1;
        }
        return 0;
      });
      if (dir == "desc") this.filteredPeople.reverse();
    },
    filterGender(gender) {
      if (gender) {
        this.filteredPeople = this.people.filter(
          (person) => person.gender == gender
        );
      } else {
        this.filteredPeople = this.people;
      }
    },
  },
};
</script>

<style>
@import url(https://fonts.googleapis.com/css?family=Raleway:400,600);
*,
*:before,
*:after {
  box-sizing: border-box;
}

body {
  background: url(https://picsum.photos/1200);
  background-size: cover;
  background-attachment: fixed;
  padding-top: 60px;
}

.sortBar {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  z-index: 10;
  background-color: white;
  padding: 20px;
}

#user-list {
  display: flex;
  flex-wrap: wrap;
  justify-content: center;
}
</style>
