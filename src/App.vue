<template>
  <div class="app">
    <NavBar />
    <div class="container mt-5">
      <h1 v-if="!data.length">Loading Countries...</h1>
      <CountriesList v-else :data="data" />
    </div>
  </div>
</template>

<script>
import NavBar from './components/NavBar.vue'
import CountriesList from './components/CountriesList.vue'

export default {
  components: {
    NavBar,
    CountriesList
  },
  data() {
    return {
      data: []
    }
  },
  async created() {
    const response = await fetch(`https://ih-countries-api.herokuapp.com/countries`)
    this.data = await response.json()
  }
}
</script>

<style>
li {
  list-style: none;
}
</style>