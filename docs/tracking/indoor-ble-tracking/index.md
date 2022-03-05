# Indoor BLE tracking
## Why?
- Track your pets, kids around the house using a cheap BLE tracker(https://robu.in/product/smart-mini-gps-tracker-anti-lost-waterproof-bluetoothtracer-for-pet-kidsgreen) or using Tile(https://www.amazon.in/Tile-Mate-Key-Finder-Phone/dp/B01L3VEC08)
- Find your keys / wallet and which room are they in?
- Automate and take actions using smartwatch / mobile tracking

## How?
There are multiple solutions in the market, use the solution that works best for you. Room assistant has a comprehensive wiki explaining the differences between different solutions(https://www.room-assistant.io/guide/#why-not)

## My setup
- [Room assistant](https://www.room-assistant.io/guide/installation.html#running-with-nodejs) running on Odroid(HA server using addon) and my linux server(NodeJS install). 
- Presence detection running on ESP32 nodes all around the house using [ESPHome](https://esphome.io/components/esp32_ble_tracker.html)
- I use a hybrid mechanism of using states from both ESP32 and RoomAssistant to find the location of the tracker. See section below

## Tracking with ESP32 + RoomAssistant
### Setup
- Running ESPHome on ESP nodes with BLE tracker integration: https://esphome.io/components/esp32_ble_tracker.html
- Running Room assistant with MQTT enabled. https://www.room-assistant.io/integrations/mqtt.html#message-format

### Configuration
- Room assistant: We will create a sensor which listens to the BLE RSSI values reported by Room assistant in HA configuration.yaml.
```
sensor:
  - platform: mqtt
    state_topic: "room-assistant/entity/<roomAssistantNodeId>/bluetooth-low-energy-presence-sensor/<trackerId>"
    name: "Bedroom tracker RSSI"
    value_template: "{{ value_json.entity.measuredValues.<roomAssistantNodeId>.rssi }}"
    unit_of_measurement: dB
```
- ESPHome: We get a sensor by declaring in espHome.yml
```
sensor:
  - platform: ble_rssi
    mac_address: AC:37:43:77:5F:4C
    name: "Hall tracker RSSI"
```
- We will now define a composite sensor which depends on the above sensors in HA configuration.yaml

```
template:
    sensor:
      - name: "Tracker location"
        state: > 
          {% set sensors = ['sensor.bedroom_tracker_rssi',  'sensor.hall_tracker_rssi'] %}
          {% set sensorsNames = ['Bedroom', 'Hall'] %}

          {% set data = namespace(new_list=[]) %}
          {% for sensor in sensors %}
             {% set data.new_list = data.new_list + [states(sensor)] %}
          {% endfor %}
    
          {% set min_rssi = min(data.new_list) %}
          {% set sensor_id = data.new_list.index(min_rssi) %}
          {{ sensorsNames[sensor_id] }}    
```
