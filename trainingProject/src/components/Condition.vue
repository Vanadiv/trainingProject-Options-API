<script>
export default {
    props: {
        weather: {
            type: Object,
        }
    },
    computed: {
        showConditions() {
            if(this.weather.rain == null && this.weather.snow == null) {
                return "Осадков нет"
            } else if(this.weather.rain == null) {
                return `Снег - в среднем ${this.weather.snow?.['1h']} см снега за 1 час`
            } else {
                return `Дождь - в среднем ${this.weather.rain?.['1h']} см дождя за 1 час` 
            }
        },
        showImage() {           
            if(this.weather.rain == null && this.weather.snow == null) {
                return 'background:none;'
            } else if(this.weather.rain == null) {
                return  'background: url(src/assets/snow.png);';
            } else {
                return 'background: url(src/assets/rain.jpg); color: #fff; font-weight: 800';
            }
        }
    }
}
</script>

<template>
<div v-if="weather" class="infoConditions" :style="showImage">
    <div class="centerHeader"> 
        <h2> Осадки </h2>
    </div>
    <div class="centerText">
        <h2> {{ showConditions }} </h2>
    </div>
</div> 
</template>

<style scoped>
.infoConditions {
    grid-area: content4; 
    box-shadow: 0px 2px 40px #00000014;
    border-radius: 10px;
    padding: 30px;
    grid-template-areas: "header" "text";
    grid-template-columns: 1fr;
    grid-template-rows: auto 1fr;
    gap: 15px;
    margin-right: 50px;
}
.centerText {
    grid-area: text;
    display: flex;
    flex-direction: column;
    align-items: center; 
    justify-content: center;
    height: 100%;
}
.centerHeader {
    grid-area: header;
}

</style>