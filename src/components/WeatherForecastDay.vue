<template>
    <div class="day">{{day}}</div>    
</template>

<script>
export default {
    name: 'weather-forecast-day',
    props: {
        day: {
            type: String,
            required: true
        }
    }
}
</script>

<style scoped>
.day {
    font-family:Verdana, Geneva, Tahoma, sans-serif;
    font-size: 15px;
    padding: 0 15px;
    height: 100%;
    max-height: 115px;
    width: 100%;
    max-width: 150px;
    background-color: rgb(227, 234, 238);
    display: flex;
    flex-wrap: wrap;
    align-items: center;
    justify-content: center;
}
.day + .day {
    margin-top: 7px;
}

@media screen and (max-width: 767px) {
    .day {
    font-size: 11px;
    padding: 0 10px;
    max-height: 100px;
    }
}
</style>