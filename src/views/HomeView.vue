<template>
  <div class="home">Hello World</div>
</template>

<script>
import hourglassImg from '../assets/hourglass.gif';

export default {
  name: "HomeView",
  components: {},
  data() {
    return {
      loading: true,
      title: 'Global',
      dataDate: '',
      stats: {},
      countries: [],
      loadingImage: hourglassImg
    }
  },
  methods: {
    async fetchCovidData(){
      const res = await fetch('https://api.covid19api.com/summary')
      const data = await res.json()
      return data
    }
  },
  async created() {
    //created is a lifecycle method in vuejs that runs before the app is been mounted
    const data = await this.fetchCovidData()
    
    //after fetching the data push or assign it to the following
    this.dataDate = data.Date
    console.log(this.dataDate)
  },
};
</script>
