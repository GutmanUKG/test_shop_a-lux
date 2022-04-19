<template>
    <form action="" class="v-from-buy">
        <span>
            Номер карты
        </span>
        <div class="v-from-buy-card-number">
            <input type="text" @input="NextInput($event.target)" maxlength="4" placeholder="0000">
            <input type="text" @input="NextInput($event.target)" maxlength="4" placeholder="0000">
            <input type="text" @input="NextInput($event.target)" maxlength="4" placeholder="0000">
            <input type="text" @input="NextInput($event.target)" maxlength="4"  placeholder="0000">
        </div>
        <div class="v-from-buy-card-info">
            <div class="date">
                <span>
                    Дата выдачи
                </span>
                <input type="input" placeholder="MM/YY" @input="CheckNumberDate($event.target)" maxlength="5">
            </div>
            <div class="cvv">
                <span>
                    CVV
                </span>
                <input type="text" placeholder="000" maxlength="3" @input="CheckNumber($event.target)">
            </div>
        </div>
    </form>
</template>

<script>
    export default {
        name: "v-from-buy",
        methods: {
            CheckNumberDate(x){
                console.log(x.value.replace(0, 1))

            },
            CheckNumber(x){
                x.value = x.value.replace(/[^\d]/g, '')
            },
            NextInput(x){
                x.value = x.value.replace(/[^\d]/g, '')
                let ml = x.getAttribute('maxlength');
                if(ml && x.value.length >= ml){
                    do{
                        x = x.nextSibling;
                    }
                    while(x && !(/text/.test(x.type)));
                    if(x && /text/.test(x.type)){
                        x.focus();
                    }
                }

            }
        }
    }
</script>

<style lang="scss">
    .v-from-buy{
        margin: 0 auto;
        background: linear-gradient(135deg, #F2C314 0%, #FC3832 100%);
        box-shadow: 0px 8px 24px 6px rgba(237, 163, 181, 0.303786);
        border-radius: 16px;
        max-width: 370px;
        width: 100%;
        padding: 26px 32px 32px 24px;
        span{
            font-family: 'Montserrat',sans-serif;
            font-style: normal;
            font-weight: 700;
            font-size: 14px;
            line-height: 17px;
            color: #FFFFFF;
            text-align: left;
            display: block;
            margin-bottom: 7px;
        }
        .v-from-buy-card-number,
        .v-from-buy-card-info{
            display: flex;
            justify-content: space-between;
            margin-bottom: 50px;
            input{
                font-family: 'Montserrat',sans-serif;
                font-style: normal;
                font-weight: 700;
                font-size: 14px;
                line-height: 17px;
                text-align: center;
                color: #FFFFFF;
                background: rgba(255,255,225,0.3);
                border: 1px solid #FFFFFF;
                box-sizing: border-box;
                border-radius: 8px;
                max-width: 70px;
                display: block;
                padding: 7px 15px;
                outline: none;
            }
        }
        .v-from-buy-card-info{
            margin-bottom: 0;
            input{
                padding: 7px 8px;
            }
        }
    }
</style>