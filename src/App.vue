<template>
  <div id="app1" :class="typeof weather.main != 'undefined' && weather.main.temp >16 ?
    'warm' : '' ">
    <main>
      <div class="search-box">
        <input
         type="text"
          class="search-bar" 
          v-model="query" 
          @keypress="fetchweather"
          placeholder="search..."
          >
      </div>

      <div class="weather-warp" v-if="typeof weather.main !='undefined'">
        <div class="location-box">
          <div class="location"> {{weather.name}} , {{weather.sys.country}} </div>
          <div class="date"> {{ dateBuilder() }} </div>
        </div>
        <div class="weather-box">
          <div class="temp"> {{Math.round(weather.main.temp)}}°C</div>
          <div class="weather"> {{ weather.weather[0].main }} </div>
        </div>
      </div>
    </main>
  </div>
</template>

<script>
export default {
  name: 'App',
  components: {
  },
  data(){
    return{
      api_key:"9fadbc8d1ce983872b27152b6695915f",
      url_base:'https://api.openweathermap.org/data/2.5/',
      query:'',
      weather:{}
    }
  },
  methods:{
    fetchweather(e){
      if(e.key=='Enter'){
        fetch(`${this.url_base}weather?q=${this.query}&appid=${this.api_key}`)
          .then((res) =>{
            return res.json();
          }).then(this.setResults)
      }
    },
    setResults(results){
      this.weather = results
    },
    dateBuilder(){
      let d = new Date();
      let months = ["January" , "February" , "March" , "April" , "May" ,
       "June" , "July" , "August" , "September" , "October" ,"November" ,
       "December"];
       let days =["Sunday" , "Monday" , "Tuseday" , "Wednesday" , "Thursday" ,
       "Friday" , "Saturdy"] ;

       let day = days[d.getDay()];
       let date = d.getDate();
       let month = months[d.getMonth()];
       let year = d.getFullYear();

       return`${day} ${date} ${month} ${year} `
    }
  }
}
</script>

<style>
@import './assets/style.css'
</style>
