<script>

export default {
    props: {
        weather: {
            type: Object,
        },
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
        },
    }
}
</script>

<template>
  <div v-if="weather" class="infoSun">
            <div class="centerHeader">
                <h2> Солнце </h2>
            </div>

            <div class="centerText">
                    <h2> Восход  — {{ timeSunrise }} </h2>
                    <h2> Заход  — {{ timeSunset }} </h2>
            </div>   

            <div class="imgSun">
                <img src="@/assets/sun2.png" class="scale-img">
            </div> 

        </div>
    
</template>

<style scoped>
.scale-img {
    width: 40%; 
    height: auto;
}
.infoSun {
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
.imgSun {
    grid-area: imgSun;
    display: flex;
    flex-direction: column;
    align-items: center; 
    justify-content: center;
    height: 100%;
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