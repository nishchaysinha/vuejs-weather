<template>
  <div id="app" :class="typeof weather.main != 'undefined' && weather.main.temp > 25 ? 'warm':''">
    <main>
      <div class="search-box">
        <input type="text" class="search-bar" placeholder="Search for a Place..." v-model="query" @keypress="fetchWeather"/>
        
      </div>
      <div class="weather-wrapper" v-if="typeof weather.main != 'undefined'">
        <div class="location-box">
          <div class="location">{{weather.name}}, {{weather.sys.country}}</div>
          <div class="date">{{dateBuilder()}}</div>
        </div>

        <div class="weather-box">
          <div class="temp">{{Math.round(weather.main.temp)}}°C</div>
          <div class="weather">{{weather.weather[0].main}}</div>
        </div>
      </div>
    </main>
  </div>
</template>

<script>
  export default {
    name: "app",
    data(){
      return{
      api_key: '323859ab1dd9648172b8ab428b2d89f5',
      url_base: 'http://api.openweathermap.org/data/2.5/',
      query:'',
      weather: {}

      }
      
    },
  methods:{
    fetchWeather (e){
      if(e.key=="Enter"){
      fetch(`${this.url_base}weather?q=${this.query}&units=metric&APPID=${this.api_key}`).then(res =>{return res.json();}).then(this.setResults);
      }

    },
    setResults(results){
      this.weather=results;
    },
    dateBuilder () {
      let d =new Date()
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
*{
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

body{
  font-family: 'Futura', sans-serif;

}
#app{
  background-image: url('./assets/cold.jpg');
  background-size: cover;
  background-position: bottom;
  transition: 0.4s;
}

#app.warm{
  background-image: url('./assets/hot.jpg');
}

main{
  min-height: 100vh;
  padding: 75px;
  background-image: linear-gradient(to bottom, rgba(0,0,0,0.2), rgba(0,0,0,0.7));
}

.search-box{
  width: 100%;
  margin-bottom: 35px;
}

.search-box .search-bar{
  display: block;
  width: 100%;
  padding: 20px;
  font-size: 20px;
  color: #313131;
  
  

  appearance: none;
  border: none;
  outline: none;
  background: none;
  
  box-shadow: 10px 0px  rgb(255, 255, 255);
  background-color: rgba(220, 220, 220, 0.512);
  border-radius: 0px 25px 0px 25px;
  


  transition: 0.4s;

}

.search-box .search-bar:focus {
  background-color: rgba(255, 255, 255, 0.75);
box-shadow: -10px 0px rgba(255,255,255,1);
border-radius: 25px 0px 25px 0px;

}


.location-box .location{
  color: aliceblue;
  font-size: 32px;
  font-weight: 500;
  text-align: center ;
  text-shadow: 5px 1px rgba(0,0,0,1);
}

.location-box .date{
  color: aliceblue;
  font-size: 16px;
  font-weight: 300;
  font-style: italic;
  text-align: center;
  text-shadow: 1px 3px rgba(0,0,0,1);
}

.weather-box{
  padding-top: 5px;
  text-align: center;
}

.weather-box .temp{
  display: inline-block;
  padding: 10px 25px;
  color: aliceblue;
  font-size: 102px;
  font-weight: 900;
  text-shadow: 10px 1px rgba(0,0,0,1);
  background-color: rgba(255,255,255,0.2);
  border-radius: 20px 0px;
  margin: 30px 0px;
  box-shadow: 6px 6px; 
}

.weather-box .weather{
  color: aliceblue;
  font-size: 45px;
  font-weight: 600;
  font-style: italic;
  text-shadow: 7px 1px rgba(0,0,0,1);
}

</style>