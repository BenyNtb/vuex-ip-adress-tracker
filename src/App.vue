<template>
  <div id="app">
    <Home/>
    <AddGoogleMap />
  </div>
</template>

<script>
import Home from './components/Home.vue'
import AddGoogleMap from "./components/AddGoogleMap";
export default {
  name: 'App',
  components: {
    Home,
    AddGoogleMap
  },
  data() {
    return {
      myloca: [50.8500, 4.3500]
    }
  },
  // methods: {
  //   switch(lat, long) {
  //     this.myloca = []
  //     this.myloca.push(lat,long)
  //   }
  // }
}
</script>

<style>

</style>
