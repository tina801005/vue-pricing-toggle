<script setup></script>

<template>
    <section class="pricing-area">
        <!-- 頁面標題 開始 -->
        <h1 class="title">Our Pricing</h1>
        <!-- 頁面標題結束 -->
    
        <form>
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
        <!-- 此處為雛形，尚須改善。
        改善方向：
        1. fieldset>label>input+div，
        2. legend隱藏，
        3. input原使用隱藏為display:none;改為visiable:hiddle; -->
        
            <fieldset>
                <legend>123</legend>
                <div class="card">
                    <input type="radio" id="basic" value="basic" name="plan">
                    <label for="basic">
                        <h2>Basic</h2>
                        <p><span>&dollar;</span>19.99</p>
                        <p>500 GB Storage</p>
                        <p>2 Users Allowed</p>
                        <p>Send up to 3 GB</p>
                        <a href="#">Learn More</a>
                    </label>
                </div>
                <div class="card">
                    <input type="radio" id="professional" value="professional" name="plan">
                    <label for="professional">
                        <h2>Professional</h2>
                        <p><span>&dollar;</span>24.99</p>
                        <p>1 TB Storage</p>
                        <p>5 Users Allowed</p>
                        <p>Send up to 10 GB</p>
                        <a href="#">Learn More</a>
                    </label>
                </div>
                <div class="card">
                    <input type="radio" id="master" value="master" name="plan">
                    <label for="master">
                        <h2>Master</h2>
                        <p><span>&dollar;</span>39.99</p>
                        <p>2 TB Storage</p>
                        <p>10 Users Allowed</p>
                        <p>Send up to 20 GB</p>
                        <a href="#">Learn More</a>
                    </label>
                </div>
            </fieldset>
        </form>
        
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
/*  
input{
    display: none;
}*/
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