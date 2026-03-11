<script setup>
import { ref } from 'vue';
import { plans } from '../script/plans.js'

// 預設第二張卡片選中
const selectedPlan = ref('professional')

// 從父組件App.vue接收定價模式
defineProps({
    pricingMode: {
        type: String,
        required: true
    }
})
</script>

<template>
    <legend class="sr-only">Select Plan</legend>
    <label v-for="plan in plans" 
    :key="plan.id" 
    class="plan-card" 
    :for="plan.id">

        <input class="sr-only card-radio" 
        type="radio" 
        :id="plan.id" 
        :value="plan.id"
        name="plan"
        :checked="plan.id === selectedPlan">

        <div class="card">
            <h2 class="card-title">{{ plan.title }}</h2>
            <p class="card-price"><span class="dollar-sign">&dollar;</span>{{ plan.price[pricingMode] }}</p>
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
.plan-card .card{
    position: relative;
    width: 350px;
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    padding: 30px;
    background-color: var(--price-card-background);
    border-radius: var(--card-border-radius);
    box-shadow: 20px 0px 50px  rgba(162, 166, 241,0.3);
    z-index: 1;
    transition: transform 0.3s ease; 
    user-select: none; /* 禁止文字選取 */
    margin: 0 3px;
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
    letter-spacing: 0.03em; 
    /* 切換不同瀏覽器及登入狀態發現，在某些狀態下文字會被擠壓拉長，故添加letter-spacing改善此狀況*/ 
    -webkit-font-smoothing: antialiased; /* 針對WebKit瀏覽器優化字體渲染 */
    -moz-osx-font-smoothing: grayscale; /* 針對Firefox優化字體渲染 */
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
}
.card .card-btn{
    border-top:1px solid var(--hr-color);
}
.card .card-btn .btn-more{
    border: 1px solid transparent;
    display: block;
    text-align: center;
    padding: 15px 0;
    margin-top: 30px;
    background: var(--more-btn-background);
    border-radius: var(--more-btn-border-radius);
    color: var(--more-btn-font-color);
    transition: all 0.5s ease-out;
}
/* learnmore btn hover效果 */
.card .card-btn .btn-more:hover{
    background: var(--more-btn-hover-background);
    color: var(--more-btn-hover-font-color);
    border: 1px solid var(--more-btn-hover-border);
}

/* 當卡片radio:checked時，card添加選中樣式 */
.plan-card .card-radio:checked + .card{
    margin: 0 10px 0 5px;
    background: var(--select-card-background);
    transform: scale(1.08);
    z-index: 10;
    transition: transform 0.5s ease;
}
.plan-card .card-radio:checked + .card .card-title,
.plan-card .card-radio:checked + .card .card-price
{
    color: var(--select-card-font-color);
}
.plan-card .card-radio:checked + .card .card-content,
.plan-card .card-radio:checked + .card .card-btn
{
    color: var(--select-card-font-color);
    border-top:1px solid var(--select-hr-color);
}
.plan-card .card-radio:checked + .card .card-btn .btn-more{
    background: var(--select-card-morebtn-background);
    color: var(--select-more-btn-font-color);
}
.plan-card .card-radio:checked + .card .card-btn .btn-more:hover{
    background: var( --select-card-background);
    color: var(--more-btn-font-color);
    border: 1px solid var(--select-more-btn-hover-border);
}

/* 價格卡片結束 */

/* RWD 卡片切換調整 */
@media (max-width: 768px){
    .plan-card .card-radio:checked + .card{
        margin: 0;
        transform: scale(1);
    }
}
</style>
