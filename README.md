<!-- 這邊要插入demo -->

# Pricing component with toggle (Frontend Mentor Challenge)

[繁體中文](#繁體中文版) | [English](#english-version)

## 繁體中文版

## 可切換模式的定價組件(Pricing component with toggle)

這是一個來自Frontend Mentor的挑戰專案，專案重點在建立具備「月費／年費切換功能定價組件」以及「3種只可單選的定價模式卡」。

作品連結：[https://tina801005.github.io/vue-pricing-toggle/]

---

## 📍簡介

### 📂 專案架構

```text
src/
 ├── assets/          # 靜態資源與全域樣式
 │    ├── images/     # 背景裝飾圖與圖標
 │    └── *.css       # 樣式表管理
 ├── components/      # 可複用組件
 │    └── card.vue    # 定價方案卡片組件
 ├── script/          # 邏輯與數據處理
 │    └── plans.js    # 定價數據配置文件
 ├── App.vue          # 主程式與佈局控制
 └── main.js          # Vue 入口檔案
 ```

### 📎技術棧

* Framework: Vue3(Composition API)
* Build Tool: Vite
* Styling: CSS Variables, Flexbox, Mobile-first workflow
* Deployment: GitHub Pages (via gh-pages package)

---

## 📋說明

### 🎯主要功能

* 年費/月費即時切換
* 3張可選擇的定價卡片

### 💡技術亮點

* 無障礙設計：針對checkbox和radio的隱藏不使用display:none和visibility:hidden，改用"sr-only"隱藏。此方法既可實現隱藏效果也為螢幕閱讀器及鍵盤保留了操作性。

* 利用input:check來實現選中/切換效果：定價卡片使用radio、定價切換按鈕用checkbox來做，並使用input:check驅動css達成卡片選中及定價切換的效果，減少JavaScript對DOM的干預，讓整體跑起來更順暢。

* 模擬資料分離：將資料放在plans.js，透過資料驅動的方式動態渲染將資料組件放進相對應的位置中。框架與資料分離，保持區塊的乾淨，提高可維護性。未來若要新增新的定價模式直接在plans.js新增資料即可，增加擴展性。

### 🔍問題挑戰與解決方案

1. 狀況：價格文字拉長變形
   分析：發現在不同瀏覽器及登入狀態下，價格文字有被擠壓拉長的狀況
   解決：在不破壞主體視覺的條件下，針對價格添加letter-spacing加寬字距，並添加-webkit-font-smoothing及-moz-osx-font-smoothing。目前已測試edge和chrome皆有解決此狀況。

   ```CSS
    letter-spacing: 0.03em; 
    -webkit-font-smoothing: antialiased; /* 針對WebKit瀏覽器優化字體渲染 */
    -moz-osx-font-smoothing: grayscale; /* 針對Firefox優化字體渲染 */
   ```

2. 狀況：toggle在多次點擊後會反白
   解決：針對整個toggle區塊添加user-select:none;禁止反白；除此之外因定價卡片也有相同問題所以一併加上user-select:none; 進行UX優化。

3. 狀況：發佈後出現路徑404問題
   分析：GitHub Pages專案網址帶有子目錄，導致根路徑抓取失敗
   解決：
   * 在vite.config.js設定base路徑

   ```javascript
   plugins: [vue()],
   base: '/vue-pricing-toggle/'
   ```

    * 在package.json使用gh-pages套件建立自動化佈署流程
    * 回到GitHub Pages重設路徑為"gh-pages"即可修正狀況

### 😊結語

這是我第一個完全使用vue開發的專案。用vue開發和用html開發最大的不同就是在開始寫code之前要先計畫好，哪部分要放在app.vue當主體，哪部分可以拆出來做component，如果沒有事先計畫好，寫到後面很容易亂。
且我很感謝有遇到路徑404的這個狀況，這和以往發布純html網頁完全不同，讓我學到更多控制項。
在開發的同時我有使用Gemini，遇到不會寫或猶豫的地方，先條列出我認為可行的作法再提出來和Gemini討論共同找出最優解。

---

## 🧩安裝流程

### Project Setup

```sh
npm install
```

#### Compile and Hot-Reload for Development

```sh
npm run dev
```

#### Compile and Minify for Production

```sh
npm run build
```

##### [🔝 回到最上面](#pricing-component-with-toggle-frontend-mentor-challenge)

---

## English Version

## Pricing component with toggle

This is a challenge project from Frontend Mentor, focusing on creating a pricing component with a 'monthly/yearly toggle feature' and 'three types of pricing mode cards that can only be radio.'

Link：[https://tina801005.github.io/vue-pricing-toggle/]

## 📍Introduction

### 📂 Project Structure

```text
src/
 ├── assets/          # Static Assets & Global Styles
 │    ├── images/     # Background SVGs & Icons
 │    └── *.css       # Root variables, Reset, Main styles
 ├── components/      # Reusable Components
 │    └── card.vue    # Pricing Card Component
 ├── script/          # Logic & Data Management
 │    └── plans.js    # Data source for pricing plans
 ├── App.vue          # Main Application & Layout
 └── main.js          # Vue Entry Point
 ```

### 📎Tech Stack

* Framework: Vue3(Composition API)
* Build Tool: Vite
* Styling: CSS Variables, Flexbox, Mobile-first workflow
* Deployment: GitHub Pages (via gh-pages package)

---

## 📋Features

### 🎯Main Features

* Real-time yearly/monthly toggle
* 3 selectable pricing cards

### 💡Technical Highlights

* Accessibility (A11y): Instead of using display: none for checkboxes and radio buttons, I implemented the "sr-only" (screen-reader only) method. This ensures the component remains fully functional for screen readers and keyboard navigation while being visually hidden.

* CSS-Driven Interactions: By leveraging the :checked pseudo-class, I minimized JavaScript DOM manipulation. This approach ensures smoother transitions and better performance for the toggle and card selection states.

* Data-Driven Rendering: Pricing data is decoupled into plans.js. This separation keeps the template clean and significantly improves maintainability and scalability—adding new plans now only requires a simple update to the configuration file.

### 🔍Challenges & Solutions

1. Issue: Price text distortion and stretching
   Analysis: Found price text being compressed and distorted in different browsers and login states
   Solution: Added letter-spacing to widen character spacing without breaking the main visual design, and added -webkit-font-smoothing and -moz-osx-font-smoothing. Tested and resolved in both Edge and Chrome.

   ```CSS
    letter-spacing: 0.03em; 
    -webkit-font-smoothing: antialiased; /* Optimize font rendering for WebKit browsers */
    -moz-osx-font-smoothing: grayscale; /* Optimize font rendering for Firefox */
   ```

2. Issue: Toggle highlight after multiple clicks
   Solution: Added user-select:none to the entire toggle area and pricing cards to prevent text selection, improving UX.

3. Issue: 404 path error after deployment
   Analysis: GitHub Pages project URL contains a subdirectory, causing root path lookup failure
   Solution:
   * Set the base path in vite.config.js

   ```javascript
   plugins: [vue()],
   base: '/vue-pricing-toggle/'
   ```

    * Use gh-pages package in package.json to configure automated deployment workflow
    * Reset the path to "gh-pages" in GitHub Pages settings to resolve the issue

### 😊Conclusion

This is my first project built entirely with Vue. The key difference between developing with Vue versus pure HTML is the need to plan your structure upfront—deciding what goes in App.vue as the main component and what should be extracted into separate components. Without proper planning, the code can become messy quickly. I'm grateful for encountering the 404 path issue, as it taught me much more about deployment control compared to publishing pure HTML pages. During development, I used Gemini as a tool—when unsure about implementation approaches, I listed my ideas and discussed them with Gemini to find the optimal solution.

---

## 🧩Installation Steps

### Project Setup

```sh
npm install
```

#### Compile and Hot-Reload for Development

```sh
npm run dev
```

#### Compile and Minify for Production

```sh
npm run build
```

##### [🔝Back to top](#pricing-component-with-toggle-frontend-mentor-challenge)
