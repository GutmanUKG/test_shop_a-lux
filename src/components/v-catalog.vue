<template>
    <div class="v-catalog">
        <keep-alive>
        <router-link :to="{name: 'cart', params: {cart_data:CART}}" class="v-catalog-link-cart">
            <div >
                Корзина: {{CART.length}}
            </div>
        </router-link>
        </keep-alive>
           <v-catalog-item
                   v-for="product in PRODUCTS"
                   :key="product.id"
                   :product_data="product"
                   @addToCart="addToCart"
           >
           </v-catalog-item>

    </div>
</template>

<script>
import VCatalogItem from "@/components/v-catalog-item";
import {mapActions, mapGetters} from 'vuex';
export default {
   name: "v-catalog",
    components: {VCatalogItem},
    data: () => ({
    }),
    methods: {
        ...mapActions([
            'GET_PRODUCTS_FROM_API',
            'ADD_TO_CART'
        ]),
        addToCart(data){
           this.ADD_TO_CART(data)

        }


    },
    computed: {
        ...mapGetters([
            'PRODUCTS',
            'CART'
        ])
    },
    mounted() {
       this.GET_PRODUCTS_FROM_API()
        .then((responce) => {
            if (responce.data){
                console.log('Data arrived!')
            }
        })
    }
}
</script>

<style lang="scss">
    .v-catalog{
        background: url("../assets/catalog_bg.png") no-repeat;

    }
    .bg_top{
        position: fixed;
        left: 0;
        width: 292px;
        height: 292px;
        background: url("../assets/bitcoin-bg.png") left no-repeat;
    }
    .bg_bottom{
        background: url("../assets/bg_bottom.png") right no-repeat;
        position: absolute;
        bottom: 0;
        right: 0;
        width: 292px;
        height: 292px;
    }
</style>