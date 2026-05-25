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

Introduction to Arduino Relay
==

![](https://hackmd.io/_uploads/SyiMqqeB2.png)

The Arduino Uno can only supply 5V or 3.3V DC to external devices. When you need higher voltages or AC power — for example, to control an electric fan or a desk lamp — you need a relay. Just like a switch, a relay lets you turn a circuit on or off from your program. If you want to build smart home appliances, a relay is absolutely essential!

![](https://hackmd.io/_uploads/ryqr9qlSh.png)

The most common type is a single-channel (1-relay) module.
There are also 2-channel, 4-channel, and 8-channel relay modules.

### 4-Channel Relay

![](https://cdn.discordapp.com/attachments/625953483576705024/763276251917582366/DSC_0256.JPG)



### Usage Guide
The relay has its rated voltage and current printed on it — for example, 10A 125V AC. Many modules do not print DC ratings, but as a general rule, DC up to 12V and 2A should be fine even if it is not stated. For long-term use, however, it is recommended to purchase a module that clearly specifies its DC ratings.

A relay module is typically divided into two sides, each with 3 pins. The pin-header side communicates with the Arduino: **+** is VCC, **-** is GND, and **IN** is the signal line you use to turn the relay on or off.

The other side carries the power-circuit terminals:

**NO** (Normally Open): The circuit is open (no current) under normal conditions.
**COM** (Common): The shared terminal. Most people connect the external power supply here and then run a wire from NO or NC to the external device.
**NC** (Normally Closed): The circuit is closed (current flowing) under normal conditions.

You connect to either NO or NC — never both at the same time. Which one you choose depends on your specific application.
