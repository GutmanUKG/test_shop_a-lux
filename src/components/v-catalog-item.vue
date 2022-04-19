<template>
    <div class="v-catalog-item-wrapper">
        <b-container>
            <div class="v-catalog-item row">
                <div class="col-5 v-catalog-price-info">
                    <div class="v-catalog-item-img">
                        <img :src="require('../assets/' + product_data.img)" alt="">
                    </div>
                    <div class="v-catalog-item-price">
                        <p>{{product_data.price}} CHF</p>
                        <span>Длительность контракта: <b>12 месяцев</b></span>
                    </div>
                </div>

                <div class="col-6 v-catalog-info">
                    <h2 class="v-catalog-item-title">{{product_data.title}}</h2>
                    <div class="v-catalog-item-descr">
                        {{product_data.descr}}
                    </div>
                    <div class="v-catalog-item-buttons">
                        <a href="#" class="v-catalog-item-about-link">
                            Подробнее
                        </a>

                        <button @click="addToCart" class="v-catalog-item-add-to-cart" v-if="isCart">Добавить в корзину</button>
                        <span class="v-catalog-item-about-link" v-else>Добавленно</span>
                    </div>

                </div>
            </div>
        </b-container>
    </div>

</template>

<script>
export default {
   name: "v-catalog-item",
    data: () => ({
        isCart: true
    }),
    props:{
    product_data: {
        type: Object,
        default: () => ({})
    }
  },
    computed: {

    },
    methods: {
        addToCart(){
            this.$emit('addToCart',this.product_data)
            this.isCart = false
        }
    }



}
</script>

<style lang="scss">
    .v-catalog-item-wrapper{
        padding: 80px;
        box-sizing: border-box;
        &:nth-child(2n + 1){
            background: #F5FBFC;
            .v-catalog-item{
                .v-catalog-price-info{
                   order: 1;
                 }
                .v-catalog-info{
                order: 0;
                 }
            }
        }
    }
    .v-catalog-item{
        margin-bottom: 80px;
        display: flex;
        gap: 102px;
        &:nth-child(2n){

            .v-catalog-price-info{
                order: 1;

            }
            .v-catalog-info{
                order: 0;

            }
        }
        .v-catalog-item-img{
            background: url("../assets/vip.png") center no-repeat;
            max-width: 338px;
            height: 335px;
            img{
                width: 259.16px;
                height: 388.26px;
                object-fit: contain;
            }
        }
        .v-catalog-price-info{
            padding: 17px 72px 72px 72px;
            box-sizing: border-box;
            background: #FFFFFF;
            background: rgba(255,255,255, 0.7);
            box-shadow: 0px 8px 48px rgba(185, 215, 238, 0.4);
            border-radius: 20px;
            max-width: 480px;
            width: 100%;
        }
        .v-catalog-item-price{
            max-width: 338px;
            width: 100%;
            p{
                font-family: 'Gotham Pro',sans-serif;
                font-style: normal;
                font-weight: 900;
                font-size: 35px;
                line-height: 33px;
                color: #FC5944;
            }
            span{
                font-family: 'Gotham Pro',sans-serif;
                font-style: normal;
                font-weight: 400;
                font-size: 16px;
                line-height: 182%;
                text-align: center;
                color: #000000;
            }
        }
        .v-catalog-item-title{
            margin-bottom: 53px;
            font-family: 'Montserrat',sans-serif;
            font-style: normal;
            font-weight: 700;
            font-size: 50px;
            line-height: 88.4%;
            text-transform: uppercase;
            color: #3D3935;
            text-align: left;
        }
        .v-catalog-item-descr{
            font-family: 'Montserrat',sans-serif;
            font-style: normal;
            font-weight: 400;
            font-size: 18px;
            line-height: 170%;
            color: #3D3935;
            text-align: left;
        }
        .v-catalog-item-buttons{
            display: flex;
            gap: 25px;
            margin-top: 48px;
            .v-catalog-item-about-link{
                font-family: 'Montserrat',sans-serif;
                font-style: normal;
                font-weight: 700;
                font-size: 16px;
                color: #FB4030;
                padding: 16px 37px;
                box-sizing: border-box;
                border: 1px solid #FB4330;
                border-radius: 4px;
                text-decoration: none;
            }
            .v-catalog-item-add-to-cart{
                outline: none;
                border: none;
                padding: 16px 31px;
                font-family: 'Montserrat',sans-serif;
                font-style: normal;
                font-weight: 700;
                font-size: 16px;
                line-height: 20px;
                color: #FFFFFF;
                box-sizing: border-box;
                background: linear-gradient(135deg, #F2C314 0%, #FC3832 100%);
                box-shadow: 0px 2px 4px rgba(32, 5, 97, 0.1), 0px 1px 2px rgba(32, 5, 97, 0.08);
                border-radius: 4px;
                position: relative;
                width: 280px;
                text-align: right;
                &:before{
                    content: '';
                    background: url('../assets/icons/cart_icon_btn.png') center (center/cover) no-repeat;
                    width: 22px;
                    height: 22px;
                    position: absolute;
                    left:calc(31px)
                }
            }
        }

    }
</style>