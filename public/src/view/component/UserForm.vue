<template>
<div v-if="open" v-on:click="closed">
    <form v-on:click.stop>
        <h1 v-if="register">Регистрация</h1>
        <h1 v-if="!register">Авторизация</h1>
        <input placeholder="Логин">
        <input v-if="register" placeholder="Email">
        <input placeholder="Пароль">
        <p class="btn-green" v-if="!register" @click="returnList">Войти</p>
        <p class="btn-green" v-if="register">Регистрация</p>
    </form>
</div>
</template>
<script>
    export default {
        props: ["open", "register"],
        data() {
            return {
                basket: [],
                list: []
            }
        },
        methods: {
            closed() {
                this.$emit('close')
            },
            returnBasket() {
                this.$emit('basket', this.basket)
            },
            returnList() {
                this.$emit('list', this.list)
            }
        }
    }
</script>
<style scoped>
div {
    margin-top: 150px;
    position: fixed;
    width: 100%;
    z-index: 100;
}
form {
    width: 400px;
    min-height: 200px;
    padding: 50px;
    border-radius: 40px;
    background: white;
    box-shadow: 0 0 100px #313131;
    margin: 0 auto;
    display: flex;
    flex-direction: column;
    justify-content: space-around;
    align-items: center;
}
input {
    width: 100%;
    height: 50px;
    outline: none;
    border: solid 2px #94BE00;
    border-radius: 15px;
    text-indent: 10px;
    font-family: "gilroy-medium";
    font-size: 20px;
    color: #313131;
    margin-top: 15px
}
input::placeholder {
    color: #94BE00;
    font-family: "gilroy-medium";
    font-size: 20px;
}
h1 {
    font-family: "gilroy-medium";
    color: #313131;
}
.btn-green {
    font-size: 25px;
    min-width: 100px;
    padding: 15px
}
</style>