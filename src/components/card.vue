<script setup>
import { ref } from 'vue';
import { FocusTrap } from 'focus-trap-vue';


// 預設第二張卡片選中
const selectedPlan = ref('professional')

// 從父組件App.vue接收定價模式
defineProps({
    pricingMode: {
        type: String,
        required: true
    },
    plan: {
        type: Object,
        required: true
    }
})

const showModal = ref(false); // 控制模態框顯示狀態

</script>

<template>
    <legend class="sr-only">Select Plan</legend>
    <label class="plan-card" :for="plan.id">

        <input class="sr-only card-radio" 
        type="radio" 
        :id="plan.id" 
        :value="plan.id"
        name="plan"
        :checked="plan.id === selectedPlan"
        @change="selectedPlan = plan.id"
        :aria-label="`${plan.title}, ${plan.price[pricingMode]}`"
        >

        <div class="card">
            <h2 class="card-title">{{ plan.title }}</h2>
            <p class="card-price"><span class="dollar-sign">&dollar;</span>{{ plan.price[pricingMode] }}</p>
            <ul>
                <li class="card-content">{{ plan.storage }} Storage</li>
                <li class="card-content">{{ plan.users }} Users Allowed</li>
                <li class="card-content">Send up to {{ plan.send }} GB</li>
                <li class="card-btn">
                    <button type="button" 
                    class="btn-more" 
                    @click.prevent=" showModal = true"
                    aria-haspopup="dialog"
                    aria-expanded="showModal"
                    :tabindex="plan.id === selectedPlan ? 0 : -1"
                    :aria-label="`Learn more about the ${plan.title} plan`"
                    :aria-hidden="true"
                    >Learn More
                        <span class="sr-only">about the {{ plan.title }} plan</span>
                    </button>
                    
                    <!-- 點擊learn more按鈕跳出小視窗介紹專案 -->
                    <Teleport to="body">
                        <FocusTrap v-if="showModal" :active="true">
                            <div v-if="showModal" @click.self="showModal = false">
                                <div class="mask"></div>
                                <div class="learnmore" role="dialog" aria-modal="true" aria-labelledby="modal-title" aria-describedby="modal-description">
                                    <h2>{{plan.title}} Details</h2>
                                    <p>Lorem IpsumLorem IpsumLorem Ipsum</p>
                                    <button @click="showModal = false" class="btn-close" aria-label="Close">X</button>
                                </div>
                            </div>
                        </FocusTrap>
                    </Teleport>
                </li>
                
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
    width: 100%;
    text-decoration: none;
    text-align: center;
    padding: 15px 0;
    margin-top: 30px;
    background: var(--more-btn-background);
    border-radius: var(--more-btn-border-radius);
    color: var(--more-btn-font-color);
    transition: all 0.5s ease-out;
    font-family: inherit; 
    font-weight: var(--font-weight);
    font-size: 15px;
    letter-spacing: 0.04em;
    cursor: pointer;
}
.btn-more:focus-visible{
    box-shadow: 0 0 0 3px white, 0 0 0 6px hsl(237, 73%, 79%); 
    transition: box-shadow 0.2s ease;
    outline-color: var(--purple) ;
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

.card-radio:focus-visible + .card {
    box-shadow: 0 0 0 3px white, 0 0 0 6px hsl(237, 73%, 79%); 
    transition: box-shadow 0.2s ease;
}

/* learnmore置中 */
.learnmore{
    position: fixed;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
    z-index: 1000;
    background-color: var(--body-background);
    width: 300px;
    height: 200px;
    border-radius: 10px;
    padding: 20px;
    display: flex;
    justify-content: center;
    align-items: center;
    flex-direction: column;
    gap: 30px;
    box-shadow: 20px 0px 50px  rgba(162, 166, 241,0.3);
}


/* close-btn */
.btn-close{
    position: absolute;
    top: 10px;
    right: 10px;
    background: transparent;
    border: 1px solid transparent;
    font-size: 20px;
    cursor: pointer;
    color: var(--select-more-btn-font-color);
    padding: 10px;
    line-height: 1;
    width: 40px;
    height: 40px;
    border-radius: 50%;
    transition: all 0.2s;
}
.btn-close:hover{
    border: 1px solid var(--select-more-btn-font-color);
}
.btn-close:focus-visible{
    box-shadow: 0 0 0 3px white, 0 0 0 6px hsl(237, 73%, 79%); 
    transition: box-shadow 0.2s ease;
    outline-color: var(--purple) ;
}

/* mask */
.mask{
    position: fixed;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    background-color: rgba(0, 0, 0, 0.5);
    z-index: 999;
}


/* RWD 卡片切換調整 */
@media (max-width: 768px){
    .plan-card .card-radio:checked + .card{
        margin: 0;
        transform: scale(1);
    }
}
</style>
