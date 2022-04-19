<template>
        <div class="v-cart" :class="{bg_1: step < 2 ,bg_2: isNext, bg_3: isLast}">
            <template v-if="cart_data.length">
            <b-container>
            <div class="v-cart-steps col-8 d-flex">
                <div class="item item_cart" :class="{item_cart_2: step > 1}">
                    1.Корзина
                </div>
                <div class="item item_price" :class="{item_price_3: step > 1 , item_price_4: step > 2}">
                    2.Оплата
                </div>
                <div class="item item_check" :class="{item_check_4: step > 2}">
                    2.Выполнено
                </div>
            </div>
            <v-card-item
                    v-for="(item, index) in cart_data"
                    :key="item.id"
                    :cart_item_data="item"
                    :step="step"
                    @deleteFromCart="deleteFromCart(index)"
                    @incrementItem="incrementItem(index)"
                    @decrementItem="decrementItem(index)"
                    v-show="step === 1"
            >

            </v-card-item>
            <v-from-buy v-show="step === 2"/>
            <v-sucsess v-show="step === 3"/>
            <div :class="{next_step: isNext}" v-show="step < 3" class="v-cart-total">
                <div class="v-cart-price-full item">
                    <span>Итого: </span>
                    <span>{{carTotalCost}}</span>
                </div>
                <div class="v-cart-price-sale item">
                    <span>
                        Скидка
                    </span>
                    <span>
                        0 CHF
                    </span>
                </div>
                <div class="v-cart-price item">
                    <span>
                        Всего:
                    </span>
                    <span>
                         <span>{{carTotalCost}}</span>
                    </span>
                </div>
            </div>

            <div class="v-cart-buttons" :class="{btn_next_step: isNext}" v-show="step < 3">
                <router-link to="/" class="v-cart-item-link-back" v-if="step === 1">
                    Назад
                </router-link>
                <button class="v-cart-back" v-show="isNext" @click="BackStep">
                    Назад
                </button>
                <button class="v-cart-item-next-step" @click="NextStep">
                    Продолжить
                </button>
            </div>
            </b-container>
            </template>
            <template v-else>
                <h2 class="text-center">К сожалению тут пока ничего нет =(</h2>
                <router-link to="/">
                    В каталог
                </router-link>
            </template>
        </div>


</template>

<script>
    import VCardItem from "@/components/v-card-item";
    import {mapActions} from 'vuex'
    import VFromBuy from "@/components/v-from-buy";
    import VSucsess from "@/components/v-sucsess";
    export default {
        name: "v-cart",
        components: {VSucsess, VFromBuy, VCardItem},
        data: ()=>({
           step: 1,
            isNext: false,
            isLast: false
        }),
        methods: {
            NextStep(){
                this.step++
                this.isNext = true
                if(this.step > 2) {
                    this.isLast = true
                    this.isNext = false
                }
            },
            BackStep(){
              this.step--
               if(this.step < 2){
                   this.isNext = false
               }
            },
            ...mapActions([
                'DELETE_FROM_CART',
                'INCREMENT_CARD_ITEM',
                'DECREMENT_CARD_ITEM'
            ]),
            incrementItem(index){
                this.INCREMENT_CARD_ITEM(index)
            },
            decrementItem(index){
                this.DECREMENT_CARD_ITEM(index)
            },
            deleteFromCart(index){
               this.DELETE_FROM_CART(index)
            }
        },
        props: {
            cart_data: {
                type: Array,
                default: () => ([])
            }
        },
        computed: {
            carTotalCost(){
                let result = []
                if(this.cart_data.length){
                    for (let item of this.cart_data) {
                        result.push(item.price * item.quantity)
                    }
                    result = result.reduce(function (sum, el) {
                        return sum + el
                    })
                    return result
                }else {
                    return  0
                }
            }
        },
    }
</script>

<style lang="scss">
    .v-cart{
        .v-cart-steps{
            margin: 0 auto 100px auto;
            gap: calc(13px + 114px);
            justify-content: center;
            .item{
                width: max-content;
                display: flex;
                justify-content: center;
                flex-direction: column;
                align-items: center;
                gap: 10px;
                font-family: 'Montserrat',sans-serif;
                font-style: normal;
                font-weight: 700;
                font-size: 20px;
                line-height: 24px;
                letter-spacing: 0.02em;
                position: relative;
                &:after{
                    content: '';
                    display: block;
                    position: absolute;
                    right: 0;
                    width: 114px;
                    height: 1px;
                    background:  #999999;
                    top: 30%;
                    left: 50%;
                    transform: translate(50%, -100%);
                }
                &:first-child{
                    color: #F4A31B;
                }
                &:last-child{
                    &:after{
                        display: none;
                    }
                }

                &_cart{
                    position: relative;

                    &:before{
                        content: '';
                        display: block;
                        background: url("../assets/icons/shopping_cart_24px.png");
                        width: 30px;
                        height: 30px;
                    }
                    &_2{
                        color: #F4A31B;
                        &:after{
                            background: #F4A31B;
                        }
                    }
                }
                &_price{
                    &:before{
                        content: '';
                        display: block;
                        background: url("../assets/icons/account_balance_wallet_24px.png");
                        width: 30px;
                        height: 30px;
                    }
                    &_3{
                        color: #F4A31B;
                       &:before{
                           background: url("../assets/icons/account_balance_wallet_24px_check.png");
                       }
                    }
                    &_4{
                        &:after{
                            background: #F4A31B;
                        }
                    }
                }
                &_check{
                    &:before{
                        content: '';
                        display: block;
                        background: url("../assets/icons/assignment_turned_in_24px.png");
                        width: 30px;
                        height: 30px;
                    }
                    &_4{
                        color: #F4A31B;
                        &:before{
                            background: url("../assets/icons/assignment_turned_in_24px_check.png");

                        }
                    }
                }
            }

        }
        .v-cart-buttons{
            display: flex;
            gap: 25px;
            justify-content: flex-end;
            .v-cart-item-link-back,
            .v-cart-back{
                font-family: 'Montserrat',sans-serif;
                font-style: normal;
                font-weight: 700;
                font-size: 16px;
                color: #FB4030;
                padding: 20px 60px;
                box-sizing: border-box;
                border: 1px solid #FB4330;
                filter: drop-shadow(0px 2px 4px rgba(32, 5, 97, 0.1)) drop-shadow(0px 1px 2px rgba(32, 5, 97, 0.08));
                border-radius: 4px;
                text-decoration: none;
            }
            .v-cart-item-next-step{
                padding: 20px 50px;
                box-sizing: border-box;
                background: linear-gradient(135deg, #F2C314 0%, #FC3832 100%);
                box-shadow: 0px 2px 4px rgba(32, 5, 97, 0.1), 0px 1px 2px rgba(32, 5, 97, 0.08);
                border-radius: 4px;
                border: none;
                outline: none;
                font-family: 'Montserrat',sans-serif;
                font-style: normal;
                font-weight: 700;
                font-size: 16px;
                line-height: 20px;
                color: #FFFFFF;
            }
        }
        .v-cart-total{
            max-width: 410px;
            width: 100%;
            margin-left: auto;
            margin-bottom: 45px;
            .item{
                display: flex;
                justify-content: space-between;
                margin-bottom: 10px;
            }
            .v-cart-price-full{
                font-family: 'Montserrat',sans-serif;
                font-style: normal;
                font-weight: 700;
                font-size: 14px;
                color: #3D3935;
            }
            .v-cart-price-sale{
                font-family: 'Montserrat',sans-serif;
                font-style: normal;
                font-weight: 700;
                font-size: 18px;
                color: #F3A919;
            }
            .v-cart-price{
                font-family: 'Montserrat',sans-serif;
                font-style: normal;
                font-weight: 600;
                font-size: 18px;
                color: #3D3935;
            }
        }
        .next_step{
            margin: 50px auto  50px auto;
        }
        .btn_next_step{
            margin-top: 140px;
            justify-content: space-between;
        }
    }
    .bg_1{
        background: url("../assets/bg_step_1.png") no-repeat;
        height: 100vh;
        background-size: contain;
    }
    .bg_2{
        background: url("../assets/bg_step_2.png") no-repeat;
        height: 100vh;
        background-size: contain;
    }
    .bg_3{
        background: url("../assets/bg_3.png") no-repeat;
        height: 100vh;
        background-size: contain;
    }
</style>