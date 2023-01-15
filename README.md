
# Unnotech Frontend Engineer 徵才小專案-林志謙

這是一個小型的徵才專案，會需要你使用 Vue 和 API 所提供的資料，依照 wireframe 來完成頁面。

## 技術選型
package manage
- [Vue 3](https://cn.vuejs.org/)
    - TypeScript
    - scss
    - Composition API + script setup
- [Vite](https://cn.vitejs.dev/guide/)
- [Nuxt3](https://nuxt.com/)
- yarn


## 專案的架構、邏輯說明
- 專案架構採用nuxt3整體架構可直接參考[Nuxt 3 documentation](https://nuxt.com/docs/getting-started/introduction)
- pages
  - Book List Page (網址: `/books`)
     - pages/books/index.vue 顯示Book List頁面順便在此頁面定義booksInfo type 方便後續打api時
  - Book Detail Page (網址: `/books/:bookId`)
     - pages/books/[id].vue 顯示書籍基本資訊
  - Book Add Page (網址: `/books/add`)
     - pages/books/add.vue 顯示新增書籍頁面
 
 - components
    - 共用元件就直接放在components內
      - VTextInput 包裝vee-validate元件
    - 屬於books頁面的元件歸類在components/books資料夾內
      - BooksHeader
        - 樣式基本上大致上就是有左中右三個區塊所以先用3個slot切分保留未來彈性
      - BooksCard顯示書籍基本資料
        - title名稱過長會省略文字(使用tailwindcss 的truncate)
      - BooksDetailInfo顯示基本書籍資訊
      - BooksForm 顯示新增書籍跟修改書籍使用的表單
        - 新增跟修改板型基本上一致，透過props  editFlag做切換功能

## 你對於所有使用到的第三方 library 的理解，以及為何使用它
  - nuxt3
    - 基於vue3的框架，因為有一些蠻方便的基本功能，可省略掉很多設定與造輪子的工，故使用
  - vee-validate
    - 為了處理表單驗證的部份故採用此第三方套件，且有支援vue3
  - tailwindcss
    - 一款基於Atomic CSS概念的css框架，由於之前沒用過故此小專案來試用看看
    - 此次僅用到很基本的樣式功能而已，其他客製化的設定此次並沒有玩到
  - fontawesome 
    - 可自由縮放而不會出現鋸齒
    - 可自由改變顏色或粗、斜體
    - 提供上千種 icon，省去自製的時間
  
  
## 在這份專案中你遇到的困難、問題，以及解決的方法
```
  此專案原本想用nuxt3+vuetify3來解決，但想說用些沒用過的第三方套件來試看看
  vuetify3提供的基本css樣式其實跟tailwindcss能提供的基本樣式差不多
  一樣都能透過class flex、pa-2、mt-0之類的css名稱直接使用樣式
  一方面是想試看看tailwindcss，故此次故意不使用vuetify3
  所以表單驗證的部份也採用vee-validate這個套件
  其實主要多花的時間是看文件，跟實驗套件功能，看能否用套件提供的功能完成
  vee-validate的套件功能蠻強大的，故花了比較多的時間實驗能符合需求的元件跟api
```

##我們該如何執行你完成的專案

Look at the [Nuxt 3 documentation](https://nuxt.com/docs/getting-started/introduction) to learn more.

## Setup

Make sure to install the dependencies:

```bash
# yarn
yarn install

# npm
npm install

# pnpm
pnpm install --shamefully-hoist
```

## Development Server

Start the development server on http://localhost:3000

```bash
npm run dev
```

## Production

Build the application for production:

```bash
npm run build
```

Locally preview production build:

```bash
npm run preview
```

Check out the [deployment documentation](https://nuxt.com/docs/getting-started/deployment) for more information.
