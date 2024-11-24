<template>
<div v-if="temp != null" class="temp-info">
    <div class="btn-change"> 
        <button class="btn-temp" @click="buttonEventName"> {{ buttonName }} </button> 
    </div>
    <div> 
        <h2> {{ showTemp }}</h2>
        <h2> {{ showFeelsLike }}</h2>
        <h2> {{ showMinTemp }}</h2>
        <h2> {{ showMaxTemp }}</h2>
    </div>
</div>    
</template>

<script>
export default {
    props: {
        temp: {
            type: Object,
        },
        getWeatherInfo:{
            type:Function
        },
        getFTemp: {
            type:Function
        },
        isButtonOneActive: {
            type: Boolean
        }
    },
    computed: {
        showTemp() {
            return "Температура: " + this.temp.main.temp 
        },
        showFeelsLike() {
            return "Ощущается как: " + this.temp.main.feels_like
        },
        showMinTemp() {
            return "Минимальная температура: " + this.temp.main.temp_min
        },
        showMaxTemp() {
            return "Максимальная температура: " + this.temp.main.temp_max
        },
        buttonName() {
            return this.isButtonOneActive ? "Перевести в °F" : "Перевести в °C"
        }
    },
    methods: {
        buttonEventName() {
           this.isButtonOneActive ? this.getFTemp() : this.getWeatherInfo()
        }
    }
}
</script>

<style scoped>
.temp-info {
    grid-area: content1; 
    display: grid;
    box-shadow: 0px 2px 40px #00000014;
    align-content: center; 
    justify-content: center;
    font-weight: 700;
    border-radius: 10px;
    grid-row: span 2;
    padding: 30px;
    margin-left: 50px;
}
.btn-temp {
    border-radius: 10px;
    border: 2px solid #0d0b87;
    padding: 10px 15px;
    margin-left: 20px;
    cursor: pointer;
    background: #0d0b87;
    color: #fff;
    transform: none !important;
}
.btn-change {
    position: absolute;
}
</style>