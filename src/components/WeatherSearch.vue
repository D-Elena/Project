<template>
    <div class="weather_search">
        <input :value="modelValue" @input="updateCityName" type="text" class="search_text">
    </div>    
</template>

<script>
export default {    
    name: 'weather-search',
    props: {
        modelValue: [String, Number]
    },
    methods: {
        updateCityName(event) {
            this.$emit('update:modelValue', event.target.value)
            this.$emit('update')
        }
    }
}
</script>

<style scoped>
.weather_search {
    width: 100%;
    max-width: 700px;
    margin: 30px auto;
}
.weather_search .search_text {
    font-family: 'Courier New', Courier, monospace;
    font-size: 20px;
    color: #282828;
}
.weather_search input {
    width: 100%;
    padding: 15px 20px;
    color: #3d343d;
    font-size: 20px;
    border: none;
    background: none;
    outline: none;
    appearance: none;
    box-shadow: 0px 0px 8px rgba(0,0,0,.25);
    background-color: rgba(255, 255, 255, .75);
    border-radius: 0 15px 0 15px;
    transition: all .4s ease;
}
.weather_search input:focus {
    box-shadow: 0px 0px 16px rgba(0, 0, 0, .35);
    background-color: rgba(255, 255, 255, .85);
    border-radius: 16px 0 16px 0;
}

@media screen and (max-width: 767px) {
    .weather_search {
    margin: 40px auto 50px;
    }
}
</style>