<template>
<body>
    <Topbar 
        v-bind:email="emailUser" 
        @register="openReg" 
        @authorisation="openAuth" 
        v-bind:auth="auth"
        v-bind:login="login"
        v-bind:password="password"
        v-bind:basket="userBasket"
        v-bind:list="userList"
    ></Topbar>
    <a v-bind:href="corpPhone">
        <div class="img phone-icon"></div>
    </a>
    <UserForm 
        @close="closeForm" 
        v-bind:open="openAuthForm" 
        v-bind:register="register"
        @basket="getBasket"
        @list="getList"
    ></UserForm>
    <div class="img shower-wallpaper">
        <p class="big-logotype">Cab Shop</p>
        <p class="losung">Магазин Душевых кабин</p>
        <p class="start-button">Начнем</p>
    </div>
    <div class="about">
        <p class="stars">* * *</p>
        <p>{{about}}</p>
        <p class="stars">* * *</p>
    </div>
    <div class="delivery">
        <div class="item">
            <p>Доставка по Минску</p>
            <p>Доставка душевых кабин: {{deliveryCity.delivery}}</p>
            <p>Бесплатная доставка: {{deliveryCity.freeDelivery}}</p>
            <p>Стоимость доставки: {{deliveryCity.price}}</p>
            <p>Подъем на этаж: {{deliveryCity.up}}</p>
            <p>Срок доставки: {{deliveryCity.deadline}}</p>
            <p>Время доставки заказов: {{deliveryCity.time}}</p>
        </div>
        <div class="img auto-icon"></div>
        <div class="item">
            <p>Доставка по Беларуси</p>
            <p>Доставка душевых кабин: {{deliveryCountry.delivery}}</p>
            <p>Бесплатная доставка: {{deliveryCountry.freeDelivery}}</p>
            <p>Стоимость доставки: {{deliveryCountry.price}}</p>
            <p>Подъем на этаж: {{deliveryCountry.up}}</p>
            <p>Срок доставки: {{deliveryCountry.deadline}}</p>
            <p>Время доставки заказов: {{deliveryCountry.time}}</p>
        </div>
    </div>
    <div class="service">
        <div class="item" @click="openPrice(price[0])">
            <div class="img calendar-icon"></div>
            <p>Работаем с 10:00 до 20:00 без выходных</p>
        </div>
        <div class="item" @click="openPrice(price[1])">
            <div class="img auto-icon"></div>
            <p>Мы осуществляем бесплатный замер</p>
        </div>
        <div class="item" @click="openPrice(price[2])">
            <div class="img role-icon"></div>
            <p>Мы осуществляем доставку бесплатно до двери</p>
        </div>
        <div class="item" @click="openPrice(price[3])">
            <div class="img hand-icon"></div>
            <p>Принимаем к оплате все виды платежей</p>
        </div>
        <price-info v-bind:openPriceInfo="openPriceInfo" v-bind:priceInfo="priceInfo" @closingPriceInfo="closingPrice"></price-info>
    </div>
    <div class="our-works"></div>
    <div class="catalog" v-if="!emptyCatalog">
        <div class="filter">
            <input 
                placeholder="Поиск"
                v-model="filterSearch"
                @input="setSearch"
            >
            <DropList
                class="droplist"
                v-bind:name="'Категория'"
                v-bind:list="categories"
                @value="setCategory"
            ></DropList>
            <DropList
                class="droplist"
                v-bind:name="'Сортировка'"
                v-bind:list="['По возрастанию цены', 'По убыванию цены', 'От новых к старым', 'От старых к новым']"
                @value="setSort"
            ></DropList>
            <input placeholder="Цены от" type="number"
                v-model="priceFrom"
                @input="setPrice"
            >
            <input placeholder="Цены до" type="number"
                v-model="priceTo"
                @input="setPrice"
            >
            <CheckBox
                v-for="(item, index) in filterNames"
                v-bind:key="(item, index)"
                v-bind:name="item"
                v-bind:list="filterProperties[index]"
                @value="setFilter"
            ></CheckBox>
        </div>
        <div class="panel">
            <div class="product" v-for="(product, idx) in products" v-bind:key="(product, idx)">
                <div v-bind:style="{ backgroundImage: 'url(' + product.desc.images[0] + ')' }" class="img"></div>
                <p>{{product.desc.name}}</p>
                <p>{{product.desc.price}} руб</p>
                <p class="button">Подробнее</p>
                <p class="button">В корзину</p>
            </div>
        </div>
    </div>
    <div class="about problems">
        <p class="stars">* * *</p>
        <p>Если возникли проблемы, то не стоит переживать, поскольку мы вернем Вам деньги по следующим услоивям</p>
        <div class="fragment" v-for="item in garanty" v-bind:key="item">
            <div class="img arrow-icon"></div>
            <p>{{item}}</p>
        </div>
        <p class="stars">* * *</p>
    </div>
    <div class="questions">
        <div class="panel">
            <Question
                v-for="(item, index) in questions"
                v-bind:key="(item, index)"
                v-bind:question="item"
                v-bind:answer="answers[index]"
            ></Question>
        </div>
        <div class="img qa-icon"></div>
    </div>
    <div class="footer">
        <iframe src="https://yandex.ru/map-widget/v1/?um=constructor%3A28a341ca2651e75a96a6c1b9c21556d13d8baa002fb86671ec2ade42da636b3a&amp;source=constructor" class="map" frameborder="0"></iframe>
        <form>
            <p>Напишите нам</p>
            <input placeholder="Имя">
            <input placeholder="Email">
            <textarea placeholder="Сообщение"></textarea>
            <button>Отправить</button>
        </form>
        <div class="contacts">
            
        </div>
    </div>
