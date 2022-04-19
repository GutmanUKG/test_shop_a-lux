<template>
    <div v-if="step === 1">
        <div class="v-card-item">
            <div class="v-card-item-img">
                <img :src="require('../assets/' + cart_item_data.img)" alt="">
            </div>

            <div class="v-card-item-info">
                <h2>{{cart_item_data.title}}</h2>
                <p>{{cart_item_data.preview}}</p>
            </div>
            <div class="d-flex align-items-center">
                <div class="v-card-item-price">
                <span>
                    {{cart_item_data.price}} CHF
                </span>
                    <small>
                        3000 CHF
                    </small>
                </div>
                <div class="v-cart-item_quantity">

                    <span @click="decrementItem">-</span>
                    <div class="v-card-item-quantity-counter">
                        {{cart_item_data.quantity}}
                    </div>
                    <span @click="incrementItem" >+</span>
                    <div class="v-card-item-quantity-price">
                        {{calcFullPrice}} CHF
                    </div>


                </div>
            </div>
            <button @click="deleteFromCart" class="v-card-item-delete"></button>
        </div>
    </div>

</template>

<script>
    export default {
        name: "v-card-item",
        props: {
            cart_item_data: {
                type: Object,
                default: () => ({})
            },
            step:{
                type:Number,
                default: 1
            }
        },
        data:() => ({
        }),
        computed: {
         calcFullPrice () {
             let full_price = '';
             full_price = this.cart_item_data.price * this.cart_item_data.quantity
             return full_price
         }
        },
        methods: {

            decrementItem(){
                this.full_price = this.cart_item_data.price * this.cart_item_data.quantity
               this.$emit('decrementItem')
            },
            incrementItem(){

                this.$emit('incrementItem')
            },
            deleteFromCart() {
                this.$emit('deleteFromCart')
            }
        },
        mounted() {
            this.$set(this.cart_item_data, 'quantity' , 1)
        }
    }
</script>

<style lang="scss">
.v-card-item{
    display: flex;
    align-items: center;
    flex-wrap: nowrap;
    justify-content: space-between;
    border-bottom: 1px solid #999999;
    padding-bottom: 20px;
    margin-bottom: 70px;
    .v-card-item-img{
        background: url("../assets/vip.png") no-repeat;
        width: 147px;
        height: 147px;
        background-size: contain;
        display: flex;
        align-items: center;
        justify-content: center;
        margin-right: 35px;
        img{
            width: 100%;
        }
    }
    .v-card-item-info{
        max-width: 322px;
        width: 100%;
        h2{
            font-family: 'Montserrat',sans-serif;
            font-style: normal;
            font-weight: 700;
            font-size: 20px;
            line-height: 88.4%;
            text-transform: uppercase;
            color: #3D3935;
            text-align: left;
            margin-bottom: 18px;
        }
        p{
            text-align: left;
            font-family: 'Montserrat',sans-serif;
            font-style: normal;
            font-weight: 500;
            font-size: 14px;
            line-height: 17px;
            color: #B0B0B0;
        }
    }
    .v-card-item-price{
        display: flex;
        flex-direction: column;
        margin-right: 26px;
        span{
            font-family: 'Montserrat',sans-serif;
            font-style: normal;
            font-weight: 700;
            font-size: 18px;
            color: #6D6D6D;
            margin-bottom: 6px;
        }
        small{
            font-family: 'Montserrat',sans-serif;
            font-style: normal;
            font-weight: 500;
            font-size: 10px;
            text-decoration-line: line-through;
            color: #8E8E8E;
        }

    }
    .v-cart-item_quantity{
        gap: 4px;
        display: flex;
        .v-card-item-quantity-counter{
            font-family: 'Montserrat',sans-serif;
            font-style: normal;
            font-weight: 700;
            font-size: 16px;
            text-align: center;
            color: #2E2E2E;
            width: 60.77px;
            height: 43.75px;
            border-radius: 100px;
            display: flex;
            align-items: center;
            justify-content: center;
            border: 1px solid #E1E1E1;
        }
        span{
           width: 43px;
            height: 43px;
            display: flex;
            justify-content: center;
            align-items: center;
            border-radius: 50%;
            background: #EFEFEF;
            cursor: pointer;
        }
        .v-card-item-quantity-price{
            font-family: 'Montserrat',sans-serif;
            font-style: normal;
            font-weight: 700;
            font-size: 18px;
            color: #6D6D6D;
            display: flex;
            align-items: center;
            margin-left: 24px;
        }
    }
    .v-card-item-delete{
        width: 13px;
        height: 17px;
        border: none;
        background: none;
        background: url("../assets/icons/delete_24px.png") center no-repeat;
    }
}
</style>