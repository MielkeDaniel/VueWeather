<template>
  <main>
    <div class="search-box">
      <input 
      type="text" 
      class="search-bar" 
      placeholder="Search..."
      v-model="query"
      @keypress="fetchWeather"
      />
    </div>

    <div class="weather-wrap" v-if="typeof weather.main != 'undefined'">
      <div class="location-box">
        <div class="location text-white text-center text-4xl font-normal">{{ weather.name }}, {{ weather.sys.country }}</div>
        <div class="date text-white text-center text-xl italic">Monday 20 January 2021</div>
      </div>
      
      <div class="weather-box text-center text-white">
        <div class="temp inline-block text-7xl rounded-2xl my-9">9°c</div>
        <div class="weather text-4xl">Rain</div>
      </div>  
    </div>
  </main>
</template>

<script>


export default {
  name: 'App',
  components: {
  },
  data() {
    return {
      api_key: "8a3e9e1e67daaf35b0f4a7cd460ad6cb",
      url_base: "http://api.openweathermap.org/data/2.5/",
      query: '',
      weather: {}
    }
  },
  methods: {
    fetchWeather(e) {
      if(e.key == 'Enter') {
        fetch(`${this.url_base}weather?q=${this.query}&units=metric&APPID=${this.api_key}`)
          .then(res => {
            return res.json();
          }).then(this.setResults);
      }
    },
    setResults (results) {
      this.weather = results;
    }
  }
}
</script>

<style>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

body {
  font-family: sans-serif;
}

#app {
  background-image: url('./assets/cold-bg.jpg');
  background-size: cover;
  background-position: bottom;
  transition: 0.5s;
}

main {
  min-height: 100vh;
  padding: 25px;

  background-image: linear-gradient(to bottom, rgba(0, 0, 0, 0.25), rgba(0, 0, 0, 0.75));
}

.search-box {
  width: 100%;
  margin-bottom: 30px;
}

.search-box .search-bar {
  display: block;
  width: 100%;
  padding: 15px;

  color: 313131;
  font-size: 20px;

  appearance: none;
  border: none;
  outline: none;
  background: none;

  box-shadow: 0px 0px 8px rgba(0, 0, 0, 0.25);
  background-color: rgba(255, 255, 255, 0.5);
  border-radius: 0px 16px 0px 16px;
  transition: 0.5s;
}

.search-box .search-bar:focus {
  box-shadow: 0px 0px 18px rgba(0, 0, 0, 0.25);
  background-color: rgb(255, 255, 255);
  border-radius: 16px 0px 18px 0px;
}

.weather-box .temp {
  padding: 10px 25px;
  font-weight: 600;

  text-shadow: 3px 6px rgba(0, 0, 0, 0.25);
  background-color: rgba(255, 255, 255, 0.25);
  border-radius: 16px;

  box-shadow: 3px 4px rgba(0, 0, 0, 0.25)
} 

.weather-box .weather {
  font-weight: 600;
  text-shadow: 3px 6px rgba(0, 0, 0, 0.25);
}
</style>