</body>
</template>
<script>
    import Topbar from '../component/Topbar.vue'
    import UserForm from '../component/UserForm.vue'
    import PriceInfo from '../component/PriceInfo.vue'
    import Question from '../component/Question.vue'
    import DropList from '../instrument/DropList.vue'
    import CheckBox from '../instrument/CheckBox.vue'
    import config from '../../../../src/client-config.json'
    export default {
        components: {
            Topbar, UserForm, PriceInfo, Question, DropList, CheckBox
        },
        data() {
            return {
                api: config.api,

                emailUser: "default@gmail.com",
                login: "default",
                password: "defPass123",
                auth: false,
                openAuthForm: false,
                openPriceInfo: false,
                priceInfo: "",
                register: false,
                userBasket: [],
                userList: [],

                about: config.about,
                deliveryCity: config.delivery.minsk,
                deliveryCountry: config.delivery.country,
                garanty: config.garanty,
                price: config.price,
                questions: config.question,
                answers: config.answer,
                corpPhone: config.phone,
                emptyCatalog: false,
                forCategory: [],
                categories: [],
                filterSearch: "",
                priceFrom: "",
                priceTo: "",
                filterNames: [],
                filterProperties: [],
                filter: new Map(),
                filterCategory: "",
                filterSort: "",
                products: [],
                rememberProducts: []
            }
        },
        computed: {
            icons: {
                get: function() {
                    return this.rememberProducts.map(item => {
                        return {backgroundImage: `url(${item.desc.images[0]})`}
                    })
                }
            }
        },
        async created() {
            if(this.products.length = 0) {
                this.emptyCatalog = true
            }
            else {
                this.emptyCatalog = false
            }

            this.forCategory = await this.requests("http://localhost:3000/public/get/category", {
                method: "GET"
            })
            this.products = await this.requests("http://localhost:3000/public/get/product", {
                method: "GET"
            })
            this.rememberProducts = this.products
            
            this.categories = this.forCategory.map(item => {
                return item.name
            })
        },
        methods: {
            setCategory(value) {
                this.filterCategory = value
                this.products = this.rememberProducts
                this.products = this.filting()
            },
            setSort(value) {
                this.filterSort = value
                this.products = this.rememberProducts
                this.products = this.filting()
            },
            setPrice() {
                this.products = this.rememberProducts
                this.products = this.filting()
            },
            setSearch() {
                this.products = this.rememberProducts
                this.products = this.filting()
            },
            searching(){
                let products = this.rememberProducts
                if(this.filterSearch != '') {
                    products = products.filter(item => {
                        return item.desc.name.indexOf(this.filterSearch) != -1
                    })
                } else {}
                return products
            },
            findPrice() {
                let products = this.rememberProducts
                if (this.priceFrom == '' && this.priceTo == '') {
                    products = this.rememberProducts
                }
                else if (this.priceFrom != '' && this.priceTo == '') {
                    products = products.filter(item => {
                        return item.desc.price >= this.priceFrom
                    })
                }
                else if (this.priceFrom == '' && this.priceTo != '') {
                    products = products.filter(item => {
                        return item.desc.price <= this.priceTo
                    })
                } else {
                    products = products.filter(item => {
                        return item.desc.price >= this.priceFrom && item.desc.price <= this.priceTo
                    })
                }
                return products
            },
            closeForm() {
                this.openAuthForm = false
                this.register = false
            },
            openReg() {
                this.openAuthForm = true
                this.register = true
            },
            openAuth() {
                this.openAuthForm = true
                this.register = false
            },
            getBasket(e){
                this.userBasket = e
            },
            getList(e){
                this.userList = e
            },
            openPrice(value) {
                this.priceInfo = value
                this.openPriceInfo = true
            },
            closingPrice() {
                this.openPriceInfo = false
            },
            findCategory() {
                let products = this.rememberProducts
                let filterNames = this.forCategory.filter(item => {
                    return item.name == this.filterCategory
                }).map(item => {
                    return item.template.filter.name
                })
                filterNames = filterNames[0]
                let filterProperties = this.forCategory.filter(item => {
                    return item.name == this.filterCategory
                }).map(item => {
                    return item.template.filter.list
                })
                filterProperties = filterProperties[0]

                if (this.filterNames == filterNames && this.filterProperties == filterProperties) {}
                else {
                    this.filter = new Map()
                }
                this.filterNames = filterNames
                this.filterProperties = filterProperties

                if(this.filterCategory == "Категория" || this.filterCategory == "") {
                    products = this.rememberProducts
                } else {
                    let category = this.forCategory.filter(item => {
                        return item.name == this.filterCategory
                    })[0].id
                    products = this.products.filter(item => {
                        return item.Category_id == category
                    })
                }
                return products
            },
            findSort(value) {
                let products = value
                let prices = products.map(item => {
                    return item.desc.price
                })
                let dates = products.map(item => {
                    return new Date(item.desc.date)
                })
                let copy = (arr, mask, parameter, parser) => {
                    let param = parameter()
                    let result = []
                    mask.forEach(m => {
                        arr.filter(a => {
                            return parser(a.desc[param]) == parser(m)
                        }).forEach(t => {
                            result.push(t)
                        })
                    })
                    return result
                }
                if(this.filterSort == "") {
                    this.filterSort = "Сортировка"
                }
                switch(this.filterSort) {
                    case 'По возрастанию цены': 
                        prices.sort((a, b) => {
                            return a - b
                        })
                        products = copy(products, prices, () => {
                            return "price"
                        }, item => {
                            return item
                        })
                        break;
                    case 'По убыванию цены':
                        prices.sort((a, b) => {
                            return b - a
                        })
                        products = copy(products, prices, () => {
                            return "price"
                        }, item => {
                            return item
                        })
                        break;
                    case 'От новых к старым':
                        dates.sort((a, b) => {
                            return b - a
                        })
                        products = copy(products, dates, () => {
                            return "date"
                        }, item => {
                            return new Date(item).getTime()
                        })
                        break;
                    case 'От старых к новым':
                        dates.sort((a, b) => {
                            return a - b
                        })
                        products = copy(products, dates, () => {
                            return "date"
                        }, item => {
                            return new Date(item).getTime()
                        })
                        break;
                    case 'Сортировка':
                        products = products
                        break;
                }
                return products
            },
            setFilter(value) {
                this.$set(this.filter, value[0], value[1])
                this.products = this.rememberProducts
                this.products = this.filting()
            },
            filting() {
                let sorting = (filter, list) => {
                    let flag = false
                    this.filterNames.forEach((name, idx) => {
                        try {
                            filter[name].forEach(item => {
                                flag = flag || list[idx].includes(item)
                            })
                        } catch(e) {}
                    })
                    return flag
                }

                let mass = this.findCategory().filter(
                    x => this.searching().filter(
                        x => this.findPrice().includes(x)
                    ).includes(x)
                )

                let count = 0
                if (this.filterNames != undefined) {
                    this.filterNames.forEach(item => {
                        try {
                            count += this.filter[item].length
                        } catch(e) {}
                    })
                }

                if (count != 0) {
                    let mass_ = []
                    mass.forEach(prod => {
                        let filter = this.filter
                        let list = prod.desc.filter.list
                        if (sorting(filter, list)) {
                            mass_.push(prod)
                        }
                    })
                    mass = mass_
                }
                return this.findSort(mass)
            },

            async requests(url, header) {
                try {
                    let response = await fetch(url, header)
                    let data = await response.json()
                    return data
                }
                catch(e) {
                    return e.message
                }
            }
        }
    }
