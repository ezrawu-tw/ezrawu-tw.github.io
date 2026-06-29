---
slug: Tinkercad
title: Tinkercad
date: 2025-10-28 12:22:27
tags:
- CAD
categories:
  - Note
---


Tinkercad 線上3D軟體介紹
==
連結：
https://www.tinkercad.com/login?next=%2Fthings%2FgyAdNPIC5oD-incredible-leelo%2Fedit

第一次使用者!


![](https://i.imgur.com/rSRZUjw.png)

點選Persoal account


功能介紹：
1. 設計Arduino電路
2. 3D列印模型設計

設計Arduino電路
==

![](https://i.imgur.com/nosivTs.png)
設計你要測試的線路(這邊使用官方給的範例)
CODE也可以直接測試

在Tinkercad網站註冊帳號並登入之後，點擊Circuits（電路），再按下「建立新電路」：
![](https://i.imgur.com/oEtYESX.png)

從右邊的「元件」面板，拖放一個小型電路試驗板，並選擇性地替它命名成「麵包板」。
![](https://i.imgur.com/O9cZCkj.png)

![](https://i.imgur.com/Qwbsste.png)
拖放一個LED到麵包板，正極（凸出的那一面）腳與電阻相連：
![](https://i.imgur.com/8SsqUh4.png)


![](https://i.imgur.com/bgRMTqL.png)
按一下LED元件，然後按著Shift鍵不放，再按一下電阻，可選取兩個元件。按下Ctrl和C鍵複製，再按下Ctrl和V鍵便能貼上剛剛複製的電阻和LED。重複按下Ctrl和V鍵、調整元件位置，完成如下的麵包板電路：
![](https://i.imgur.com/tGBvqxT.png)

LED來回跑馬燈的Arduino程式
==
按一下「程式碼」鈕，從下拉式選單選擇「文字」式程式碼：
![](https://i.imgur.com/fMudGik.png)
在程式碼編輯器中輸入LED跑馬燈程式：
![](https://i.imgur.com/zSh0SWx.png)

```
const byte LEDs[] = {8,9,10,11,12};
const byte total = sizeof(LEDs);
int8_t index = 1;
byte i = 0;

void setup() {
  for (byte i=0; i<total; i++) {
    pinMode(LEDs[i], OUTPUT);
    digitalWrite(LEDs[i], LOW);
  }
}

void loop() {
  digitalWrite(LEDs[i], HIGH);
  delay(100);
  digitalWrite(LEDs[i], LOW);

  i += index;
  
  if (i < 0 || i >= total) {
      index *= -1;   // 原本的1變成-1
      i += (index*2);
  }
}

```



3D列印模型設計
==

預設庫
![](https://i.imgur.com/l0k7xoi.png)

1. 畫面介紹
![](https://i.imgur.com/8M3w9D4.png)
2. 滑鼠功能
請從零件區，拉一個正方形出來，測試滑鼠的功能
![](https://i.imgur.com/O3FvLGy.png)
![](https://i.imgur.com/bjOAGOB.png)
3. 單一方向的移動 滑鼠+Shift
![](https://i.imgur.com/ZrwBZbB.png)
![](https://i.imgur.com/PgUHasS.png)


4. 畫面的角度控制
![](https://i.imgur.com/elL4m2Z.png)
![](https://i.imgur.com/lIPWuKn.png)
![](https://i.imgur.com/OZB4HE8.png)
5. 等比例縮放物件 Shift+白點
![](https://i.imgur.com/7u096xV.png)

6. 中心點位置不變 Alt+白點
![](https://i.imgur.com/rGnSnf6.png)
![](https://i.imgur.com/hkXS4ng.png)
![](https://i.imgur.com/1aYIE4L.png)


7. 對齊
![](https://i.imgur.com/njXtJS6.png)
![](https://i.imgur.com/MFEKgJm.jpg)
![](https://i.imgur.com/3MLlXar.png)
![](https://i.imgur.com/Bes8bca.png)
![](https://i.imgur.com/fQcB6n7.png)
![](https://i.imgur.com/YPagMPO.png)
![](https://i.imgur.com/46jgjKH.png)


8. 組合、分解
![](https://i.imgur.com/7fqUgFU.png)
![](https://i.imgur.com/QIG6ZSL.png)
![](https://i.imgur.com/7D3GhVJ.png)

9. 挖洞開孔、切割

![](https://i.imgur.com/fVYAcsH.png)
![](https://i.imgur.com/F3vwvt5.png)
![](https://i.imgur.com/aV5MJfj.png)
![](https://i.imgur.com/xdyD10g.png)
![](https://i.imgur.com/LW8X8q9.png)



10. QR二維碼

![](https://i.imgur.com/aou4upG.png)
![](https://i.imgur.com/45CQkPU.png)


3d模型匯出
==


按Export 匯出選STL檔
![](https://i.imgur.com/9tm08U7.png)
