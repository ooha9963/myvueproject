<template>
  <div id="app"  :class="typeof weather.main != 'undefined' && weather.main.temp > 16 ? 'warm' : ''">
   
   <main>
    <div class="search_box">
      <input 
       type="text"
       class="search_bar"
        placeholder="search..."
        v-model="query"
      @keypress="fetchWeather"
     />
     
    </div>

    <div class="weather-box"v-if="typeof weather.main != 'undefined'" >
     <div class="loction-box">
       <div class="location">{{ weather.name }}, {{ weather.sys.country }}</div>
       <div class="data">{{ dateBuilder() }}</div>
      </div>
    

     <div class="weather-details">
       <div class="temp">{{ Math.round(weather.main.temp) }}°c</div>
       <div class="weather">{{ weather.weather[0].main }}</div>
      </div> 
    </div>
   </main>
  </div>
</template>

 <script>


 export default {
  name: 'App',
  data () {
    return {
      api_key:'96b18472d36f0d6886eac4d51f1bc76e',
      url_base: 'https://api.openweathermap.org/data/2.5/',
      query: '',
      weather: {}
     }
   },
   method: {
    fetchweather (e) {
      if ("e.key == enter") {
        fetch(`${this.url_base}weather?q=${this.query}&units=metric&APPID=${this.api_key}`)
        .then(res => {
            return res.json();
          }).then(this.setResults);
      }
     },
     setResults (results) {
      this.weather = results;
     },
  
  
     dateBuilder () {
      let d = new Date();
      let months = ["January", "February", "March", "April", "May", "June", "July", "August", "September", "October", "November", "December"];
      let days = ["Sunday", "Monday", "Tuesday", "Wednesday", "Thursday", "Friday", "Saturday"];
      let day = days[d.getDay()];
      let date = d.getDate();
      let month = months[d.getMonth()];
      let year = d.getFullYear();
      return `${day} ${date} ${month} ${year}`;
    }
  }
}
  

</script>

<style>
 * {
  margin:0;
  padding:0;
  box-sizing:border-box;
}
 
 body {
   font-family:'montserrat',san-serif;
 }

 #app {
   background-image: url('./assets/cold.jpg');
   background-size:cover;
   background-position:middle;
   transiton:0.4s;
 }

 main {
  min-height: 100vh;
  padding: 25px;
  background-image: linear-gradient(to middle, rgba(0, 0, 0, 0.25), rgba(0, 0, 0, 0.75));
}
.search-box {
  width: 100%;
  margin-bottom: 10px;
}
.search-box .search-bar {
  display: block;
  width: 100%;
  padding: 15px;
  
  color: #313131;
  font-size: 30px;
  
  appearance: none;
  border:none;
  outline: none;
  background: none;
  
  box-shadow: 0px 0px 8px rgba(0, 0, 0, 0.5);
  background-color: rgba(255, 255, 255, 255);
  border-radius: 0px 16px 0px 16px;
  transition: 0.4s;
}
.search-box .search-bar:focus {
  box-shadow: 0px 0px 16px rgba(0, 0, 0, 0.25);
  background-color: rgba(255, 255, 255, 0.75);
  border-radius: 16px 0px 16px 0px;
}
.location-box .location {
   color: #FFF;
  font-size: 32px;
  font-weight: 500;
  text-align: center;
  text-shadow: 1px 3px rgba(0, 0, 0, 0.25);
}
.location-box .data {
  color: #FFF;
  font-size:32px;`
  font-weight:300;
  font-style: italic;
  text-align:center;
}
.weather-details{
  text-align: center;
}

.weather-details .temp {
  display: inline-block;
  padding: 10px 25px;
  color: #FFF;
  font-size: 102px;
  font-weight: 900;
  text-shadow: 3px 6px rgba(0, 0, 0, 0.25);
  background-color:rgba(255, 255, 255, 0.25);
  border-radius: 16px;
  margin: 30px 0px;
  box-shadow: 3px 6px rgba(0, 0, 0, 0.25);
}
.weather-details .weather {
  color: #FFF;
  font-size: 48px;
  font-weight: 700;
  font-style: italic;
  text-shadow: 3px 6px rgba(0, 0, 0, 0.25);
}
</style>
