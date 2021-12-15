<template>
  <div class="hello">
    <header>
      <div class="title">
        <h1 class="app_title">IP Address Tracker</h1>
      </div>
      <div class="searchBar">
        <form class="shorten-url-form" @submit.prevent="submit(IP)">
          <input class="ip_input" v-model="IP" placeholder="Search for any IP address or domain" required>
          <button class="search_button" type="button" v-on:click="getIPGeolocation()" @click="data"><b>></b></button>
        </form>
      </div>
      <div class="info_section">
        <div class="ip info_wrapper">
          <h3>IP ADDRESS</h3>
          <h2 class="ip_address">{{ IPGeolocation.ip }}</h2>
        </div>
        <div class="location info_wrapper">
          <h3>LOCATION</h3>
          <h2 class="location_value">{{ IPGeolocation.location.city }}
            {{ IPGeolocation.location.country }}</h2>
        </div>
        <div class="time_zone info_wrapper">
          <h3>TIMEZONE</h3>
          <h2 class="time_zone_value">{{ IPGeolocation.location.timezone }}</h2>
        </div>
        <div class="isp info_wrapper">
          <h3>ISP</h3>
          <h2 class="isp_value">{{ IPGeolocation.isp }}</h2>
        </div>
      </div>
    </header>
    <main>
      <div id="map">
        
      </div>
    </main>
  </div>
</template>

<script>
  import axios from 'axios'
  import L from 'leaflet';
  export default {
    name: 'HelloWorld',
    
    data: () => {
      return {
        IP: "",
        IPGeolocation: []
      }
    },
    props: {

    },
    mounted() {
      this.getIPGeolocation()
    },
    methods: {
      getIPGeolocation() {

        var self = this
        var api_key = 'at_mmXglrBsbTRaQK68Rdz2dU6AdLd9D'
        axios.get('https://geo.ipify.org/api/v1', {
          params: {
            apiKey: api_key,
            ipAddress: this.IP
          }
        }).then(function (response) {
          self.IPGeolocation = response.data
        }).then(function () {
          self.initializeMap()
        });
      },
      initializeMap() {
					var container = L.DomUtil.get('mapid');
					if (container != null) {
						container._leaflet_id = null;
					}
					var lng = this.IPGeolocation.location.lng
					var lat = this.IPGeolocation.location.lat

					var map = L.map('mapid').setView([lat, lng], 13);

					L.tileLayer('https://api.mapbox.com/styles/v1/{id}/tiles/{z}/{x}/{y}?access_token={accessToken}', {
    attribution: 'Map data &copy; <a href="https://www.openstreetmap.org/">OpenStreetMap</a> contributors, <a href="https://creativecommons.org/licenses/by-sa/2.0/">CC-BY-SA</a>, Imagery © <a href="https://www.mapbox.com/">Mapbox</a>',
    maxZoom: 18,
    id: 'mapbox/streets-v11',
    tileSize: 512,
    zoomOffset: -1,
    accessToken: 'pk.eyJ1IjoiYmVueW50YiIsImEiOiJja3g3bnZodXMwYXp0MnZuM2NwNXhxMWpqIn0.WI5PF5ywI_tRUbLVQ5JB_A'
}).addTo(map);
					var marker = L.marker([lat, lng]).addTo(map);
				}
    }
  }
</script>

<style scoped>
  * {
    box-sizing: border-box;
    margin: 0;
    padding: 0;
    font-family: 'Rubik', sans-serif;
  }

  body {
    margin: 0px auto;
    width: 100vw;
    max-width: 1920px;
    background-color: lightgray;
    overflow: hidden;
    overflow-y: visible;
    height: 100vh;
    min-height: 640px;

  }

  /* HEADER */
  header {
    width: 100%;
    height: 225px;
    position: relative;
    z-index: 1000;
    background-image: url(../assets/images/pattern-bg.png);
    background-position: center;
    background-repeat: no-repeat;
    background-size: auto 100%;
    display: flex;
    flex-direction: column;
    flex-wrap: nowrap;
    align-items: center;
    overflow-y: visible;
  }

  .title {
    padding: 25px 0px;
  }

  .title h1 {
    color: white;
    font-size: 20px;
  }

  .searchBar {
    display: flex;
    justify-content: space-around;
    align-items: center;
    width: 80%;
    margin-bottom: 20px;
  }

  input {
    height: 45px;
    width: 85%;
    border: 0px;
    border-bottom-left-radius: 10px;
    border-top-left-radius: 10px;
    padding-left: 20px;
    outline: none;
    font-size: 18px;
  }

  button {
    height: 45px;
    width: 15%;
    border: 0px;
    background-color: black;
    color: white;
    border-bottom-right-radius: 10px;
    border-top-right-radius: 10px;
    outline: none;
  }

  .info_section {
    width: 80%;
    background-color: white;
    display: flex;
    flex-wrap: nowrap;
    flex-direction: column;
    align-content: center;
    justify-content: space-between;
    padding: 10px 0px;
    border-radius: 10px;
  }

  .info_wrapper {
    text-align: center;
    padding-top: 10px;
    padding-bottom: 10px;
  }

  .info_wrapper h2 {
    margin-bottom: 10px;
    font-size: 10px;
    color: gray;
  }

  /* MAIN */
  main {
    width: 100%;
  }

  #map {
    min-height: 50px;
  }

  @media only screen and (min-width:576px) {
    .searchBar {
      width: 50%;
    }

    .info_section {
      width: 50%;
    }

  }

  @media only screen and (min-width:768px) {
    .searchBar {
      width: 30%;
    }

    .info_section {
      width: 30%;
    }
  }

  @media only screen and (min-width:992px) {
    header {
      background-size: 100% auto;
    }

    .searchBar {
      width: 40%;
    }

    input {
      width: 90%;
    }

    button {
      width: 10%;
    }

    .info_section {
      height: 136px;
      padding-top: 25px;
      padding-bottom: 25px;
      width: 80%;
      flex-direction: row;
      justify-content: space-evenly;

    }

    .info_wrapper {
      height: 86px;
    }

    .info_section div {
      width: 25%;
      padding-right: 20px;
      padding-left: 20px;
      border-right: 1px solid lightgray;
      text-align: center;
    }

    .isp {
      border: none;
    }
  }
</style>