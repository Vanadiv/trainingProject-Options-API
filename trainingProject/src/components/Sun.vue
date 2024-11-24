<template>
<div v-if="weather != null" class="sun-info">
    <div class="center-header">
        <h2> Солнце </h2>
    </div>

    <div class="center-text">
        <h2> Восход  — {{ timeSunrise }} </h2>
        <h2> Заход  — {{ timeSunset }} </h2>
    </div>   

    <div class="sun-img">
        <img src="@/assets/sun2.png" class="scale-img">
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
    data() {
        return {
            sunset: "",
            sunrise: ""
        }
    },
    computed: {
        timeSunset() {
            this.sunset = new Date(this.weather.sys.sunset * 1000);
            return this.sunset.toLocaleString('ru-RU', {
                hour: '2-digit',
                minute: '2-digit'
            })
        },
        timeSunrise() {
           this.sunrise = new Date(this.weather.sys.sunrise * 1000);
           return this.sunrise.toLocaleString('ru-RU', {
                hour: '2-digit',
                minute: '2-digit'
            })
        }
    }
}
</script>

<style scoped>
.scale-img {
    width: 40%; 
    height: auto;
}
.sun-info {
    grid-area: content2; 
    display: grid;
    box-shadow: 0px 2px 40px #00000014;
    border-radius: 10px;
    padding: 30px;
    grid-template-areas: "header header" "text imgSun";
    grid-template-columns: 1fr 0.5fr;
    grid-template-rows: auto 1fr;
    gap: 15px;
    margin-right: 50px;
}
.sun-img {
    grid-area: imgSun;
    display: flex;
    flex-direction: column;
    align-items: center; 
    justify-content: center;
    height: 100%;
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