<script setup>
import { plans } from '../script/plans.js'

</script>

<template>
    <legend>Select Plan</legend>
    <label v-for="plan in plans" 
    :key="plan.id" 
    class="plan-card" 
    :for="plan.id">

        <input class="sr-only" 
        type="radio" 
        :id="plan.id" 
        :value="plan.id" 
        name="plan">

        <div class="card">
            <h2 class="card-title">{{ plan.title }}</h2>
            <p class="card-price"><span class="dollar-sign">&dollar;</span>{{ plan.price.monthly }}</p>
            <ul>
                <li class="card-content">{{ plan.storage }} Storage</li>
                <li class="card-content">{{ plan.users }} Users Allowed</li>
                <li class="card-content">Send up to {{ plan.send }} GB</li>
                <li class="card-btn"><a href="#" class="btn-more">Learn More</a></li>
            </ul>
            
        </div>
    </label>
</template>

<style scoped>
/*價格卡片開始*/
.pricing-area legend{
    display: none;
}
/* 隱藏radio小圓圈 */
/* 不直接使用display:none和visibility: hidden;
是因為前者會影響鍵盤控制，後者隱藏但會佔空位，所以用這個sr-only的方式
畫面上看起來隱藏了但鍵盤滑鼠依然能控制選取 */
.plan-card .sr-only{
    position: absolute;
    width: 1px;
    height: 1px;
    padding: 0;
    margin: -1px;
    overflow: hidden;
    clip: rect(0,0,0,0);
    white-space: nowrap;
    border: 0;
}
.plan-card .card{
    position: relative;
    width: 350px;
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    gap: 0;
    padding: 30px;
    background-color: var(--price-card-background);
    border-radius: var(--card-border-radius);
    box-shadow: 0 30px 50px -15px rgba(162, 166, 241,0.2);
    z-index: 1;
}

/* card title */
.card .card-title{
    color: var(--card-font-color);
    font-size: var(--card-title-font-size);
    margin-bottom: 40px;
}
/* card price */
.card .card-price{
    color: var(--card-font-color);
    font-size: var(--card-price-font-size);
    margin-bottom: 40px;
    display: flex;
    justify-content: center;
    align-items: center;
}
.card .card-price .dollar-sign{
    font-size: var(--card-dollarsign-size);
    margin-right: 8px;
}

/* card content */
.card .card-content{
    color: var(--card-font-color);
    font-size: var(--card-content-font-size);
    padding: 18px 94px;
    white-space: nowrap;
    border-top:1px solid var(--hr-color);
    /* border-bottom:1px solid var(--hr-color); */
    /* border: 1px solid red; */
}
.card .card-btn{
    border-top:1px solid var(--hr-color);
    /* margin-top: 20px; */
}
.card .card-btn .btn-more{
    border: none;
    display: block;
    text-align: center;
    padding: 15px 0;
    margin-top: 30px;
    background: var(--more-btn-background);
    border-radius: var(--more-btn-border-radius);
    color: var(--more-btn-font-color);
    /* display: inline-block;
    padding: 10px 20px;
    background-color: var(--card-btn-background);
    color: var(--card-btn-font-color);
    text-decoration: none;
    border-radius: 5px;
    transition: background-color 0.3s ease; */
}
/* 價格卡片結束 */
</style>