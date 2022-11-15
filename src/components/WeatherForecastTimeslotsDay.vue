<template>
    <div class="day">
        <h4>{{day.dt_txt.match(/\d\d:00/g)[0]}}</h4>
        <div class="wrapper">
            <app-icon :class="`small`" :src="`https://openweathermap.org/themes/openweathermap/assets/vendor/owm/img/widgets/${day.weather[0].icon}.png`"></app-icon>            
            <div>
                <div>{{day.main.temp}} °C</div>
                <div>{{day.weather[0].description}}</div>
            </div>
        </div>
        <div>Wind: {{day.wind.speed}} m/s</div>
        <div>Humidity: {{day.main.humidity}}%</div>
    </div>    
</template>

<script>
export default {
    name: 'weather-forecast-timeslots-day',
    props: {
        day: {
            type: Object,
            required: true
        }
    }
}
</script>

<style scoped>
.day {
    padding: 5px 0;
    height: 115px;
    width: 210px;
    background-color: rgb(237, 241, 244);
    text-align: center;
}
.day h4 {
    text-align: center;
    margin-bottom: 5px;
}
.day + .day {
    margin-left: 4px;
}
.wrapper {
    display: flex;
    margin-bottom: 10px;
    align-items: center;
    justify-content: center;
}

@media screen and (max-width: 767px) {
    .day {
    height: 100px;
    width: 115px;
    text-align: left;
    padding: 5px 5px;
    } 

    .day + .day {
    margin-left: 2px;
    }

    .wrapper {
    justify-content: flex-start;
}
}
</style>