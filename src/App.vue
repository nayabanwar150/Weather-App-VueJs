<template>
  <div id="app" :class="typeof weather.main != 'undefined' && weather.weather[0].main == 'Haze'  ? 
    'cloud-bg' : ''">
    <Weather v-bind:weather="weather" v-on:search="fetchWeather" />
  </div>
</template>

<script>
import Weather from './components/Weather';
import axios from 'axios';

export default {
  name: 'App',
  components: {
    Weather
  },
  data(){
    return{
      base_url : 'api.openweathermap.org/data/2.5/weather?q=',
      api_key : '8d8c398df7ae5e2e8f8f7aabb70c86d4',
      city_name : 'Delhi',
      weather: []
    }
  },
  created(){
    this.fetchWeather(this.city_name);
  },
  methods:{
    fetchWeather(search_city){
      
      this.city_name = search_city;
      axios.get('http://api.openweathermap.org/data/2.5/weather?q='+this.city_name+'&?units=metric&APPID='+this.api_key)
      .then(response => this.weather = response.data)
      .catch(err => console.log(err));
    }
  }
}
</script>

<style>
*{
  padding: 0;
  margin: 0;
  box-sizing: border-box;
}

body{
  font-family: Georgia, 'Times New Roman', Times, serif;
}

#app{
  background-image: url('./assets/main-bg.jpg');
  background-size: cover;
  background-position: bottom;
  transition: 0.4s;
}

.cloud-bg{
  background-color: url('./assets/cloud-bg.jpg');
}

</style>
