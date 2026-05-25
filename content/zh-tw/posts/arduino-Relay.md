---
slug: arduino-Relay
title: arduino_Relay
date: 2025-10-28 12:17:54
tags:

- Arduino

categories:
  - Note

---
slug: arduino-Relay

Arduino繼電器介紹
==

![](https://hackmd.io/_uploads/SyiMqqeB2.png)

Arduino Uno只能提供5V或3.3V的直流電給外部設備，若是我們需要更高電壓或是交流電，
像是要控制電風扇、檯燈，這時就必須靠繼電器(Relay)了。繼電器開關一樣，
我們可以從程式去控制通電或斷電，如果你想做智慧家電，一定少不了繼電器！

![](https://hackmd.io/_uploads/ryqr9qlSh.png)

常見的是1路
此外還有 2 4 8 路繼電器

### 4路

![](https://cdn.discordapp.com/attachments/625953483576705024/763276251917582366/DSC_0256.JPG)



### 使用說明
繼電器會把它的容許電壓、電流印在上面，AC就是交流電，像是10A 125V AC。但有不少沒有印DC直流電的，一般來說，就算沒有印出來，直流在12V、2A內是沒什麼問題的。但如果要長期使用，建議還是買有明確印出數值的款式。

繼電器一般會分兩邊，一邊各3個接腳。PIN腳的那邊是用來和Arduino溝通的，+就是VCC，-就是GND，IN則是訊號線，我們可以透過這個訊號線來控制繼電器的開或關。

另一邊則是電源線的接腳：

NO：Normal Open，常開，也就是正常情況它是不通電的。
COM：Common Ground，共接電，很多人習慣把外電接到這個接腳，再從NO或NC接到外部設備上。
NC：Normal Close，常閉，它在正常情況下是接通的。

NO和NC一次只會選擇接一個，至於要接哪一個，就要看實際的情況了

