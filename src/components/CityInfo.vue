<template>
<div>
    <div v-if="info" class="city-info">
        <div class="day-info"> <p> {{timeFormat(info.sunrise)}} | {{time}} </p> </div>
        <div @click="toggleSearch()" class="city-name">{{info.name}},{{info.country}}</div>
    </div>
    <transition name="fade">
        <div v-if="show" class="search-city">
            <div class="search-location">Location</div>
            <div class="search-input">
                <input ref="input" v-model="searchquery" type="text" placeholder="Search city...">
            </div>
            <div class="suggested-cities">
                <ul>
                    <li>
                        <a @click="citySearch(city)" href="#" v-for="(city,index) in FilterCities" :key="index+1">{{ city }}</a>
                    </li>
                </ul>
            </div>
        </div>
    </transition>
</div>

</template>

<script>
import { setInterval } from 'timers';
    export default {
        data() {
            return {
                time:'',
                show:false,
                cities:[],
                searchquery:'',
            }
        },
        created () {
            this.GetSlovakiaCities()   
            
                   
        },
        updated () {
            if(this.show){
                this.$refs.input.focus()
            }
            this.currentTime()
            setInterval(this.currentTime,10000)
        },
        props: ['info'],
        methods: {
            async GetSlovakiaCities(){
                //population >1000//
                try{
                    let response = await fetch(`https://public.opendatasoft.com/api/records/1.0/search/?dataset=geonames-all-cities-with-a-population-1000&q=slovakia&rows=160&facet=timezone&facet=country&exclude.name=Bratislava+-+Vajnory`)
                    let data = await response.json()
                    data.records.map(city => {
                        this.cities.push(city.fields.name)
                    });
                    
                }
                catch(error){
                    console.log(error);
                    
                }
            },
            timeFormat(timestamp){
                function dayOfWeekAsString(dayIndex) {
                    return ["Sunday", "Monday", "Tuesday", "Wednesday", "Thursday", "Friday", "Saturday"][dayIndex] || '';
                }
            
                let time = new Date(timestamp * 1000);
                let months = ["Jan", "Feb", "Mar", "Apr", "May", "Jun", "Jul","Aug", "Sep", "Oct", "Nov", "Dec"];
                let month = months[time.getMonth()];
                let date = time.getDate();
                let day =time.getDay();
                let year =time.getFullYear();
                let formated = dayOfWeekAsString(day)+','+ date + ' ' + month +' ' +year;

                return formated;
            },
            currentTime(){
                let date = new Date();
                let hours =date.getHours();
                let mins =('0'+date.getMinutes()).slice(-2);
                this.time = hours+':'+mins;
            },
            toggleSearch(){
                this.show = !this.show
            },
            citySearch(city){
                this.$emit('city',city.split(' ').join('+'))
                this.$root.$emit('loader',true)
                this.show = false
                this.searchquery = ''
            },
        },
        computed: {
            FilterCities() {
                // normalize = get rid of the diacritics  //
                let filterArray = this.cities
                    .filter(city => city.normalize("NFD")
                    .replace(/[\u0300-\u036f]/g, "").toLowerCase()
                    .includes(this.searchquery.normalize("NFD")
                    .replace(/[\u0300-\u036f]/g, "").toLowerCase())) 

                return  [...new Set(filterArray.sort())]

               
                
            }
        },

    }
</script>

<style lang="scss" scoped>

.city-info{
    width: 100%;
    display: flex;
    justify-content: space-between;
    align-items: flex-end;

    .day-info{
        font-size: em(14);
        color: $color-very-light;
        font-weight: 400;
        padding: 0.7em 1em;
        width: 60%;
    }
    .city-name{
        position: relative;
        font-weight: 500;
        padding: 0.7em 1em;
        width: 40%;
        color: $color-city;
        background: rgba(13, 159, 234, 0.08);
        border-radius: 0 0 0 20px ;
        cursor: pointer;

        &::before{
            position: absolute;
            content: '';
            width: 15px;
            height: 15px;
            top: 12px;
            right: 10px;
            background: url(../assets/icons/pin1.svg);
            background-repeat: no-repeat;
            background-size: contain;
        }
    }
}

.search-city{
    position: absolute;
    top: 28px;
    left: 0;
    width: 100%;
    min-height: 100%;
    background: $bg-main;
    border-radius: 25px 25px 0 0;
    box-shadow: 0px -16px 40px rgba(0, 0, 0, 0.2);
    z-index: 1;

    .search-location{
        display: flex;
        justify-content: center;
        padding: 28px 0;
    }

    .search-input{
        display: flex;
        justify-content: center;
        position: relative;
        input{
        width: 86%;
        height: 40px;
        border: none;
        outline: none;
        background: $bg-search;
        border-radius: 4px;
        text-indent: 1.5em;
        font-weight: 500;
        font-style: italic;
        margin: 0 0px 2em;
        }

        &::before{
            position: absolute;
            content: '';
            width: 15px;
            height: 15px;
            top: 12px;
            right: 30px;
            background: url(../assets/icons/pin2.svg);
            background-repeat: no-repeat;
            background-size: contain;
            z-index: 1;
        }
    }
    .suggested-cities{
        ul{
            display: flex;
            justify-content: center;
            padding: 20px 0;
        }
        li{
            display: flex;
            flex-direction: column;
        }
        a{
            text-decoration: none;
            color: $color-medium;
            margin: 6px 0;
            font-weight: 400;
        }
    }
}

</style>