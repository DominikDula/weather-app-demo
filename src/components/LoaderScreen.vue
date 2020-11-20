<template>
    <div class="loader">
        <div class="spin"></div>
    </div>
</template>

<style lang="scss" scoped>

.loader{
    position: absolute;
    top: 0;
    left: 0;
    z-index: 5;
    width: 100%;
    height: 100%;  
    background: rgba(255, 255, 255, 0.6);

}

.spin{
    width: 40px;
    height: 40px;
    position: fixed;
    transform: translate(-50%,-50%);
    top: 20%;
    left: 50%;
}

.spin:before{
    content: '';
    position: absolute;
    width: 40px;
    height: 40px;
    border-radius: 50%;
    border: 3px solid rgba(8, 206, 196, 0.507);
    border-bottom: 3px solid rgb(10, 43, 190);
    animation: spinner 1s linear infinite;

}

@keyframes spinner{

    0%{
        transform: rotate(0deg)
    }
    100%{
        transform: rotate(360deg)
    }
}

</style>