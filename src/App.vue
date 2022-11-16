<template>
    <div class="app">
      <weather-search
          v-model="city.name"
          @update="updateAll"
         />

         <weather-current
          :city="city" 
          :current="current" 
         />

        <app-button
          @click="showDialog"
        >
          Show forecast
        </app-button>

         <app-dialog v-model:show="dialogVisible">
          <weather-forecast
            :city="city" 
            :forecast="forecast" 
            :days="days" 
          />
        </app-dialog>
    </div>
</template>

<script>
import WeatherSearch from "@/components/WeatherSearch";
import WeatherCurrent from "@/components/WeatherCurrent";
import WeatherForecast from "@/components/WeatherForecast";

export default {
  components: {
    WeatherSearch, WeatherCurrent, WeatherForecast
  },  
  data() {
      return {
        key: '184fce7e77911adf1c29831cd4980fee',   
        city: {
          name: 'Kyiv',      
          country: '',
          lat: 0,
          lon: 0,
        },
        current: {
          icon: '04d',
          temp: 0,
          minTemp: 0,
          maxTemp: 0,
          desc: '',
          wind: '',
          humidity: '',
        }, 
        forecast: [],
        days: [],
        dialogVisible: false
      }
  },
  created() {
    this.updateAll() 
  },
  methods: {
    updateAll() {
      this.currentWeather(),
      this.daysDate(),
      this.forecastWeather()
    },
    cityData() {
      const self = this;
      
      fetch('http://api.openweathermap.org/geo/1.0/direct?'
        + 'q='+ self.city.name 
        + '&appid=' + self.key
        + '&limit=1' //вернут даные о самом перевом городе, по мнению программы это самый важный город
        )
        .then(function(response) {
          return response.json()
        })
        .then(function(response) { 
          console.log(response);
          self.city.country = response[0].country;
          self.city.lat = response[0].lat;
          self.city.lon = response[0].lon;
        })
    },
    currentWeather() {
      const self = this;

      this.cityData();  

      setTimeout(function(){  
        fetch('https://api.openweathermap.org/data/2.5/weather?'
        + 'lat=' + self.city.lat
        + '&lon=' + self.city.lon 
        + '&appid=' + self.key 
        + '&units=metric' 
        ).then(function(response) {
          return response.json()
        })
        .then(function(data) {
          console.log(data);
          self.current.temp =	data.main.temp; //1-куда сохраняю 2-откды вытягиваю
          self.current.minTemp =	data.main.temp_min;
          self.current.maxTemp =	data.main.temp_max;
          self.current.icon =	data.weather[0].icon;
          self.current.desc =	data.weather[0].description;					
          self.current.wind =	data.wind.speed;					
          self.current.humidity =	data.main.humidity;		
        });          
      }, 1000)
    },
    getDayDate(date) {    //чтобы обработать дату и сохранить в нужном формате 
      let day = date.getDate(); //(вытягиваю день)
      day = day < 10 ? '0' + day : day;
      let month = date.getMonth() + 1;
      let year = date.getFullYear();
      
      return `${year}-${month}-${day}`;
    },
    daysDate() { //создаю масив с датами на пять дней в нужнем формате для фильтрации
      this.days = [];

      const today  = new Date();    
      this.days.push(this.getDayDate(today)); //

      const second = new Date(today);
      second.setDate(second.getDate() + 1);
      this.days.push(this.getDayDate(second));

      const third = new Date(today);
      third.setDate(third.getDate() + 2);
      this.days.push(this.getDayDate(third));

      const fourth = new Date(today);
      fourth.setDate(fourth.getDate() + 3);
      this.days.push(this.getDayDate(fourth));

      const fifth = new Date(today);
      fifth.setDate(fifth.getDate() + 4);
      this.days.push(this.getDayDate(fifth));
    },
    forecastWeather() {
        const self = this;

        this.cityData();  

        setTimeout(function(){  
          fetch('https://api.openweathermap.org/data/2.5/forecast?'
          + 'lat=' + self.city.lat
          + '&lon=' + self.city.lon 
          + '&appid=' + self.key 
          + '&units=metric'
          + '&cnt=40'
          + '&limit=1' 
          ).then(function(response) {
            return response.json()
          })
          .then(function(data) {
            self.forecast = [];

            self.forecast.push(data.list.filter(item => item.dt_txt.indexOf(self.days[0]) > -1)); //фильтрую даные по дате (и времени) и записываю его в масив forecast (40 строк с погодой с датой и временем)
            self.forecast.push(data.list.filter(item => item.dt_txt.indexOf(self.days[1]) > -1 && (item.dt_txt.indexOf('09:00') > -1 || item.dt_txt.indexOf('15:00') > -1 || item.dt_txt.indexOf('21:00') > -1)));
            self.forecast.push(data.list.filter(item => item.dt_txt.indexOf(self.days[2]) > -1 && (item.dt_txt.indexOf('09:00') > -1 || item.dt_txt.indexOf('15:00') > -1 || item.dt_txt.indexOf('21:00') > -1)));
            self.forecast.push(data.list.filter(item => item.dt_txt.indexOf(self.days[3]) > -1 && (item.dt_txt.indexOf('09:00') > -1 || item.dt_txt.indexOf('15:00') > -1 || item.dt_txt.indexOf('21:00') > -1)));
            self.forecast.push(data.list.filter(item => item.dt_txt.indexOf(self.days[4]) > -1 && (item.dt_txt.indexOf('09:00') > -1 || item.dt_txt.indexOf('15:00') > -1 || item.dt_txt.indexOf('21:00') > -1)));
          });          
        }, 1000)
    },
    showDialog() {
      this.dialogVisible = true
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

.app {
  padding: 20px;
  background-image: url(./img/background.webp);
  background-repeat: no-repeat;
  background-size: 100% 100%;
  height: 100vh;
}  
</style>
