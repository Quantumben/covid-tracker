<template>
  <main class="main" v-if="!loading">
      Show Data
  </main>

  <main class="flex flex-col align-center justify-center text-center" v-else>
    <div class="text-gray-500 text-3xl mt-10 mb-6">
        Fetching Data
    </div>

    <!--
      we are binding the loading image here with :src
    
    -->
    <img :src="loadingImage" class="w-24 m-auto" alt="">

  </main>
</template>

<script>
import hourglassImg from "../assets/hourglass.gif";

export default {
  name: "HomeView",
  components: {},
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
