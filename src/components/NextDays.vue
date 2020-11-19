<template>
    <div v-if="next" class="next-days flex">
        <div class="daily flex-item">
            <img :src="require(`@/assets/icons/${nextday.day1.icon}.svg`)" alt="logo">
            <h4>{{timeFormat(nextday.day1.day)}}</h4>
            <div class="min-max">
                <div class="next-max">{{nextday.day1.max}}</div> 
                <div class="next-min">{{nextday.day1.min}}</div>
            </div>
        </div>
        <div class="daily flex-item">
            <img :src="require(`@/assets/icons/${nextday.day2.icon}.svg`)" alt="logo">
            <h4>{{timeFormat(nextday.day2.day)}}</h4>
            <div class="min-max">
                <div class="next-max">{{nextday.day2.max}}</div> 
                <div class="next-min">{{nextday.day2.min}}</div>
            </div>
        </div>
        <div class="daily flex-item">
            <img :src="require(`@/assets/icons/${nextday.day3.icon}.svg`)" alt="logo">
            <h4>{{timeFormat(nextday.day3.day)}}</h4>
            <div class="min-max">
                <div class="next-max">{{nextday.day3.max}}</div> 
                <div class="next-min">{{nextday.day3.min}}</div>
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
        props: ['next'],
        methods: {
            timeFormat(timestamp){
                function dayOfWeekAsString(dayIndex) {
                    return ["Sun","Mon","Tues","Wed","thurs","Fri","Sat"][dayIndex] || '';
                }
                let time = new Date(timestamp * 1000);
                let date = time.getDate();
                let day =time.getDay();
                let formated = dayOfWeekAsString(day)+','+ date;

                return formated;
            },
        },
        computed: {
            nextday() {
                return {
                    day1 : {
                        day : this.next.daily[1].dt,
                        max : Math.round(this.next.daily[1].temp.max),
                        min : Math.round(this.next.daily[1].temp.min),
                        icon : this.next.daily[1].weather[0].icon,
                    },
                    day2 : {
                        day : this.next.daily[2].dt,
                        max : Math.round(this.next.daily[2].temp.max),
                        min : Math.round(this.next.daily[2].temp.min),
                        icon : this.next.daily[2].weather[0].icon,
                    },
                    day3 : {
                        day : this.next.daily[3].dt,
                        max : Math.round(this.next.daily[3].temp.max),
                        min : Math.round(this.next.daily[3].temp.min),
                        icon : this.next.daily[3].weather[0].icon,
                    },
                } 
            }
        },
    }
</script>

<style lang="scss" scoped>

.next-days{
    .daily{
        box-shadow: 0px 8px 24px rgba(0, 0, 0, 0.1);
        border-radius: 16px;
        height: 95px;
        margin: 0 0.7em;

        img{
            width: 24px;
            height: 50px;
        }
        h4{
            font-weight: 500;
        }

        .min-max{
            width: 100px;
            display: flex;
            justify-content: center;
            margin-top: 2px;
        }

        .next-max,.next-min{
            position: relative;
            font-size: em(8);
            color: $color-very-light;
            font-weight: 500;

            &::before{
                position: absolute;
                content: '';
                width: 7px;
                height: 7px;
                top: 1.5px;
                right: -8px;
                background: url(../assets/icons/celsiumlite.svg);
                background-repeat: no-repeat;
                background-size: contain;
        }
        }
        .next-max{
           margin: 0px 21px;
        }
        .next-min{
           margin:  0 36px 0 0;
        }
        .next-max::after{
                position: absolute;
                content: '';
                width: 6px;
                height: 6px;
                top: 2.3px;
                right: -16px;
                background: url(../assets/icons/vectormax.svg);
                background-repeat: no-repeat;
                background-size: contain;            
        }
        .next-min::after{
                position: absolute;
                content: '';
                width: 6px;
                height: 6px;
                top: 2.3px;
                right: -16px;
                background: url(../assets/icons/vectormin.svg);
                background-repeat: no-repeat;
                background-size: contain;            
        }
    }
}

</style>