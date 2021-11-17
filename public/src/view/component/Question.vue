<template>
    <div class="block">
        <p class="question">{{question}}</p>
        <p class="showit" @click="mout">Показать</p>
        <p class="answer" v-if="show">{{answer}}</p>
    </div>
</template>
<script>
    export default {
        props: ["question", "answer"],
        data() {
            return {
                show: false
            }
        },
        methods: {
            mout() {
                this.show = !this.show
            }
        }
    }
</script>
<style scoped>
    .block {
        background: #f3f3f3;
        font-family: "gilroy-medium";
        font-size: 22px;
        color: #313131;
        display: flex;
        justify-content: space-between;
        flex-wrap: wrap;
        margin-bottom: 5px;
        width: 600px;
        border-radius: 20px 0 0 20px;
    }
    .block p {
        margin: 0;
    }
    .question {
        color: #94BE00;
        width: 60%;
        font-size: 20px;
        display: flex;
        align-items: center;
        padding: 20px;
    }
    .answer {
        width: 100%;
        font-size: 20px;
        display: flex;
        align-items: center;
        padding: 20px;
    }
    .showit {
        color: white;
        width: 20%;
        background: #94BE00;
        transition-duration: 0.5s;
        cursor: pointer;
        display: flex;
        justify-content: center;
        align-items: center;
    }
    .show-it:hover {
        background: #aabe61;
    }
</style>