</script>
<style>
body {
    margin: 0;
    padding: 0;
}

@keyframes phone {
    from {
        transform: scale(1);
    }
    50% {
        transform: scale(1.2);
    }
    to {
        transform: scale(1);
    }
}

.phone-icon {
    width: 70px;
    height: 70px;
    position: fixed;
    margin: 80vh 0 0 70vw;
    animation: phone 2s ease-in-out infinite;
    display: none;
}

@media screen and (max-width: 800px) {
    .phone-icon {display: block}
}

[v-cloak] {
    display: none;
}

body::-webkit-scrollbar {
    width: 0;
}

p.big-logotype {
    color: #94BE00;
    font-family: "gilroy-medium";
    font-size: 110px;
    text-shadow: 0 0 20px black;
    padding: 0;
    margin: 0;
}

p.losung {
    color: white;
    font-family: "gilroy-medium";
    font-size: 35px;
    margin: 15px;
}

p.start-button {
    width: 300px;
    height: 60px;
    color: #313131;
    background: #94BE00;
    border-radius: 40px;
    display: flex;
    justify-content: center;
    align-items: center;
    position: absolute;
    font-family: "gilroy-medium";
    font-size: 25px;
    margin-top: 400px;
    cursor: pointer;
    transition-duration: 0.5s;
    user-select: none;
}

