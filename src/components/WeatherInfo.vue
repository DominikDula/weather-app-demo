<template>
    <div class="weather-info">
        <div class="current flex">
            <div class="weather-icon ">
                <img :src="require('@/assets/demoicon.svg')" alt="logo">
                <h4>Sunny</h4>
            </div>
            <div class="weather-temp">33</div>
            <div class="weather-temp-range">
                <div class="max">30C</div>
                <div class="min">20C</div>
            </div>
        </div>

        <div class="details flex">
            <div class="humidity flex-item">
                <img :src="require('@/assets/demoicon.svg')" alt="logo">
                <h4>49%</h4>
                <p>Humidity</p>
            </div>
            <div class="pressure flex-item">
                <img :src="require('@/assets/demoicon.svg')" alt="logo">
                <h4>1000Mbar</h4>
                <p>Pressure</p>
            </div>
            <div class="wind flex-item">
                <img :src="require('@/assets/demoicon.svg')" alt="logo">
                <h4>23km/h</h4>
                <p>Wind</p>
            </div>
            <div class="sunrise flex-item">
                <img :src="require('@/assets/demoicon.svg')" alt="logo">
                <h4>49%</h4>
                <p>Sunrise</p>
            </div>
            <div class="sunset flex-item">
                <img :src="require('@/assets/demoicon.svg')" alt="logo">
                <h4>1000Mbar</h4>
                <p>Sunset</p>
            </div>
            <div class="daytime flex-item">
                <img :src="require('@/assets/demoicon.svg')" alt="logo">
                <h4>23km/h</h4>
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

        h4{
            font-size: em(18);
            font-weight: 500;
        }
    }

    .weather-temp{
        
            font-size: em(64);
            font-weight: 300;
        
        
    }
    .weather-temp-range{
        .max,.min{
            font-size: em(14);
            font-weight: 300;
            color: $color-light;
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