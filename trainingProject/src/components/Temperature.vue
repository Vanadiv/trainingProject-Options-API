<script>
export default {
    props: {
        temp: {
            type: Object,
        },
        get_data:{
            type:Function
        },
        getFtemp: {
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
        showFeelsLke() {
            return "Ощущается как: " + this.temp.main.feels_like
        },
        showMinTemp() {
            return "Минимальная температура: " + this.temp.main.temp_min
        },
        showMaxTemp() {
            return "Максимальная температура: " + this.temp.main.temp_max
        },
    }
}

</script>

<template>
        <div v-if="temp" class="infoTemp">
            <div class="changeBtn"> 
                <button class="btnTemp" @click="getFtemp" v-if="isButtonOneActive"> Перевести в °F </button> 
                <button class="btnTemp" @click="get_data" v-if="!isButtonOneActive"> Перевести в °C </button>
            </div>

            <div> 
                <h2> {{ showTemp }}</h2>
                <h2> {{ showFeelsLke }}</h2>
                <h2> {{ showMinTemp }}</h2>
                <h2> {{ showMaxTemp }}</h2>
            </div>
        </div>

    
</template>

<style scoped>
.infoTemp {
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

.btnTemp {
    border-radius: 10px;
    border: 2px solid #0d0b87;
    padding: 10px 15px;
    margin-left: 20px;
    cursor: pointer;
    background: #0d0b87;
    color: #fff;
    transform: none !important;
}

.changeBtn {
    position: absolute;
}
</style>