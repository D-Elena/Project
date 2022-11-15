<template>
    <div class="weather_forecast">
        <div class="days" v-if="days.length > 0">
            <weather-forecast-day 
                v-for="day in days" 
                :day="day"
            />   
        </div>
        <div class="timeslots" v-if="forecast.length > 0">
            <weather-forecast-timeslots 
                v-for="timeslots in forecast" 
                :timeslots="timeslots"
            />   
        </div>
    </div>    
</template>

<script>
import WeatherForecastDay from "@/components/WeatherForecastDay";
import WeatherForecastTimeslots from "@/components/WeatherForecastTimeslots";

export default {
    name: 'weather-forecast',
    components: {
        WeatherForecastDay, WeatherForecastTimeslots
    },
    props: {
        city: {
            type: Object,
            required: true
        },
        forecast: {
            type: Object,
            required: true
        },
        days: {
            type: Object,
            required: true
        }
    }
}
</script>

<style scoped>
.weather_forecast {    
    display: flex;
    margin: auto;
    border-radius: 15px;
    overflow: hidden;
    border: 5px solid #fff;
    background-color: #fff;
}
.days {
    margin-right: 4px;
}

@media screen and (max-width: 767px) {
    .weather_forecast {    
    border: 3px solid #fff;
    }
    .days {
    margin-right: 2px;
    }
}
</style>