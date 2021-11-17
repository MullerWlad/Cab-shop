<template>
    <div class="icon-topbar">
        <div class="basket"><div class="img icon-basket" @click="showBaskets"></div></div>
        <div class="img icon-user" @click="open"></div>
        <p class="email">{{email}}</p>
        <div class="info" v-if="showInfo">
            <p class="info" v-if="showData">Логин: {{login}}</p>
            <p class="info" v-if="showData">Пароль: {{password}}</p>
            <p class="btn-green" @click="show">{{showWord}} данные</p>
            <p class="btn-green">Выйти</p>
            <p class="btn-green" @click="showOrders">Мои заказы</p>
            <o-bcomponent class="component"
                v-if="showOrder"
                v-bind:list="list"
                v-bind:name="names[1]"
            ></o-bcomponent>
        </div>
        <o-bcomponent class="component"
            v-if="showBasket"
            v-bind:list="basket"
            v-bind:name="names[0]"
        ></o-bcomponent>
    </div>
</template>
<script>
    import OBcomponent from './OBcomponent.vue'
    export default {
        components: {
            OBcomponent
        },
        props: ["email", "login", "password", "basket", "list"],
        data() {
            return {
                showInfo: false,
                showWord: "Показать",
                showData: false,
                showOrder: false,
                showBasket: false,
                names: ["Корзина", "Заказы"]
            }
        },
        methods: {
            open() {
                this.showInfo = !this.showInfo
                if(this.showInfo == false) {
                    this.showOrder = false
                }
            },
            show() {
                this.showData = !this.showData
                if (this.showData) {
                    this.showWord = "Скрыть"
                }
                else {
                    this.showWord = "Показать"
                }
            },
            showOrders() {
                this.showOrder = !this.showOrder
            },
            showBaskets() {
                this.showBasket = !this.showBasket
            }
        }
    }
</script>
<style scoped>
.img {
    width: 50px;
    height: 50px;
    border-radius: 100px;
    cursor: pointer;
    transition-duration: 0.5s;
}

div.info > .component {
    margin-left: -480px;
    top: -7px;
}

div.icon-topbar > .component {
    top: 120px;
    left: 100px;
}

.img:hover {
    opacity: 0.4;
}

.icon-user {
    margin-left: 15px;
}

.basket {
    background: #94BE00;
    border-radius: 100px;
    padding: 7px;
}

.icon-topbar {
    margin-left: 20px;
    height: 100%;
    display: flex;
    justify-content: center;
    align-items: center;
}

p.email {
    color: #94BE00;
    font-family: "gilroy-medium";
    font-size: 20px;
    margin-left: 10px;
}

p.info {
    color: #313131;
    font-family: "gilroy-medium";
    font-size: 20px;
}

div.info {
    width: 300px;
    padding: 30px;
    min-height: 200px;
    background: white;
    display: flex;
    flex-direction: column;
    justify-content: space-around;
    box-shadow: 0 0 100px #313131;
    border-radius: 20px;
    position: absolute;
    margin-top: 500px;
}

.btn-green {
    padding: 15px;
    font-size: 20px;
    min-width: 100px;
}
</style>