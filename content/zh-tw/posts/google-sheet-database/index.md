---
slug: google-sheet-database
title: google_sheet_database
date: 2025-10-28 12:23:53
updated: 
tags:
- google 
categories:
  - Note
---


# 如何用 Google Sheets / Excel 當作資料庫？

1. 建立 Google Excel
2. 設定的假資料欄位 (欄位名稱的部份要用英文)
* id：流水號
* name：姓名
* image：圖片
* email：信箱
* phone：電話

**特別注意下面要求的表單是指(工作表一)不是DB**
![](https://i.imgur.com/N1vHWEx.png)


3. 發佈 Google Excel 到網路
*  Demo 因為只有一張表，所以直接用「整份文件」，如果是有很多張表，但限制其中幾張是可以抓的，就選擇可以公開的表即可。

(點選發佈到網路上) 按發布


4. 接著記得將表單的「檢視」權限開放給知道連結的任何人，以免後面步驟因權限不足而被阻擋。 這邊的連結(才是後面才要的格式，就是複製連結按下去)

![](https://i.imgur.com/oyv4FR3.png)

取得 Google API Key
==

1. GCP 新增新專案
沒有專案的才需要這步，進到 Google Cloud Platform 的頁面按下新增專案，取好專案名稱後即可新增。

2. 開通 Google Sheets API 功能
有了 GCP 的專案後，進到 API 程式庫：https://console.cloud.google.com/apis/library?hl=zh-TW

搜尋欄中搜尋「sheet」，會看到一項「Google Sheets API」：
![](https://i.imgur.com/nSgWAp0.png)
點擊後按下「啟用」，專案就會開通 Google Sheets API 的功能：
![](https://i.imgur.com/6Ps757J.png)
啟用完成，頁面會回到 GCP 的頁面，可以看到上面一條訊息提醒要有憑證才能使用 API：

直接點擊「建立憑證」，或是打開網址：https://console.cloud.google.com/apis/credentials/wizard?hl=zh-TW

3. 建立憑證
建立憑證的第一步要先做一些選擇：
![](https://i.imgur.com/GgjLWkQ.png)
「選取 API」，選擇「Google Sheets API」。
「您需要存取什麼資料？」，這段看了 說明文件 也看不太懂使用的情境，選擇「應用程式資料」就可以。

「您打算將這個 API 與 Compute Engine、Kubernetes Engine、App Engine 或 Cloud Functions 搭配使用嗎？」，本篇只是為了要能夠取得 Google Sheets 中的資料，並不會用到上述的功能，選擇「不，我不會使用任何一項憑證」。

接著按「下一步」。

下一步是填寫我們建立這個帳戶的資料，填寫成我們之後回頭來看時，看得懂要做什麼的資訊就可以：
![](https://i.imgur.com/9kpTubt.png)
填寫完後按下「建立並繼續」。

後面二項是選填，不用設定也沒關係，按下「完成」。

4. 建立 API 金鑰
上一步完成後，頁面會回到 憑證的頁面，點擊上方的「建立憑證」，選擇「API 金鑰」：
![](https://i.imgur.com/ce31aaN.png)
幾秒後，就會看見跳出一個小視窗，上面寫了「您的 API 金鑰」，這個金鑰也就是我們要取 Google Sheets 時後面要附上的：

![](https://i.imgur.com/mj5sTgE.png)

視窗上面也提醒了，為了怕金鑰被外人拿到也可以用，我們必須要對這組金鑰加上限制，點擊「限制金鑰」就會進入設定的頁面。

建議一定要設定限制，本篇的 Demo 有限制只有在 Demo 頁下才有效，而且也只能用 Google Sheets API 的功能。

有了 API 金鑰，接著就是用新的 URL 去執行 GET。

Google Sheets URL V4 版的 URL 規則如下：
==

```
https://sheets.googleapis.com/v4/spreadsheets/{表單id}/values/{sheet名稱}?alt=json&key={API金鑰}
```
* {表單id}：表單的網址上就可以看到。 
>共用連結中的ID不是發布的連結
* {sheet名稱}：就是每一張試算表的名稱，預設會是叫「工作表1」，這邊有測試過，有支援中文。
* {API金鑰}：就是上一段我們從 GCP 上取得的金鑰。
我們用一個簡單的 fetch 來取：
```
 fetch('https://sheets.googleapis.com/v4/spreadsheets/1JD19NEjYZNXuML_AX4G9Tg3SmQ8r9O7rayQNEkt_uq0/values/%E5%B7%A5%E4%BD%9C%E8%A1%A81?alt=json&key={api key}')
        .then(res => res.json())
        .then(res => {
          console.log(res)

```
實際測試結果
![](https://i.imgur.com/2msBaqR.png)

本篇的相關連結：
> Google Sheet 
https://docs.google.com/spreadsheets/d/1JD19NEjYZNXuML_AX4G9Tg3SmQ8r9O7rayQNEkt_uq0/edit?usp=sharing


