<template>
    <div class="city-info">
        <div class="day-info"> <p>Day,Date,Time</p> </div>
        <div class="city-name">City,Country</div>
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

.city-info{
    width: 100%;
    // padding: 0.5em 1em;
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
        font-weight: 500;
        padding: 0.7em 1em;
        width: 40%;
        color: $color-city;
        background: rgba(13, 159, 234, 0.08);
        border-radius: 0 0 0 20px ;
    }
}

</style>