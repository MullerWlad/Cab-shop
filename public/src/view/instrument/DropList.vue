<template>
    <div class="droplist">
        <div class="droper">
            <p class="list" @click="use">{{nameP}}</p>
            <div v-for="item in list" v-bind:key="item">
                <p class="list" v-if="open" @click="change(item)">{{item}}</p>
            </div>
        </div>
        <p class="clear" @click="clear">-</p>
    </div>
</template>
<script>
    export default {
        props: ["name", "list"],
        data() {
            return {
                open: false,
                mind: [this.name, this.list],
                nameP: this.name
            }
        },
        methods: {
            use() {
                this.open = !this.open
            },
            change(value) {
                this.nameP = value
                this.$emit('value', this.nameP)
                this.use()
            },
            clear() {
                this.nameP = this.mind[0]
                this.$emit('value', this.nameP)
                this.open = false
            }
        }
    }
</script>
<style scoped>
    .droplist {
        width: 100%;
        font-family: "gilroy-medium";
        font-size: 17px;
        display: flex;
        flex-direction: row;
    }
    .droper {
        width: 80%;
        color: white;
    }
    .droper > div {
        width: 100%;
    }
    p.list {
        width: 100%;
        min-height: 50px;
        text-indent: 10px;
        color: #323232;
        margin: 0;
        display: flex;
        align-items: center;
        cursor: pointer;
        border-bottom: 1px #c1c1c1 solid;
    }
    .droper > p.list:first-child {
        color: white;
        border: none;
        margin: none;
        background: #94BE00;
        border: none;
    }
    .clear {
        width: 20%;
        height: 50px;
        background: rgba(196, 48, 48, 0.8);
        display: flex;
        justify-content: center;
        align-items: center;
        color: white;
        transition-duration: 0.5s;
        cursor: pointer;
        padding: 0;
        margin: 0;
    }
    .clear:hover {
        background: rgba(201, 75, 75, 0.8);
    }
</style>