<template>
  <main class="main" v-if="!loading">
    <!-- 
      This where we are using our defined components
      where we are binding the following
      :title binding title from data object defined below
      :dataDate binding dataDate from data object defined below
    -->
    <DataTitle :title="title" :dataDate="dataDate" />

    <!-- 
      This where we are using our defined components
      where we are binding the following
      :stats binding title from data object defined below
    -->
    <DataBoxes :stats="stats" />

    <!-- 
      This where we are using our defined components
      where we are binding the following
      :countries binding title from data object defined below
    -->
    <CountrySelect @get-country="getCountryData" :countries="countries" />

    <button 
    @click="clearCountryData"
    v-if="stats.Country" 
    class="bg-green-700 text-white rounded p-3 mt-10 focus:outline-none hover:bg-green-6">
      Clear Country
    </button>
  </main>

  <main class="flex flex-col align-center justify-center text-center" v-else>
    <div class="text-gray-500 text-3xl mt-10 mb-6">Fetching Data</div>

    <!--
      we are binding the loading image here with :src
    
    -->
    <img :src="loadingImage" class="w-24 m-auto" alt="" />
  </main>
</template>

<script>
import hourglassImg from "../assets/hourglass.gif";
import DataTitle from "@/components/DataTitle.vue";
import DataBoxes from "@/components/DataBoxes.vue";
import CountrySelect from "@/components/CountrySelect.vue";

export default {
  name: "HomeView",
  components: {
    DataTitle,
    DataBoxes,
    CountrySelect,
  },
  data() {
    return {
      loading: true,
      title: "Global",
      dataDate: "",
      stats: {},
      countries: [],
      loadingImage: hourglassImg,
    };
  },
  methods: {
    async fetchCovidData() {
      const res = await fetch("https://api.covid19api.com/summary");
      const data = await res.json();
      return data;
    },
    getCountryData(country){
      this.stats = country
      this.title = country.Country
    },
    async clearCountryData(){
      this.loading = true
      const data = await this.fetchCovidData()
      this.title = 'Global'
      this.stats = data.Global
      this.loading = false
    }
  },
  async created() {
    //created is a lifecycle method in vuejs that runs before the app is been mounted
    const data = await this.fetchCovidData();

    //after fetching the data push or assign it to the following
    this.dataDate = data.Date;
    this.stats = data.Global;
    this.countries = data.Countries;
    this.loading = false;
  },
};
</script>
