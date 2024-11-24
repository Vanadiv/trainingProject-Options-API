<template>
<div class="wrap"> 
    <div class="city-input">  
        <h1> Погодное приложение</h1>
        <input type="text" v-model="city" placeholder="Введите название города" @keydown.enter="getWeatherInfo">
        <button :disabled="city ==''" @click="getWeatherInfo"> {{ buttonName }} </button>
    </div>

    <div class="city-name">
        <template v-if="weather != null">
            <img src="@/assets/map.svg" />
            <h1> {{ showCityName }} </h1>
        </template>
        <p v-else> {{ error }}</p>
    </div>   

    <Temperature :temp="weather" :getWeatherInfo="getWeatherInfo" :getFTemp="getFTemp" :isButtonOneActive="isButtonOneActive" />

    <Sun :weather="weather" />

    <Condition :weather="weather"/>
        
</div>
</template>

<script>
import axios from 'axios';
import Temperature from './components/Temperature.vue';
import Sun from './components/Sun.vue';
import Condition from './components/Condition.vue';

export default {
    components: {
    Temperature,
    Sun,
    Condition
    },
    data() {
        return {
            city: "",
            error: "",
            weather: null,
            backgroundColor: "",
            isButtonOneActive: true,
            conditions: "",
            sunset: "",
            sunrise: ""
        }
    },
    methods: {
        getWeatherInfo() {
            if(this.city.trim().length < 2) {
                this.error = "Введите более одного символа"
                this.weather = null;
                return false
            }
            this.error = ""
            axios.get(`https://api.openweathermap.org/data/2.5/weather?q=${this.city}&lang=ru&units=metric&appid=9bc72beca7fd1dafc25b81e5fb32b98e`)
            .then (res => (this.weather = res.data))
            .catch(err => {
            if (err.response && err.response.status === 404) {
                this.error = "Такого города нет";
                this.weather = null;
                return;
            } 
            this.error = "Произошла ошибĸа. Попробуйте снова.";
            this.weather = null
            })
            this.isButtonOneActive = true
        },
        getFTemp() {
            axios.get(`https://api.openweathermap.org/data/2.5/weather?q=${this.city}&lang=ru&appid=9bc72beca7fd1dafc25b81e5fb32b98e`)
            .then (res => (this.weather = res.data))
            this.isButtonOneActive = false
        }
        
    },
    computed: {
        showCityName() {
            return this.weather.name
        },
        buttonName() {
            return this.city =='' ? 'Введите название' : 'Узнать погоду'
        }
    }
}

</script>

<style>
.wrap {
    display: grid;
    gap: 30px 30px;
    grid-template-areas: "header header" "city city" "content1 content2" "content3 content4";
    grid-template-columns: 0.5fr 0.5fr;
    grid-template-rows: auto auto 1fr 1fr;
    width: 100vw;
    height: 70vh;
    background: #FDF5E6;
    color: #292733;
    text-align: center;
    align-content: center;
    margin: 0;
    padding: 50px 0;
}
.wrap input {
    margin-top: 30px;
    padding: 5px 30px 5px 8px;
    font-size: 14px;
    background: transparent;
    border: 0;
    border-bottom: 1px solid #292733;
    outline: none;
}
.wrap input:focus {
    border-bottom: 2px solid #292733;
}
.wrap button:disabled {
    border-radius: 10px;
    border: 2px solid #a0a0a5;
    padding: 10px 15px;
    margin-left: 20px;
    cursor: default;
    background: #a0a0a5;
    color: #fff;
    transform: none !important;
}
.wrap button {
    border-radius: 10px;
    border: 2px solid #0d0b87;
    padding: 10px 15px;
    margin-left: 20px;
    cursor: pointer;
    transition: transfor, 500ms ease;
    background: #0d0b87;
    color: #fff;
}
.wrap button:hover {
    transform: scale(1.1) translateY(-5px);
}
.city-name {
    display: flex;
    grid-area: city;  
    align-items: center; 
    justify-content: center;
    border-radius: 10px;
}
.city-input {
    grid-area: header;
}
</style>