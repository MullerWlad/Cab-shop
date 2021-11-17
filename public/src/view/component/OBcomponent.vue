<template>
    <div class="ob-panel">
        <h1>{{name}}</h1>
        <div class="img empty-icon" v-if="empty"></div>
        <PanelItem 
            v-for="item in list" 
            v-bind:key="item"
            v-bind:data="item"
        ></PanelItem>
        <PanelItem 
            v-for="item in basket" 
            v-bind:key="item"
            v-bind:data="item"
        ></PanelItem>
    </div>
</template>
<script>
    import PanelItem from './PanelItem.vue'
    export default {
        props: ["list", "basket", "name"],
        data() {
            return {
                empty: true
            }
        },
        components: {
            PanelItem
        }
    }
</script>
<style scoped>
.ob-panel {
    width: 400px;
    min-height: 200px;
    max-height: 300px;
    position: absolute;
    padding: 20px 50px 50px 50px;
    background: white;
    display: flex;
    flex-direction: column;
    justify-content: space-between;
    align-items: center;
    box-shadow: 0 0 100px #313131;
    border-radius: 15px;
    overflow-y: auto;
}
.ob-panel > .img {
    width: 150px;
    height: 150px;
}
.ob-panel::-webkit-scrollbar {
    background: #f1f1f1;
    width: 10px;
    border-radius: 0 15px 15px 0;
}
.ob-panel::-webkit-scrollbar-thumb {
    background: #c1c1c1;
    border-radius: 10px;
}
h1 {
    font-family: "gilroy-medium";
    color: #313131;
}
</style>