<template>
    <div class="weather_сurrent">
        <div class="current_title">
            <h2>{{city.name}}, {{city.country}}</h2>
        </div>
        <div class="current_infotmation">       
            <div class="infotmation_basic">
                <div>
                    <app-icon :class="`large`" :src="`https://openweathermap.org/themes/openweathermap/assets/vendor/owm/img/widgets/${current.icon}.png`"></app-icon>
                </div>
                <div>
                    <div class="basic_temp">{{current.temp}}°C</div>                
                    <div class="basic_desc">{{current.desc}}</div>
                </div>
            </div>
            <div class="infotmation_details">      
                <div class="details_text">   
                    <app-icon :src="`${require('@/img/wind.png')}`"></app-icon>
                    <div class="details_subtitle">{{current.wind}} m/s</div>
                    Wind
                </div>
                <div class="details_text">   
                    <app-icon :src="`${require('@/img/humidity.png')}`"></app-icon>
                    <div class="details_subtitle">{{current.humidity}}%</div>
                    Humidity
                </div>
                <div class="details_text">
                    <app-icon :src="`${require('@/img/thermometer.png')}`"></app-icon>
                    <div class="details_subtitle">Min: {{current.minTemp}} °C</div>
                    <div>Max: {{current.maxTemp}} °C</div>
                </div>
            </div>
        </div>  
    </div>    
</template>

<script>
export default {
    name: 'weather-current',
    props: {
        city: {
            type: Object,
            required: true
        },
        current: {
            type: Object,
            required: true
        }
    }
}
</script>

<style scoped>
.weather_сurrent {
    margin: auto;
    width: 100%;
    max-width: 700px;
}
.weather_сurrent .current_title {
    font-family: 'Courier New', Courier, monospace;
    font-size: 25px;
    color: #fff;
    text-shadow: 3px 6px rgb(0 0 0 / 25%);
}
.weather_сurrent .current_title h2 {
    text-align: center;
}
.weather_сurrent .infotmation_details {
    display: flex;
    justify-content: space-evenly;
    align-items: center;
}
.weather_сurrent .infotmation_basic {
    width: 100%;
    max-width: 500px;
    margin: 0 auto 15px;
    padding-bottom: 40px;
    border-bottom: 1px solid #3d343d;
    text-align: center;
}
.weather_сurrent .basic_temp {
    color: #fff;
    font-family: 'Courier New', Courier, monospace;
    font-size: 50px;
    font-weight: bold;
    margin-bottom: 15px;
    text-shadow: 3px 6px rgb(0 0 0 / 25%);
}
.weather_сurrent .basic_desc {
    font-family: 'Courier New', Courier, monospace;
    font-size: 20px;
    color: #fff;
    text-shadow: 3px 6px rgb(0 0 0 / 15%);
    font-weight: bold;
}
.weather_сurrent .infotmation_details {
    text-align: center;
    margin-bottom: 45px;
}
.weather_сurrent .details_text {
    font-family: 'Courier New', Courier, monospace;
    font-size: 18px;
    color: #fff;
    text-shadow: 3px 6px rgb(0 0 0 / 15%);
    font-weight: bold;
}
.weather_сurrent .details_subtitle {
    padding: 7px;
}


@media screen and (max-width: 767px) {
    .weather_сurrent .details_text {
    font-size: 16px;
    }
    .weather_сurrent .infotmation_details {
    justify-content: space-between;
    margin-bottom: 70px;
    }
    .weather_сurrent .current_title {
    font-size: 20px;
    margin-bottom: 20px;
    }
    .weather_сurrent .basic_temp {
    font-size: 40px;
    margin-top: 15px;
    
    }
}
   
</style>