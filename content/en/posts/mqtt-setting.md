---
slug: mqtt-setting
title: mqtt_setting
date: 2025-10-28 12:05:43
tags:
- MQTT  
---
slug: mqtt-setting

# MQTT Basic Configuration

## 1. MQTT Broker Setup (Using Mosquitto)

```ini
# mosquitto.conf
listener 1883
allow_anonymous true
```

The hand-raise and head-turn counts will be stored directly into the database by the Python side.

This should be what I referred to as the start of training. In addition to this, we also need to send a message when it ends — I have that written below.

4. **Collision Event**
   - Topic: `collision_topic`
   ```json
   {
     "hit_light": true|false
   }
   ```



## 3. IoT to Python
1. **A new student begins**
   - Topic: `game_start_topic`
   ```json
   {
     "game_start": true|false
   }
   ```
2. **This student finishes**
   - Topic: `game_over_topic`
   ```json
   {
     "game_over": true|false
   }
   ```


## 4. Python to IoT
1. **Pedestrian position per frame**
   - Topic: `student_walk_distence_topic`
   ```json
   {
     "on_the_near_lane": true|false
     "on_the_far_lane": true|false
   }
   ```
