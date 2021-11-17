<template>
<div class="topbar">
    <p class="logotype">Cab Shop</p>
    <nav class="menu">
        <a class="menu-item" @click="scrollingTo(catalog)">Каталог</a>
        <a class="menu-item" @click="scrollingTo(about)">О нас</a>
        <a class="menu-item" @click="scrollingTo()">Наши работы</a>
        <a class="menu-item" @click="scrollingTo(delivery)">Доставка</a>
        <a class="menu-item" @click="scrollingTo(service)">Услуги</a>
        <a class="menu-item" @click="scrollingTo(contact)">Контакты</a>
        <a class="menu-item" @click="scrollingTo(garanty)">Гарантия</a>
        <a class="menu-item" @click="scrollingTo(questions)">Вопрос / Ответ</a>
    </nav>
    <p v-if="!auth" @click="register" class="btn-green">Регистрация</p>
    <p v-if="!auth" @click="authorisation" class="btn-green">Войти</p>
    <UserTopbar 
        v-if="auth" 
        v-bind:email="email"
        v-bind:login="login"
        v-bind:password="password"
        v-bind:basket="basket"
        v-bind:list="list"
    ></UserTopbar>
</div> 
</template>
<script>
    import UserTopbar from './UserInfo.vue'
    export default {
        components: {
            UserTopbar
        },
        props: ["email", "auth", "login", "password", "basket", "list"],
        data() {
            return {
                about: ".about",
                delivery: ".delivery",
                catalog: ".catalog",
                service: ".service",
                contact: ".footer",
                garanty: ".problems",
                questions: ".questions",
                ourWorks: ".our-works"
            }
        },
        methods: {
            register() {
                this.$emit('register')
            },
            authorisation() {
                this.$emit('authorisation')
            },
            scrollingTo(value) {
                alert(value)
            }
        }
    }
</script>
<style>
.topbar {
    display: flex;
    justify-content: center;
    align-items: center;
    width: 100%;
    height: 100px;
    background: #313131;
    position: fixed;
    z-index: 100;
}

.logotype {
    font-size: 40px;
    color: #94BE00;
    font-family: "gilroy-medium";
}

.topbar > .logotype {
    margin-right: 40px;
}

nav.menu {
    height: 100%;
    display: flex;
    justify-content: space-around;
    align-items: center;
    margin-right: 30px;
}

nav.menu > a.menu-item {
    height: 100%;
    padding: 0 10px 0 10px;
    color: white;
    font-family: "gilroy-medium";
    font-size: 16px;
    cursor: pointer;
    display: flex;
    justify-content: center;
    align-items: center;
    text-decoration: none;
    transition-duration: 0.5s;
    background: rgb(148,190,0,0);
    user-select: none;
}

nav.menu > a.menu-item:hover {
    color: #94BE00;
    background: rgb(148,190,0,0.1);
}

.btn-green {
    padding: 10px 20px 10px 20px;
    background: #94BE00;
    color: #313131;
    border-radius: 50px;
    font-family: "gilroy-medium";
    display: flex;
    justify-content: center;
    align-items: center;
    transition-duration: 0.5s;
    cursor: pointer;
    user-select: none;
}

.btn-green:hover {
    background: #d6ee80;
}

.topbar > .btn-green {
    margin: 0 10px 0 10px;
}
</style>