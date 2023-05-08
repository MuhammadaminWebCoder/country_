<template>
      <div class="container">
            <div class="back">
                  <router-link to="/">
                        <div class="CitemBtn"><i class="far fa-long-arrow-left"></i> <span>back</span></div>
                  </router-link>
            </div>
            <div class="indexBox">
                  <div class="IndImage">
                        <img width="100%" :src="country.flags?.png">
                  </div>
                  <div class="dalnx">
                        <h2>{{ country.name?.common }}</h2>
                        <div class="flex">
                              <div class="dalnx-one">
                                    <span class="comp">Native Name:
                                    <span v-for="countrys in country.name?.nativeName" :key="countrys.id">{{ countrys.official }}</span>
                              </span>
                                    <span class="comp">Population: <span>{{ country?.population }}</span></span>
                                    <span class="comp">Region: <span>{{ country?.region }}</span></span>
                                    <span class="comp">Sub Region:<span>{{ country?.subregion }}</span></span>
                                    <span class="comp">Capital: <span v-for="capi in country?.capital" :key="capi.id">{{ capi
                                    }}</span></span>
                              </div>
                              <div class="dalnx-two">
                                    <span class="comp">Top level domain: <span>{{ country?.Region }}</span></span>
                                    <span class="comp">Currencies: <span v-for="mony in country.currencies" :key="mony.id">{{ mony.symbol }}</span></span>
                                    <span class="comp">Languages: <span v-for="laguage in country.languages"
                                                :key="laguage.id">{{ laguage }} , </span></span>
                              </div>
                        </div>
                        <span class="comp Clast">Border Countries:<span class="CitemBtn" v-for="borders in country.borders"
                                    :key="borders.id">{{ borders || 'is undefined' }}</span></span>
                  </div>
            </div>
      </div>
</template>

<script>
let ok = '/img/hi__ok.svg'
export default {
      data() {
            return {
                  country: {},
            };
      },
      async mounted() {
            await this.fetchData();
      },
      methods: {
            async fetchData() {
                  const response = await fetch(`https://restcountries.com/v3.1/name/${this.$route.params.id}`);
                  const data = await response.json();
                  this.country = data[0];
            },
      },
};
</script>
