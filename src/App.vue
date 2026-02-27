<script setup>
import Card from './components/card.vue';

</script>

<template>
    <section>
        <!-- 頁面標題 開始 -->
        <h1 class="title">Our Pricing</h1>
        <!-- 頁面標題結束 -->
    
        <form>
            <!-- 定價模式切換按鈕 開始 -->
            <div class="pricing-model">
                <p>Annually</p>
                <label for="toggle" class="toggle">
                    <input type="checkbox" id="toggle" class="billing-toggle">
                    <div class="btn-toggle"></div>
                </label>
                <p>Monthly</p>
            </div>
        <!-- 定價模式切換按鈕 結束 -->
        
        <!-- 價格卡片 開始 -->
        <!-- 此處為雛形，尚須改善。
        改善方向：
        1. fieldset>label>input+div，
        2. legend隱藏，
        3. input原使用隱藏為display:none;改為visiable:hiddle; -->

        <!-- 從card引入連結 -->
        <fieldset class="pricing-area">
            <Card>
                <slot></slot>
            </Card>
        </fieldset>
        </form>
        
    </section>
    <!-- 價格卡片 結束 -->
</template>

<style scoped>
/* 頁面標題 開始 */
.title{
    display: grid;
    place-items: center;
    color:var(--page-title-font-color);
    font-size: var(--page-title-font-size);
    margin-bottom: 40px;
}
/* 頁面標題 結束 */

/* 價格切換按鈕區塊 開始*/
.pricing-model{
    display: flex;
    justify-content: center;
    align-items: center;
}
.toggle{
    margin: 0 25px;
}
.toggle .billing-toggle{
    display: none; 
}
.pricing-model p{
    color: var(--switch-font-color);
}
.btn-toggle{
    width: 60px;
    height: 35px;
    border-radius: 20px;
    background: var(--switch-background);
    position: relative;
    padding: 5px;
}
.btn-toggle::before{
    content:"";
    position: absolute;
    width: 25px;
    height: 25px;
    background-color: #fff;
    border-radius: 50%;
    top: 0;
    left: 0;
    transform: translateX(5px) translateY(5px);
    transition: margin-left 0.2s;
}
.toggle .billing-toggle:checked + .btn-toggle::before{
    margin-left: 25px;
}

/* 定價按鈕區塊 結束 */
.pricing-area{
    margin-top: 65px;
    width: inherit;
    height: 455px;
    display: flex;
    justify-content: center;
    align-items: center;
    border: none;
}
</style>