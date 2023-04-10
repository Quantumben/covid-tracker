<template>
  <div class="home">Hello World</div>
</template>

<script>
export default {
  name: "HomeView",
  components: {},
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
    console.log(data)
  },
};
</script>
