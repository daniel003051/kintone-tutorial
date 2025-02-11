---
theme: seriph
background: https://cover.sli.dev
title: Welcome to Slidev
info: |
  ## Slidev Starter Template
  Presentation slides for developers.

  Learn more at [Sli.dev](https://sli.dev)
class: text-center
drawings:
  persist: false
transition: slide-left
mdc: true
---

# kintone API 概要說明

kintone Consulting Service

日商才望子股份有限公司 

---
src: ./pages/intro.md
---

---

## kintone JavaScript API

事件

```js
kintone.events.on('app.record.index.show', (event) => {
  // 要做的事情 ...
})
```

就像是…

```js 
button.addEventListener('click', () => {
  // 要做的事情 ...  
})
```

<style>
code {
  font-size: 20px;
}
</style>

---

## 較常使用的 kintone JavaScript API

kinrone JavaScript API(事件)

- 🛠 **app.record.index.show** 紀錄列表頁面
- 🛠 **app.record.detail.show** 紀錄詳細頁面
- 🛠 **app.record.create.show** 紀錄添加頁面
- 🛠 **app.record.create.change.<欄位代碼>**
- 🛠 **app.record.create.submit** 紀錄新增按鈕觸發

<v-click>

```js
// 範例 ...
kintone.events.on('app.record.create.submit', (event) => {
  // 要做的事情 ...
})
```
</v-click>

<div class="abs-br m-6 text-xl">
  <a href="https://cybozu.dev/zh-tw/id/9744d83c79ac1b73e5cab2c7/#記錄清單畫面" target="_blank" class="slidev-icon-btn">
    <carbon:link />
  </a>
</div>

<style>
code {
  font-size: 20px;
}
</style>

---

## 較常使用的 kintone JavaScript API

kinrone JavaScript API(方法)

- 🛠 **kintone.app.record.getId** - 取得紀錄 id
- 🛠 **kintone.app.getId** - 取得 app id
- 🛠 **kintone.app.record.get** - 取得當前紀錄
- 🛠 **kintone.app.record.set** - 設定當前紀錄
- 🛠 **kintone.getLoginUser** - 取得登入者資料

<v-click>

```js
// 範例 ...
const APP_ID = kintone.app.getId()
const RECORD_ID = kintone.app.record.get()
```

</v-click>

<div class="abs-br m-6 text-xl">
  <a href="https://cybozu.dev/zh-tw/id/9744d83c79ac1b73e5cab2c7/#get-set" target="_blank" class="slidev-icon-btn">
    <carbon:link />
  </a>
</div>

<style>
code {
  font-size: 20px;
}
</style>

---

## kintone REST API

分以下幾種

* 應用程式
* 記錄
* 空間
* 檔案
* 外掛程式
* API資訊

<div class="abs-br m-6 text-xl">
  <a href="https://cybozu.dev/zh-tw/kintone/docs/rest-api/" target="_blank" class="slidev-icon-btn">
    <carbon:link />
  </a>
</div>

---

## kintone REST API 範例

|  |  |  |
| -------- | -------- | -------- |
| 「取得」單個記錄     | `GET`     | /k/v1/record.json     |
| 「新增」單條記錄     | `POST`     | /k/v1/record.json     |
| 「更新」單個記錄     | `PUT`     | /k/v1/record.json     |

```js
(async () => {
  const response = await fetch('/k/v1/records.json', {
    // ....
  })
})()
```

---

## 調用 API 的權限

分為以下兩種：

```js
// 帳號密碼轉 base64
headers: {
  'X-Cybozu-Authorization': 'cXFxcWVzOjI0ZmRnZGZhYQ=='
}

// 應用程式中的 token
headers: {
  'X-Cybozu-API-Token': 'Kxw76467FlFgjDkQ4jZtpgPFGKcA7y6s5fNn0M0x'
}
```

<style>
code {
  font-size: 18px;
}
</style>

---

## 呼叫外部 API

即跨域，使用 Proxy 避開 CORS

```js
try {
  const [body, status, headers] = await kintone.proxy(
    'https://api.example.com',
    'GET',
    {},
    {}
  );
  // success
  console.log(status, body, headers);
} catch (error) {
  // error
  console.log(error); // 顯示代理 API 的回應正文（字串）
}
```

<div class="abs-br m-6 text-xl">
  <a href="https://cybozu.dev/zh-tw/kintone/docs/js-api/proxy/kintone-proxy/" target="_blank" class="slidev-icon-btn">
    <carbon:link />
  </a>
</div>


<style>
code {
  font-size: 18px;
}
</style>

---

## js-sdk

![](https://hackmd.io/_uploads/H1GQ1mR_0.png)

<div class="abs-br m-6 text-xl">
  <a href="https://hackmd.io/_uploads/H1GQ1mR_0.png" target="_blank" class="slidev-icon-btn">
    <carbon:link />
  </a>
</div>

---

## 參考資料
　
* [Cybozu Developer Network](https://cybozu.dev/zh-tw/kintone/)
* [Cybozu Developer Network（CN）](https://cybozudev.kf5.com/hc/)
* [iT邦幫忙 Cybozu台灣](https://ithelp.ithome.com.tw/users/20170470/articles)
* [iThome 鐵人賽 | kintone 娛樂城](https://ithelp.ithome.com.tw/2024ironman/signup/team/336)
* [Qiita](https://qiita.com/search?q=kintone&sort=created)
* [js-sdk](https://github.com/kintone/js-sdk)

---

## 注意事項
.
1. 不能使用 ESModule（ex: Vite）

