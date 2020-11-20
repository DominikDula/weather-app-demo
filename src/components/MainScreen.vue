<template>
    <main class="container">
        <div class="bg"></div>
        <div class="content">
            <city-info @city="ChangeCity" :info="dayinfo"/>
            <weather-info :daily="results"/>
            <next-days :next="results"/>
        </div>
        <loader-screen v-if="loader" />
    </main>
</template>

<script>
import CityInfo from "@/components/CityInfo.vue";
import WeatherInfo from "@/components/WeatherInfo.vue";
import NextDays from "@/components/NextDays.vue";
import LoaderScreen from "@/components/LoaderScreen.vue";
    export default {
        data() {
            return {
                city:'Košice',
                lon:'',
                lat:'',
                dayinfo:'',
                results:'',
                minmax:{},
                loader:false,
                

            }
        },
        components: {
            CityInfo,
            WeatherInfo,
            NextDays,
            LoaderScreen
        },
        created () {
            this.GetCurrentWeather()
        },
                mounted () {
            this.$root.$on('loader',  data => {
                this.loader = data
            })
        },
        methods: {
           async GetCurrentWeather() {
               this.loader = true
               try{
                   let response = await fetch(`https://api.openweathermap.org/data/2.5/forecast?q=${this.city}&units=metric&appid=37fa2633ce3326fbb19b469d4f34d00e`)
                   let data = await response.json()
                   this.dayinfo = data.city
                   console.log(data);
                   this.lon = data.city.coord.lon
                   this.lat = data.city.coord.lat
                   let dailyresponse = await fetch(`https://api.openweathermap.org/data/2.5/onecall?lat=${this.lat}&lon=${this.lon}&units=metric&exclude=minutely,hourly,alerts&appid=37fa2633ce3326fbb19b469d4f34d00e`)
                   let dailydata = await dailyresponse.json()
                   this.results = dailydata
                   console.log(dailydata);
                   this.loader = false
                   
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
    overflow: scroll;
    overflow-x: hidden;

}

.bg{
    width: 100%;
    height: rem(300);
    background-image: url(../assets/background.png);
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