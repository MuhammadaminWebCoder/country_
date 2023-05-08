<template>
      <div class="container">
            <form class="nav-form">
                  <div class="input-form">
                        <input type="text" class="inps" v-model="search" placeholder="Search for a country…">
                        <i class="far fa-search"></i>
                  </div>
                  <select name="cars" id="cars">
                        <option class="ss" value="FilteredByRegion">Filtered by region</option>
                        <option v-for="country in filteredCountries" :key="country.cca3" :value="country.region" >{{country.region}} </option>
                  </select>
            </form>
            <div :class="{'loader':loading}"></div>
            <ul class="allBox">
                  <li class="box" v-for="country in filteredCountries" :key="country.cca3">
                  <router-link :to="{ name : 'country', params :{id: country.name?.common.trim()}}">
                        <img :src="country.flags?.png" width="100%">
                  </router-link>
                        <div class="text">
                              <h3 :country="country.name?.common">{{country.name?.common}}</h3>
                              <span class="comp">Population: <span>{{country.population}}</span></span>
                              <span class="comp">Region: <span>{{country.region}}</span></span>
                              <span class="comp">Capital: <span v-for="capital in country.capital" :key="capital.id">{{capital}}</span></span>
                        </div>
                  </li>
            </ul>
            
      </div>
</template>

<script>
import './style.scss'
export default {
//       data() {
//             return {
//                   allCountry: [],
//                   apiUrl: 'https://restcountries.com/v3.1/all',
//                   loading: true,
//                   search: ""
//             };
//       },
//       async mounted() {
//             await this.fetchData();
//             this.loading = false
//       },
//       computed: {
//             allCountry() {
//                   return this.allCountry.filter((country) =>
//                   country.name.common.toLowerCase().includes(this.search.toLowerCase()));
//       }
//       },
//       methods: {
//             async fetchData() {
//                   const response = await fetch(this.apiUrl);
//                   const data = await response.json();
//                   this.allCountry = data;
//             },
//       },
// };
name: "CountryList",
  data() {
    return {
      countries: [],
      search: "",
      loading: true,
    };
  },
  async mounted() {
    const response = await fetch("https://restcountries.com/v3.1/all");
    const data = await response.json();
    this.countries = data;
    this.loading = false
  },
  computed: {
    filteredCountries() {
      return this.countries.filter((country) =>
        country.name.common.toLowerCase().includes(this.search.toLowerCase())
      );
    },
  },
};
</script>

