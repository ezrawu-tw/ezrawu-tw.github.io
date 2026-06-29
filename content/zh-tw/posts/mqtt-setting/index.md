---
slug: mqtt-setting
title: mqtt_setting
date: 2025-10-28 12:05:43
tags:
- MQTT  
---


# MQTT 基本設定

## 1. MQTT Broker 設定 (使用 Mosquitto)

```ini
# mosquitto.conf
listener 1883
allow_anonymous true
```

舉手轉頭次數會由pytnon這邊直接存進資料庫

這應該就是我說的訓練開始對吧，那除了這個以外，結束也需傳一個，我有寫在下面

4. **碰撞事件**
   - Topic: `collision_topic`
   ```json
   {
     "hit_light": true|false
   }
   ```



## 3. IoT to Python
1. **開始一位新的學生**
   - Topic: `game_start_topic`
   ```json
   {
     "game_start": true|false
   }
   ```
2. **這位學生結束**
   - Topic: `game_over_topic`
   ```json
   {
     "game_over": true|false
   }
   ```


## 4. Python to IoT
1. **每幀行人走到哪了**
   - Topic: `student_walk_distence_topic`
   ```json
   {
     "on_the_near_lane": true|false
     "on_the_far_lane": true|false
   }
   ```