p.start-button:hover {
    background: #a9bd63;
}

div.shower-wallpaper {
    width: 100%;
    height: 650px;
    display: flex;
    justify-content: center;
    flex-direction: column;
    align-items: center;
}

p::selection {
    color: white;
    background: #94BE00;
}

h1::selection {
    color: white;
    background: #94BE00;
}

.img {
    background-repeat: no-repeat;
    background-position: center center;
    background-size: cover;
}
input::placeholder{
    user-select: none;
}

.about {
    width: 100%;
    min-height: 500px;
    font-family: "gilroy-medium";
    font-size: 23px;
    display: flex;
    justify-content: space-around;
    align-items: center;
    flex-direction: column;
    color: #313131;
}

.about p {
    width: 70%;
    text-align: center;
    line-height: 35px;
}

.about .img {
    width: 120px;
    height: 60px;
    margin: 30px;
}

.about .fragment {
    width: 100%;
    display: flex;
    justify-content: space-around;
    align-items: center;
    flex-direction: column;
}

.stars {
    font-size: 50px;
    color: #94BE00;
    margin: 20px 0 0 0;
}
.delivery {
    width: 100%;
    min-height: 500px;
    font-family: "gilroy-medium";
    font-size: 20px;
    display: flex;
    justify-content: center;
    align-items: center;
    color: #313131;
    padding: 70px 0 70px 0;
    background: linear-gradient( rgba(0, 0, 0, 0.7), rgba(255, 255, 255, 0.1) ), url("../../../../public/src/resource/sprite/other/del.jpg");
    background-repeat: no-repeat;
    background-position: center center;
    background-size: cover;
}

.delivery > p {
    width: 100%;
    text-align: center;
}

.delivery > .img {
    width: 250px;
    height: 250px;
    margin: 0;
    margin-right: 60px;
    margin-left: 60px;
}

.delivery > .item {
    width: 330px;
    margin: 0 10px 0 10px;
    min-height: 400px;
    background: #f3f3f3;
    padding: 30px;
    border-radius: 30px;
}

.delivery > .item > p:first-child {
    margin: 0 auto;
    color: #94BE00;
    font-size: 30px;
    text-align: center;
}

.service {
    width: 100%;
    min-height: 250px;
    text-align: center;
    font-family: "gilroy-medium";
    font-size: 20px;
    display: flex;
    justify-content: center;
    align-items: center;
    color: #313131;
    flex-wrap: wrap;
    padding-top: 80px;
    padding-bottom: 80px;
}

.service > .item {
    display: flex;
    align-items: center;
    flex-direction: column;
    width: 200px;
    height: 200px;
    background: #f3f3f3;
    margin: 0 30px 0 30px;
    padding: 25px;
    border-radius: 15px;
    cursor: pointer;
    transition-duration: 0.5s;
}
.service > .item:hover {
    transform: scale(1.1)
}

.service .img {
    width: 100px;
    height: 100px;
}

.catalog {
    width: 100%;
    display: flex;
    justify-content: center;
    padding-bottom: 50px;
}

.catalog > .filter {
    background: #f3f3f3;
    border-radius: 20px;
    padding: 30px;
    width: 300px;
    display: flex;
    flex-direction: column;
}

.catalog > .filter .droplist {
    margin-top: 10px;
    margin-bottom: 10px;
}

