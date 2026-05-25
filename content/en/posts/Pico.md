---
slug: Pico
title: Pico
date: 2025-10-28 12:25:56
tags:
- Raspberry
categories:
  - Note
---
slug: Pico

Raspberry Pico
==


1. Use Thonny to flash the blink (built-in LED blink) program onto the Pico.
2. Use the Pico + 1602 LCD to display temperature data read from the built-in temperature sensor.
3. Use a Raspberry Pi to flash/debug Pico programs (all steps).
![](https://i.imgur.com/C09WwSI.jpg)
* getTemp.py
* Temperature reading program
```Python=
import utime
from machine import I2C, Pin, ADC
from lcd_api import LcdApi
from pico_i2c_lcd import I2cLcd
I2C_ADDR     = 63
I2C_NUM_ROWS = 2
I2C_NUM_COLS = 16

i2c = I2C(0, sda=Pin(0), scl=Pin(1), freq=400000)
lcd = I2cLcd(i2c, I2C_ADDR, I2C_NUM_ROWS, I2C_NUM_COLS)
def read_temp():
    sensor_temp = ADC(4)
    conversion_factor = 3.3 / (65535)
    reading = sensor_temp.read_u16() * conversion_factor 
    temperature = 27 - (reading - 0.706)/0.001721
    formatted_temperature = "{:.2f}".format(temperature)
    string_temperature = str("Temp:" + formatted_temperature)
    print(string_temperature)
    utime.sleep(2)
    return string_temperature
while True:
    temperature = read_temp()
    lcd.move_to(0,0)
    lcd.putstr(temperature)
```

4. Use VSCode with the Pico to develop MicroPython programs.
![](https://i.imgur.com/8RmvIhI.png)

![](https://i.imgur.com/ez2V7OS.jpg)
