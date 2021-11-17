<template>
<div class="item">
    <div class="img icon-product"></div>
    <div class="content">
        <p>Код: {{data.code}}</p>
        <p>{{data.name}}</p>
        <p>Цена: {{data.price * data.count}}</p>
        <div class="counter">
            <p class="counter" @click="minus()" v-if="data.flag">-</p>
            <p class="count">Количество: {{count}}</p>
            <p class="counter" @click="plus()" v-if="data.flag">+</p>
        </div>
        <p class="btn-delete btn-buy" v-if="data.flag">Купить</p>
        <p class="btn-delete" v-if="data.flag">Удалить</p>
    </div>
</div>
</template>
<script>
    export default {
        props: ["data"],
        data() {
            return {
                count: data.count
            }
        },
        methods: {
            plus() {
                this.count++
            },
            minus() {
                if (this.count > 1) {
                    this.count--
                }
            }
        }
    }
</script>
<style scoped>
.item {
    width: 95%;
    min-height: 250px;
    padding-left: 10px;
    margin: 10px;
    background: #f1f1f1;
    display: flex;
    justify-content: space-between;
    align-items: center;
    border-radius: 5px;
}

p {
    padding: 0;
    margin: 10px 0 10px 0;
    font-family: "gilroy-medium";
    font-size: 17px;
}

.img {
    width: 100px;
    height: 100px;
}

.content {
    min-height: 100%;
    width: 70%;
    display: block;
}

.content > .counter {
    display: flex;
    align-items: center;
}

.counter > .counter {
    cursor: pointer;
    padding: 10px;
    background: #94BE00;
    color: white;
    border-radius: 10px;
    font-size: 20px;
    line-height: 20px;
    margin: 0 10px 0 10px;
}

.btn-delete {
    font-size: 15px;
    background: rgb(196, 48, 48);
    color: white;
    border-radius: 10px;
    font-family: "gilroy-medium";
    display: flex;
    justify-content: center;
    align-items: center;
    transition-duration: 0.5s;
    cursor: pointer;
    user-select: none;
    width: 150px;
    height: 40px;
}

.btn-delete:hover {
    background: rgb(192, 105, 105);
    color: white;
}

.btn-buy {
    font-size: 15px;
    background: #94BE00;
    color: #313131;
    border-radius: 10px;
    font-family: "gilroy-medium";
    display: flex;
    justify-content: center;
    align-items: center;
    transition-duration: 0.5s;
    cursor: pointer;
    user-select: none;
    width: 150px;
    height: 40px;
}

.btn-buy:hover {
    color: white;
    background: #6d8b00;
}
</style>