---
slug: Tinkercad
title: Tinkercad
date: 2025-10-28 12:22:27
tags:
- CAD
categories:
  - Note
---
slug: Tinkercad

Introduction to Tinkercad — Online 3D Software
==
Link:
https://www.tinkercad.com/login?next=%2Fthings%2FgyAdNPIC5oD-incredible-leelo%2Fedit

First-time users!


![](https://i.imgur.com/rSRZUjw.png)

Click **Personal account**.


Features:
1. Design Arduino circuits
2. 3D printing model design

Designing Arduino Circuits
==

![](https://i.imgur.com/nosivTs.png)
Design the circuit you want to test (this example uses the official sample provided).
You can also test the CODE directly.

After registering and logging in to the Tinkercad website, click **Circuits**, then press **Create new circuit**:
![](https://i.imgur.com/oEtYESX.png)

From the **Components** panel on the right, drag and drop a small breadboard onto the canvas, and optionally rename it "Breadboard".
![](https://i.imgur.com/O9cZCkj.png)

![](https://i.imgur.com/Qwbsste.png)
Drag and drop an LED onto the breadboard so that its positive leg (the longer, protruding side) connects to the resistor:
![](https://i.imgur.com/8SsqUh4.png)


![](https://i.imgur.com/bgRMTqL.png)
Click an LED component, then hold Shift and click the resistor to select both components. Press Ctrl+C to copy, then Ctrl+V to paste the copied resistor and LED. Keep pressing Ctrl+V and adjusting component positions to complete the breadboard circuit as shown below:
![](https://i.imgur.com/tGBvqxT.png)

LED Back-and-Forth Chaser Program for Arduino
==
Click the **Code** button, then select **Text** from the dropdown menu:
![](https://i.imgur.com/fMudGik.png)
Enter the LED chaser program in the code editor:
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
      index *= -1;   // changes from 1 to -1
      i += (index*2);
  }
}

```



3D Printing Model Design
==

Default library
![](https://i.imgur.com/l0k7xoi.png)

1. Interface overview
![](https://i.imgur.com/8M3w9D4.png)
2. Mouse controls
Drag a cube out from the parts panel to test the mouse controls.
![](https://i.imgur.com/O3FvLGy.png)
![](https://i.imgur.com/bjOAGOB.png)
3. Single-axis movement — Mouse + Shift
![](https://i.imgur.com/ZrwBZbB.png)
![](https://i.imgur.com/PgUHasS.png)


4. View angle control
![](https://i.imgur.com/elL4m2Z.png)
![](https://i.imgur.com/lIPWuKn.png)
![](https://i.imgur.com/OZB4HE8.png)
5. Proportional scaling — Shift + white handle
![](https://i.imgur.com/7u096xV.png)

6. Scale from center — Alt + white handle
![](https://i.imgur.com/rGnSnf6.png)
![](https://i.imgur.com/hkXS4ng.png)
![](https://i.imgur.com/1aYIE4L.png)


7. Align
![](https://i.imgur.com/njXtJS6.png)
![](https://i.imgur.com/MFEKgJm.jpg)
![](https://i.imgur.com/3MLlXar.png)
![](https://i.imgur.com/Bes8bca.png)
![](https://i.imgur.com/fQcB6n7.png)
![](https://i.imgur.com/YPagMPO.png)
![](https://i.imgur.com/46jgjKH.png)


8. Group and ungroup
![](https://i.imgur.com/7fqUgFU.png)
![](https://i.imgur.com/QIG6ZSL.png)
![](https://i.imgur.com/7D3GhVJ.png)

9. Hole / cutout / slice

![](https://i.imgur.com/fVYAcsH.png)
![](https://i.imgur.com/F3vwvt5.png)
![](https://i.imgur.com/aV5MJfj.png)
![](https://i.imgur.com/xdyD10g.png)
![](https://i.imgur.com/LW8X8q9.png)



10. QR Code

![](https://i.imgur.com/aou4upG.png)
![](https://i.imgur.com/45CQkPU.png)


Exporting a 3D Model
==


Click **Export** and choose the STL format.
![](https://i.imgur.com/9tm08U7.png)
