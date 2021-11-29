## Building a cheap and reliable PIR system with ESPHome
This guide explains how to build a powered WiFi PIR system in your house. If you are looking to build a battery powered system, then WiFi is probably the wrong choice and you should look elsewhere.

Note: If you are using the slightly expensive PaPIR, you neither need the Power supply mod nor the noise mod.

### Components needed
- Any ESP device
- PSU for powering up ESP
- PIR Sensor: HC SR501
- Ceramic capacitor: 47-220nF

### Steps

#### Power
- Wire your PSU to power the ESP device. If your power system is 5V, then you don't need any additional steps since that's the power expected from HC SR501.
- However, if you are using a 3.3V power supply, you need to bypass the onboard regulator on the sensor to directly take in 3.3V input. 


#### Reducing noise
- HC SR501 is prone to noise and can behave erratically if the issues are not solved. Two major problems usually: ESP brings in WiFi noise and PSU noise. 
- First solve the WiFi noise problem since that's more common. Solder your ceramic capacitor on pins 12-13 of the IC on the PIR sensor. 
- Test your setup after fixing the WiFi noise. If it is still erratic after adjusting sensitivity, then you should look at reducing the power supply noise by soldering an electrolytic capacitor on the PSU input to the sensor. Note: Multiple people have tried and failed using the PSU on Smitch bulbs, consider using an additional supply. 

### Configuration files
ESPHome YAML
```
binary_sensor:
  - platform: gpio
    pin: 
      number: GPIO16
      inverted: false

    name: "PIR Sensor"
    device_class: motion
```

Example HA automation (Generated using Blueprint)
```
alias: Motion-activated Light
description: ''
use_blueprint:
  path: homeassistant/motion_light.yaml
  input:
    motion_entity: binary_sensor.pir_sensor_hall
    light_target:
      device_id: 153528f8b7ba7faa426499554bf2f015
    no_motion_wait: 63
```
