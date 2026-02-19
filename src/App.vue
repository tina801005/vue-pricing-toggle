<script setup></script>

<template>
    <!-- 頁面標題 開始 -->
    <h1 class="title">Our Pricing</h1>
    <!-- 頁面標題結束 -->
    
    <!-- 定價模式切換按鈕 開始 -->
    <div class="pricing-model">
        <p>Annually</p>
        <label for="toggle" class="toggle">
            <input type="checkbox" name="" id="toggle">
            <div class="btn-toggle"></div>
        </label>
        <p>Monthly</p>
    </div>
    <!-- 定價模式切換按鈕 結束 -->
    
    <!-- 價格卡片 開始 -->
    <section class="pricing-area">
        <div class="card card-basic">
            
        </div>
        <div class="card card-pro">
            
        </div>
        <div class="card card-master">

        </div>
    </section>
    <!-- 價格卡片 結束 -->
</template>

<style scoped>
/* 頁面標題 開始 */
.title{
    border: 1px solid blue;
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
    border: 1px solid red;
}
.toggle{
    margin: 0 25px;
}
.pricing-model p{
    color: var(--switch-font-color);
}
.btn-toggle{
    width: 60px;
    height: 25px;
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
    transition: margin-left 0.2s;
}
input:checked + .btn-toggle::before{
    margin-left: 35px;
}
input{
    display: none;
}
/* 定價按鈕區塊 結束 */

/* 價格卡片開始 */
.pricing-area{
    margin-top: 65px;
    background-color: skyblue;
    width: inherit;
    height: 420px;
}
.card{
    width: ;
}
/* 價格卡片結束 */
</style>