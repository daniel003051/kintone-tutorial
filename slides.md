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

## 注意事項
　
1. 不能使用 ESModule（ex: Vite）
2. 連結需要是 `https`


<div style="display: flex">
  <img src="https://www.svgrepo.com/show/374146/typescript-official.svg" style="width: 100px" > 
  <img src="https://www.svgrepo.com/show/374167/vite.svg" style="width: 100px" > 
  <img src="https://www.svgrepo.com/show/452092/react.svg" style="width: 100px" > 
  <img src="https://www.svgrepo.com/show/452130/vue.svg" style="width: 100px" > 
  <img src="https://www.svgrepo.com/show/452156/angular.svg" style="width: 100px" > 
</div>

---

## 如何上傳 JavaScript 檔案？

應用程式齒輪 > 設定 > 透過JavaScript/CSS自訂 

<img src="https://hackmd.io/_uploads/r1HxRHLuC.png" style="height: 80%">

---

## 快速建立專案

終端機輸入：`pnpm create krsb`


![](https://i.imgur.com/hepkCmr.png)

> https://www.npmjs.com/package/create-krsb


---

## kintone JavaScript API（事件）

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

## 事件的 event

```js
kintone.events.on('app.record.index.show', (event) => {
  console.log(event)
})
```

<v-click>
```js
{
  "type": "app.record.index.show",
  "appId": 193,
  "viewType": "list",
  "viewId": 20,
  "viewName": "（全部）",
  "records": [],
  "offset": 0,
  "size": 4,
  "date": null
}
```
</v-click>

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
- 🛠 **kintone.app.getHeaderSpaceElement** - 取得 header 的 DOM

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

## 範例：新增一個按鈕

```js
kintone.events.on('app.record.index.show', () => {
  // 取得 DOM
  const el = kintone.app.getHeaderMenuSpaceElement()
  // 建立 button 並 append
  const button = document.createElement('button')
  button.textContent = '按鈕'
  el.appendChild(button)
})
```

<v-click>

![](https://i.imgur.com/ka8qKUU.png)

</v-click>

<style>
code {
  font-size: 18px;
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
kintone.events.on('app.record.index.show', async () => {
  const response = await fetch('/k/v1/record.json?app=193&id=1', {
    headers: {
      'X-Cybozu-API-Token': 'Kgzg2TvnRvMLMve3ppd4abIKPKZoprADAKve04OI'
    }
  })
})
```

<style>
code {
  font-size: 18px;
}
</style>

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

## kintone 外部串接（Proxy）

即跨域，使用 Proxy 避開 CORS

```mermaid
sequenceDiagram
    participant kintone
    participant ProxyServer
    participant TargetServer

    kintone ->> ProxyServer: Request (API Call)
    ProxyServer ->> TargetServer: Forward Request
    TargetServer ->> ProxyServer: Response Data
    ProxyServer ->> kintone: Return Response
```

---

## kintone.proxy 語法 

使用 `kintone.proxy`，`response` 返回 `[body, status, headers]`

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

## 作業 1 - 自動編碼
　
1. 應用程式需要建立一個 ''自動編碼欄位''
2. 編碼內使用格式為 `YYYYMMDD-001`，再建一單變成 `YYYYMMDD-002`
3. 每天的值都是從 `YYYYMMDD-001` 開始

---

## kintone Plugin 製作

外掛與客製化不同的地方：

1. 外掛需要先打包成 zip 才能匯入
2. 能夠針對 APP 做設定（儲存資料）
3. 重復使用

---
layout: image-right
image: https://i.imgur.com/3odGn0X.png
backgroundSize: contain
---

## 如何安裝外掛

右上角齒輪 > kintone系統管理 > 外掛程式 > 匯入

---
layout: image-right
image: https://i.imgur.com/MDODKOP.png
backgroundSize: contain
---


## plugin 架構範例

不一定要是此架構，只要 `manifest.json` 指定檔案路徑即可。

範例程式碼：[連結](https://github.com/daniel003051/kintone-plugin-temp)

---
layout: image-right
image: https://i.imgur.com/uds60ha.png
backgroundSize: contain
---

## manifest.json

* 在 `desktop`、`mobile`、`config` 指定 JS 和 CSS 路徑。

* `config` 代表外掛設定頁面的檔案。

---

## 打包 plugin

使用 [@kintone/plugin-packer](https://www.npmjs.com/package/@kintone/plugin-packer) 打包 plugin。

```shell
{
  "scripts": {
    "package": "kintone-plugin-packer ./app --ppk private.ppk"
  }
}
```
<v-click>
參數：

* `--ppk`：指令打包後的 ppk 檔，若沒指定將會產生一個 ppk 檔案。
* `--out`：輸出的外掛檔名。
* `--watch`：監聽模式。
</v-click>

<style>
code {
  font-size: 20px;
}
</style>

---

## 關於 .ppk 檔案
　
1. 外掛打包用的私鑰，須自行保管
2. 每個外掛都有自己的 `.ppk`
3. 若外掛要更新版本，需要有 `.ppk` 檔，不然會視為打包一個新的外掛，並產生新的 `.ppk`

---

## 外掛可操作的方法
　
* 儲存外掛設定：**`kintone.plugin.app.setConfig`**
* 取得外掛設定：**`kintone.plugin.app.getConfig`**
* 儲存 Proxy 設定：**`kintone.plugin.app.setProxyConfig`**
* 取得 Proxy 設定：**`kintone.plugin.app.getProxyConfig`**

<br><br><br>

<v-click>
⚠️ setConfig 只能在外掛設定頁面調用
</v-click>

---

## 外掛的設定畫面
　
指的是 `html/index.html`、`js/config.js`、`css/config.css`

<img src="https://i.imgur.com/rhbWKYC.png" style="width: 100%">


---

## 取得應用程式欄位
　
1. 發送 API：[Get Form Fields](https://kintone.dev/en/docs/kintone/rest-api/apps/get-form-fields/)
2. 設定至外掛 config：[kintone.plugin.app.setConfig](https://cybozu.dev/zh-tw/kintone/docs/js-api/plugins/set-config/)
3. 於客製化頁面中取得外掛設定：[kintone.plugin.app.getConfig](https://cybozu.dev/zh-tw/kintone/docs/js-api/plugins/get-config/)

運用此方法，不用將欄位名稱寫死在 `.JS`，可讓使用者自由指定欄位名稱。

---

## 隱藏 token 資訊
<br>

1. 預先在 [plugin proxy config](https://cybozu.dev/zh-tw/kintone/docs/js-api/plugins/get-config-for-proxy/) 中設定 headers 等資訊
2. 在 customize.js 中調用 [Plugin Proxy Request](https://cybozu.dev/zh-tw/kintone/docs/js-api/plugins/kintone-plug-in-proxy/)
<br><br>
```mermaid
graph LR;
    A[設定 Plugin Proxy Config] --> B[調用 Plugin Proxy Request]
```


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

