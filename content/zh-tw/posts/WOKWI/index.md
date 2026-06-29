---
slug: WOKWI
title: WOKWI
date: 2025-10-28 12:29:03
tags:

categories:
  - Note
---


WOKWI 電路模擬網站使用教學
==
WOKWI 電路模擬網站使用教學Wokwi有什麼特點呢？ 
即刻開始. https://wokwi.com/
* 無需使用實際的元器件或下載大型軟體。 wokwi在線網站可以提供你需要的一切！ 在這裡你可以用短時間去構建你的下一個物聯網專案。


1. 無需擔心犯錯誤.
您是不會損壞虛擬硬體的。 相信我們，我們都測試完畢了！ 所以不要擔心燒毀了你珍貴的元器件。 與真正的硬體不同，在這裡，你總是可以撤銷，你還有重來無數次的機會。


1. 尋找幫助和反饋非常簡單.
在這裡，你只需要分享你的Wokwi項目的連結，就可以方便的尋求説明。


1. 從你的代碼中獲得信心.
在這裡，硬體和軟體問題是分開的，不用擔心硬體的問題，專心你的軟體。


1. 不受約束的硬體.
再也不用從舊的專案中拆除元器件了，隨意的取用你需要使用的零件吧！ 你再也不用擔心項目的花費和元器件的庫存。


1. 開放的創客社區.
這是一個分享專案、尋求幫助和獲得靈感的地方！

1. 獨家提供——特色功能！ 
WiFi 模擬 - 模擬專案可以連接到互聯網。 您可以使用MQTT、HTTP、NTP和許多其他網路協定。
虛擬邏輯分析儀 - 在模擬中可以捕獲數位信號（例如UART、I2C、SPI）並在你的計算機上進行分析。
強力的GDB模擬 - 為高級使用者提供了強大的Arduino和Raspberry Pi Pico調試器。
SD卡模擬 - 可以使用代碼來存儲和檢索文件和目錄。 Club 會員也可以上傳二進位檔（例如圖像）。
.
改變連線的顏色
==

![](https://i.imgur.com/guffQ2s.png)

**這些鍵盤快捷鍵也可以在繪製新線時使用。 你也可以通過編輯[diagram.json](https://docs.wokwi.com/zh-CN/diagram-format#connections)檔來改變線的顏色。**

編輯器鍵盤快速鍵
==
![](https://i.imgur.com/YwhlH6v.png)
![](https://i.imgur.com/Otc2P5w.png)
![](https://i.imgur.com/cUPPnjl.png)

基礎使用
==

1.新增元件到 Wokwi模擬器
![](https://i.imgur.com/ujM2lj3.png)

按加按鈕，就可以選擇要新增的元件。

2.移動 Wokwi模擬器上的元件
![](https://i.imgur.com/P8U2zcO.png)

滑鼠左鍵點擊元件不放，就可以移動元件。

3.旋轉 Wokwi模擬器上的元件
![](https://i.imgur.com/X8OKoun.png)

點擊元件後，按鍵盤上的 R鍵。

4.刪除 Wokwi模擬器上的元件
![](https://i.imgur.com/WuOGdbs.png)

點擊元件後，看元件上的方框，按下 delete鍵。

5.連接 Wokwi模擬器上的元件
![](https://i.imgur.com/97hfan3.png)

滑鼠移到元件上，如果出現可以連接的腳位的話，會出現顯示腳位的方框，接下來再點擊一下元件上的腳位，就可以拉出電線。

6.電線轉彎
![](https://i.imgur.com/7LExz7i.png)

拉電線的時候，在要轉彎的方向點一下滑鼠左鍵，就可以把電線轉彎。

7.修改電線的顏色
![](https://i.imgur.com/lHhPsLG.png)

點擊拉好的電線，上方就會出現可以選擇的顏色

8.刪除電線
![](https://i.imgur.com/eKBas6d.png)

點擊電線後，按 delete。

9.常用快捷鍵
![](https://i.imgur.com/HRPeKxh.png)

常用的按鈕如上。

10.開啟零件更多說明
![](https://i.imgur.com/bQL8OMH.png)

點擊元件後，再點擊出現的問號。
也可以直接按鍵盤上的 ” / “。鍵

11.改 LED燈顏色
![](https://i.imgur.com/FYRn5Gx.png)

點擊左上的 diagram.json。
找到 led燈的代碼，修改 “attrs”下的顏色。

12.隱藏電線
![](https://i.imgur.com/QB8eGsO.png)

點擊左上的 diagram.json。
找到 “connection”，把連接兩個元件腳位的電線顏色，改為空白。

13.重新命名專案名稱
![](https://i.imgur.com/gQRRKVO.png)

點擊 Library Manager右方的箭頭。點擊 Rename。
改完名稱後，要記得存檔。

14.鏡射 LED燈
![](https://i.imgur.com/pfjZKu0.png)

點擊左上的 diagram.json。
在 “attrs”裡頭，新增一個 “flip” : “1”的屬性，1是水平鏡射。
這個翻轉的屬性，不是每個元件都可以用。

15.LED燈加標籤、按鈕加標籤
![](https://i.imgur.com/eiTldZM.png)

點擊左上的 diagram.json。
在 LED的 “arrts”中，新增 “label” : “顯示名稱”的屬性。
按鈕的作法也是一樣。
同樣，標籤這個屬性也是沒有辦法應用在每一個元件上。

16.專案儲存及分享
![](https://i.imgur.com/2h6GSSw.png)

1.點擊 SAVE按鈕。
2.點擊分享按鈕。
3.複製分享連結。
這個功能很方便，可以讓其它人看到我們拉的電線和程式碼。

17.修改電阻值

點擊左上的 diagram.json。
找到電阻的 “attrs”，修改 value的值就可以了。
修改完之後，模擬器上的電阻色碼顏色會跟著變動，很方便。
![](https://i.imgur.com/UyHdPdb.png)


支援的板子
==
![](https://i.imgur.com/bLMxtYc.png)

相關資料
==
wokwi社群
https://discord.com/invite/e5yFaayXkK
https://www.facebook.com/groups/wokwi
電阻色碼轉換器
https://www.digikey.tw/zh/resources/conversion-calculators/conversion-calculator-resistor-color-code