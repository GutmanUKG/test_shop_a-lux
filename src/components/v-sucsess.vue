<template>
    <div class="v-sucsess">
        <img src="../assets/secsess_img.png" alt="">
        <div class="v-sucsess_text">
            <h2>
                Заказ оформлен!
            </h2>
            <p>
                По своей сути рыбатекст является альтернативой традиционному lorem ipsum, который вызывает у некторых людей недоумение при попытках прочитать рыбу текст
            </p>
            <a href="#">
                Личный кабинет
            </a>
        </div>
    </div>
</template>

<script>
    export default {
        name: "v-sucsess"
    }
</script>

<style lang="scss">
    .v-sucsess{
        .v-sucsess_text{
            max-width: 448px;
            width: 100%;
            margin: 80px auto 100px auto;
            h2{
                font-family: 'Montserrat',sans-serif;
                font-style: normal;
                font-weight: 400;
                font-size: 34px;
                line-height: 41px;
                text-align: center;
                letter-spacing: 0.4px;
                color: #1B2437;
                margin-bottom: 30px;
            }
            p{
                font-family: 'Montserrat',sans-serif;
                font-style: normal;
                font-weight: 400;
                font-size: 16px;
                line-height: 24px;
                text-align: center;
                color: #8E8E93;
            }
            a{
                margin: 47px auto 0 auto;
                background: linear-gradient(135deg, #F2C314 0%, #FC3832 100%);
                box-shadow: 0px 2px 4px rgba(32, 5, 97, 0.1), 0px 1px 2px rgba(32, 5, 97, 0.08);
                border-radius: 4px;
                padding: 16px 32px;
                box-sizing: border-box;
                text-decoration: none;
                font-family: 'Montserrat',sans-serif;
                font-style: normal;
                font-weight: 700;
                font-size: 16px;
                color: #FFFFFF;
                display: block;
                width: max-content;
            }
        }
    }
</style>