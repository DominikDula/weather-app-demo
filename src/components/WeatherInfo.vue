<template>
    <div v-if="daily" class="weather-info">
        <div class="current flex">
            <div class="weather-icon ">
                <img :src="require(`@/assets/icons/${weather.icon}.svg`)" alt="logo">
                <h4 class="capitalize">{{weather.description}}</h4>
            </div>
            <div class="weather-temp"> {{weather.temp}} </div>
            <div class="weather-temp-range">
                <div class="max">{{weather.max}}</div>
                <div class="min">{{weather.min}}</div>
            </div>
        </div>

        <div class="details flex">
            <div class="humidity flex-item">
                <img :src="require('@/assets/icons/humidity.svg')" alt="logo">
                <h4> {{weather.humidity}}% </h4>
                <p>Humidity</p>
            </div>
            <div class="pressure flex-item">
                <img :src="require('@/assets/icons/barometer.svg')" alt="logo">
                <h4> {{weather.pressure}}mBar </h4>
                <p>Pressure</p>
            </div>
            <div class="wind flex-item">
                <img :src="require('@/assets/icons/wind.svg')" alt="logo">
                <h4> {{weather.wind}}km/h </h4>
                <p>Wind</p>
            </div>
            <div class="sunrise flex-item">
                <img :src="require('@/assets/icons/sunrise.svg')" alt="logo">
                <h4> {{hoursFormat(weather.sunrise)}} </h4>
                <p>Sunrise</p>
            </div>
            <div class="sunset flex-item">
                <img :src="require('@/assets/icons/sunset.svg')" alt="logo">
                <h4> {{hoursFormat(weather.sunset)}} </h4>
                <p>Sunset</p>
            </div>
            <div class="daytime flex-item">
                <img :src="require('@/assets/icons/daytime.svg')" alt="logo">
                <h4> {{hoursFormat(weather.sunset,weather.sunrise)}} </h4>
                <p>Daytime</p>
            </div>
        </div>

    </div>
</template>

<script>
    export default {
        data() {
            return {
                
            }
        },
        props: ['daily'],
        methods: {
            hoursFormat(timestamp,optionaltimestamp = 0){
                let date = new Date((timestamp - optionaltimestamp) * 1000);
                let hours =date.getHours();
                let mins =('0'+date.getMinutes()).slice(-2);
                let time = hours+':'+mins;
                
                return time;
            },
        },
        computed: {
            weather() {
                return {
                    description : this.daily.current.weather[0].main,
                    temp : Math.round(this.daily.current.temp ),
                    humidity : this.daily.current.humidity,
                    pressure : this.daily.current.pressure,
                    wind : this.daily.current.wind_speed,
                    sunrise : this.daily.current.sunrise,
                    sunset : this.daily.current.sunset,
                    icon : this.daily.current.weather[0].icon,
                    max: Math.round(this.daily.daily[0].temp.max),
                    min: Math.round(this.daily.daily[0].temp.min),

                } 
                
               
            }
        },
    }
</script>

<style lang="scss" scoped>

.weather-info{
    margin-top: 1em;
}


.current{
    .weather-icon,.weather-temp,.weather-temp-range{
        display: flex;
        flex-direction: column;
        align-items: center;
        color: $color-medium;
        width:33.3333%;
  
    
    }

    .weather-icon{
        display: flex;
        flex-direction: column;
        
        img{
            width: 40px;
        }

        h4{
            font-size: em(18);
            font-weight: 500;
        }
    }

    .weather-temp{
            position: relative;
            font-size: em(64);
            font-weight: 300;
        
        &::before{
            position: absolute;
            content: '';
            width: 26px;
            height: 26px;
            top: 15px;
            right: 5px;
            background: url(../assets/icons/celsiumlite.svg);
            background-repeat: no-repeat;
            background-size: contain;
        }
        
    }
    .weather-temp-range{
        .max,.min{
            position: relative;
            font-size: em(14);
            font-weight: 300;
            color: $color-light;

            &::before{
                position: absolute;
                content: '';
                width: 12px;
                height: 12px;
                top: 3px;
                right: -12px;
                background: url(../assets/icons/celsiumlite.svg);
                background-repeat: no-repeat;
                background-size: contain;
        }
        }
        .max::after{
                position: absolute;
                content: '';
                width: 6px;
                height: 6px;
                top: 4px;
                right: -20px;
                background: url(../assets/icons/vectormax.svg);
                background-repeat: no-repeat;
                background-size: contain;
        }
        .min::after{
                position: absolute;
                content: '';
                width: 6px;
                height: 6px;
                bottom: 4px;
                right: -20px;
                background: url(../assets/icons/vectormin.svg);
                background-repeat: no-repeat;
                background-size: contain;
        }
        
    }

}

.details{
    flex-wrap: wrap;

    h4{
        font-weight: 500;
        color: $color-medium;
        margin: 4px 0;
    }
    p{
        font-size: em(8);
        color: $color-very-light;
        font-weight: 500;
    }


    
}

</style>