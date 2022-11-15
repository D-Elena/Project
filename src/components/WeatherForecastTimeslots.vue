<template>
    <div class="timeslots" v-if="timeslots.length > 0">
        <weather-forecast-timeslots-day 
            v-for="day in timeslots" 
            :day="day"
        />   
    </div>    
</template>

<script>
import WeatherForecastTimeslotsDay from "@/components/WeatherForecastTimeslotsDay";

export default {
    name: 'weather-forecast-timeslots',
    components: {
        WeatherForecastTimeslotsDay
    },
    props: {
        timeslots: {
            type: Array,
            required: true
        }
    }
}
</script>

<style scoped>
.timeslots {
    display: flex;
    font-family: Verdana, Geneva, Tahoma, sans-serif;
    font-size: 12px;
}
.timeslots + .timeslots {
    margin-top: 7px;
}

@media screen and (max-width: 767px) {
    .timeslots {
    font-size: 9px;
}
}
</style>