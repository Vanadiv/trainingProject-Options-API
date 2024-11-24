<template>
<div v-if="weather != null" class="conditions-info" :style="showImage">
    <div class="center-header"> 
        <h2> Осадки </h2>
    </div>
    <div class="center-text">
        <h2> {{ showConditions }} </h2>
    </div>
</div> 
</template>

<script>
export default {
    props: {
        weather: {
            type: Object,
        }
    },
    computed: {
        showConditions() {
            if(this.weather.rain != null) {
                return `Дождь - в среднем ${this.weather.rain?.['1h']} см дождя за 1 час`
            } 
            if(this.weather.snow != null) {
                return `Снег - в среднем ${this.weather.snow?.['1h']} см снега за 1 час`
            } 
            return "Осадков нет"
        },
        showImage() {           
            if(this.weather.rain != null) {
                return 'background: url(src/assets/rain.jpg); color: #fff; font-weight: 800'
            }
            if(this.weather.snow != null) {
                return  'background: url(src/assets/snow.png);';
            }
            return 'background:none;'
            }
        }
    }
</script>

<style scoped>
.conditions-info {
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
.center-text {
    grid-area: text;
    display: flex;
    flex-direction: column;
    align-items: center; 
    justify-content: center;
    height: 100%;
}
.center-header {
    grid-area: header;
}
</style>