.catalog > .filter input {
    width: 100%;
    height: 40px;
    border: solid #94BE00 2px;
    outline: none;
    border-radius: 20px;
    font-family: "gilroy-medium";
    font-size: 17px;
    text-indent: 10px;
    background: #f3f3f3;
    transition-duration: 0.5s;
    margin-top: 10px;
    margin-bottom: 10px;
}

.catalog > .filter input::placeholder {
    color: #94BE00
}

.catalog > .panel {
    padding: 30px;
    border: solid 2px #c1c1c1;
    width: 900px;
    margin-left: 30px;
    display: flex;
    flex-wrap: wrap;
    max-height: 2000px;
    overflow-y: scroll;
}

.panel > .product {
    width: 29.9%;
    height: 450px;
    padding-bottom: 30px;
    background: #eeeeee;
    border-radius: 10px;
    display: flex;
    align-items: center;
    flex-direction: column;
    margin: 5px;
    padding-left: 10px;
    padding-right: 10px;
}

.product > .img {
    width: 85%;
    height: 60%;
    font-family: "gilroy-medium";
    font-size: 15px;
    color: #94BE00;
    display: flex;
    align-items: center;
    justify-content: center;
    border-radius: 0 0 10px 10px;
}

.product > p {
    display: flex;
    justify-content: center;
    align-items: center;
    font-family: "gilroy-medium";
    font-size: 17px;
    margin: 0;
    margin-top: 10px;
    text-align: center;
}

.product > .button {
    width: 70%;
    height: 30px;
    background: #94BE00;
    color: white;
    cursor: pointer;
    border-radius: 10px;
    transition-duration: 0.5s;
}

.product > .button:hover {
    background: #b4c967;
}

.panel::-webkit-scrollbar {
    background: rgba(0, 0, 0, 0);
    width: 10px;
    border-radius: 0 15px 15px 0;
}

.panel::-webkit-scrollbar-thumb {
    background: #c1c1c1;
    border-radius: 5px 0 0 5px;
}

.questions {
    width: 100%;
    min-height: 500px;
    display: flex;
    justify-content: center;
    padding: 60px 0 80px 0;
}

.questions .img {
    width: 600px;
    height: 800px;
    box-shadow: 30px 30px 0 #94BE00;
}

.questions .panel {
    display: block;
    margin-right: 40px;
}

.footer {
    width: 100%;
    height: 550px;
    background: #313131;
    display: flex;
    justify-content: space-around;
    align-items: center;
}

.footer > form {
    width: 400px;
    height: 450px;
    background: #464646;
    border-radius: 20px;
    display: flex;
    justify-content: space-around;
    align-items: center;
    flex-direction: column;
    padding-bottom: 15px;
}

.footer > form input {
    width: 85%;
    height: 40px;
    background: #464646;
    border: solid #94BE00 2px;
    outline: none;
    border-radius: 20px;
    font-family: "gilroy-medium";
    font-size: 17px;
    text-indent: 10px;
    color: white;
    transition-duration: 0.5s;
}

.footer > form input:focus {
    border: solid #94BE00 2px;
    background-color: #5c5c5c;
}

.footer > form textarea {
    width: 85%;
    height: 150px;
    background: #464646;
    border: solid #94BE00 2px;
    outline: none;
    border-radius: 20px;
    resize: none;
    font-family: "gilroy-medium";
    font-size: 17px;
    text-indent: 10px;
    color: white;
    transition-duration: 0.5s;
    padding-top: 10px;
}

.footer > form textarea:focus {
    border: solid #94BE00 2px;
    background-color: #5c5c5c;
}

.footer > form textarea::placeholder {
    color: #94BE00;
}

.footer > form input::placeholder {
    color: #94BE00;
}

.footer > form p {
    color: #94BE00;
    font-family: "gilroy-medium";
    font-size: 30px;
    line-height: 0;
}

.map {
    width: 450px;
    height: 450px;
    border-radius: 20px;
}

.footer > .contacts {
    width: 400px;
    height: 450px;
    justify-content: space-around;
    align-items: center;
    flex-direction: column;
}

.footer > form button {
    width: 70%;
    height: 60px;
    background: #94BE00;
    border: none;
    outline: none;
    border-radius: 20px;
    color: #313131;
    font-family: "gilroy-medium";
    font-size: 20px;
    cursor: pointer;
    border: #94BE00 solid 2px;
    transition-duration: 0.5s;
}

.footer > form button:hover {
    background: #464646;
    color: #94BE00;
}
</style>
