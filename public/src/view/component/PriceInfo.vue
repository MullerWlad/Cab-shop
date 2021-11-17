<template>
    <div class="info" v-if="openPriceInfo" @click="close()">
        <p>{{priceInfo}}</p>
    </div>
</template>
<script>
    export default {
        props: ["openPriceInfo", "priceInfo"],
        methods: {
            close() {
                this.$emit("closingPriceInfo")
            }
        }
    }
</script>
<style scoped>
.info {
    width: 900px;
    min-height: 150px;
    padding: 50px;
    border-radius: 50px;
    background: #f3f3f3;
    margin-top: 80px;
    display: flex;
    justify-content: center;
    align-items: center;
}

p {
    width: 90%;
    text-align: center;
    line-height: 35px;
    font-family: "gilroy-medium";
    font-size: 23px;
    color: #313131;
}
</style>
