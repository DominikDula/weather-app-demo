<template>
    <main class="container">
        <div class="bg"></div>
        <div class="content">
            <city-info @city="ChangeCity" :info="dayinfo"/>
            <weather-info :daily="results"/>
            <next-days/>
        </div>
    </main>
</template>

<script>
import CityInfo from "@/components/CityInfo.vue";
import WeatherInfo from "@/components/WeatherInfo.vue";
import NextDays from "@/components/NextDays.vue";
    export default {
        data() {
            return {
                city:'Košice',
                lon:'',
                lat:'',
                results:'',
                dayinfo:''
            }
        },
        components: {
            CityInfo,
            WeatherInfo,
            NextDays,
        },
        created () {
            this.GetCurrentWeather();
        },
        methods: {
           async GetCurrentWeather() {
               try{
                   let response = await fetch(`https://api.openweathermap.org/data/2.5/forecast?q=${this.city}&units=metric&appid=37fa2633ce3326fbb19b469d4f34d00e`)
                   let data = await response.json()
                   this.dayinfo = data.city
                   console.log(data);
                   this.lon = data.city.coord.lon
                   this.lat = data.city.coord.lat
                   let dailyresponse = await fetch(`https://api.openweathermap.org/data/2.5/onecall?lat=${this.lat}&lon=${this.lon}&units=metric&exclude=minutely,hourly,alerts&appid=37fa2633ce3326fbb19b469d4f34d00e`)
                   let dailydata = await dailyresponse.json()
                   this.results = dailydata.current
                   console.log(dailydata);
                   
                }
                catch (error) {
                    console.log(error);
                }
                
            },

            ChangeCity(data){
                this.city = data
                this.GetCurrentWeather()
            
            }

        },
    }
</script>

<style lang="scss" scoped>



.container{
    min-width: rem(375);
    min-height: rem(812);
    position: relative;
    // border: 1px solid black;

}

.bg{
    width: 100%;
    height: rem(300);
    background-image: url(../assets/background.png);
    background-position: center center;
    background-size: cover;
    background-repeat: no-repeat;
}

.content{
    background: $bg-main;
    width: 100%;
    height: rem(531);
    margin-top: -21px;
    border-radius: 40px 40px 0 0;
    box-shadow: 0px -16px 40px rgba(0, 0, 0, 0.2);
    overflow: hidden;
}






</style>