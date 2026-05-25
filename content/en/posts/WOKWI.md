---
slug: WOKWI
title: WOKWI
date: 2025-10-28 12:29:03
tags:

categories:
  - Note
---
slug: WOKWI

WOKWI Circuit Simulator — Getting Started Guide
==
What makes Wokwi special?
Get started instantly at https://wokwi.com/
* No physical components or large software downloads required. The Wokwi online platform provides everything you need! You can build your next IoT project here in a fraction of the time.


1. No need to worry about making mistakes.
You cannot damage virtual hardware. Trust us — we have tested everything! So do not worry about burning out your precious components. Unlike real hardware, here you can always undo, and you have unlimited chances to start over.


1. Getting help and feedback is easy.
All you need to do is share a link to your Wokwi project and you can get help right away.


1. Build confidence in your code.
Here, hardware and software problems are separated. You do not need to worry about hardware issues — focus entirely on your software.


1. Unconstrained hardware.
No more scavenging components from old projects. Take whatever parts you need freely! You never have to worry about project costs or component inventory.


1. An open maker community.
This is a place to share projects, get help, and find inspiration!

1. Exclusive features!
WiFi simulation — simulated projects can connect to the internet. You can use MQTT, HTTP, NTP, and many other network protocols.
Virtual logic analyzer — capture digital signals (e.g., UART, I2C, SPI) during simulation and analyze them on your computer.
Powerful GDB debugging — a robust Arduino and Raspberry Pi Pico debugger for advanced users.
SD card simulation — use code to store and retrieve files and directories. Club members can also upload binary files (e.g., images).

Changing Wire Colors
==

![](https://i.imgur.com/guffQ2s.png)

**These keyboard shortcuts can also be used while drawing new wires. You can also change wire colors by editing the [diagram.json](https://docs.wokwi.com/zh-CN/diagram-format#connections) file.**

Editor Keyboard Shortcuts
==
![](https://i.imgur.com/YwhlH6v.png)
![](https://i.imgur.com/Otc2P5w.png)
![](https://i.imgur.com/cUPPnjl.png)

Basic Usage
==

1. Adding components to the Wokwi simulator
![](https://i.imgur.com/ujM2lj3.png)

Click the + button to select the component you want to add.

2. Moving components in the Wokwi simulator
![](https://i.imgur.com/P8U2zcO.png)

Click and hold the left mouse button on a component, then drag to move it.

3. Rotating components in the Wokwi simulator
![](https://i.imgur.com/X8OKoun.png)

Click on the component, then press the **R** key on your keyboard.

4. Deleting components in the Wokwi simulator
![](https://i.imgur.com/WuOGdbs.png)

Click on the component to see the selection box around it, then press the **Delete** key.

5. Connecting components in the Wokwi simulator
![](https://i.imgur.com/97hfan3.png)

Move your mouse over a component. If connectable pins are available, a tooltip showing the pin names will appear. Click on a pin to start drawing a wire.

6. Bending wires
![](https://i.imgur.com/7LExz7i.png)

While drawing a wire, click the left mouse button in the direction you want to turn to create a bend.

7. Changing wire color
![](https://i.imgur.com/lHhPsLG.png)

Click on a completed wire; a color selector will appear at the top.

8. Deleting wires
![](https://i.imgur.com/eKBas6d.png)

Click on the wire, then press **Delete**.

9. Common shortcuts
![](https://i.imgur.com/HRPeKxh.png)

The most commonly used shortcuts are shown above.

10. Opening more component details
![](https://i.imgur.com/bQL8OMH.png)

Click on a component, then click the question mark icon that appears.
You can also press the **/** key directly on your keyboard.

11. Changing LED color
![](https://i.imgur.com/FYRn5Gx.png)

Click **diagram.json** in the upper left.
Find the LED entry in the code and modify the color value under **"attrs"**.

12. Hiding wires
![](https://i.imgur.com/QB8eGsO.png)

Click **diagram.json** in the upper left.
Find the **"connections"** section and set the wire color connecting the two component pins to an empty string.

13. Renaming a project
![](https://i.imgur.com/gQRRKVO.png)

Click the arrow to the right of the Library Manager, then click **Rename**.
Remember to save the file after renaming.

14. Mirroring an LED
![](https://i.imgur.com/pfjZKu0.png)

Click **diagram.json** in the upper left.
Inside **"attrs"**, add a **"flip": "1"** property; 1 means horizontal mirror.
Note that the flip property is not supported on every component.

15. Adding labels to LEDs and buttons
![](https://i.imgur.com/eiTldZM.png)

Click **diagram.json** in the upper left.
In the LED's **"attrs"**, add a **"label": "display name"** property.
The same approach works for buttons.
Likewise, the label property is not supported on every component.

16. Saving and sharing a project
![](https://i.imgur.com/2h6GSSw.png)

1. Click the **SAVE** button.
2. Click the share button.
3. Copy the share link.
This feature is very convenient — it lets others see both your wiring and your code.

17. Changing resistor value

Click **diagram.json** in the upper left.
Find the resistor's **"attrs"** and modify the **value** field.
After saving, the color bands on the resistor in the simulator will update automatically — very handy.
![](https://i.imgur.com/UyHdPdb.png)


Supported Boards
==
![](https://i.imgur.com/bLMxtYc.png)

Related Resources
==
Wokwi community
https://discord.com/invite/e5yFaayXkK
https://www.facebook.com/groups/wokwi
Resistor color code calculator
https://www.digikey.tw/zh/resources/conversion-calculators/conversion-calculator-resistor-color-code
