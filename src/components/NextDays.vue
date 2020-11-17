<template>
    <div class="next-days flex">
        <div class="daily flex-item">
            <img :src="require('@/assets/demoicon.svg')" alt="logo">
            <h4>Thu,09</h4>
            <p>35|26</p>
        </div>
        <div class="daily flex-item">
            <img :src="require('@/assets/demoicon.svg')" alt="logo">
            <h4>Thu,09</h4>
            <p>35|26</p>
        </div>
        <div class="daily flex-item">
            <img :src="require('@/assets/demoicon.svg')" alt="logo">
            <h4>Thu,09</h4>
            <p>35|26</p>
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

.next-days{
    .daily{
        box-shadow: 0px 8px 24px rgba(0, 0, 0, 0.1);
        border-radius: 16px;
        height: 95px;
        margin: 1em 0.7em;
    }
}

</style>