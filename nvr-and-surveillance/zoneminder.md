---
parent: NVR
---

## ZoneMinder
Zoneminder is a long runnng reliable project for setting up NVR. 

### Installation
Docker is the easiest way to setup ZoneMinder. 

docker-compose.yaml
```

```

### Home Assistant integration
Home Assistant supports Native camera integration with ZoneMinder cameras. Add this to your `configuration.yaml`

```
zoneminder:
  host: <URL>:<PORT>
  verify_ssl: false
  ssl: true

camera:
  - platform: zoneminder
```

Now you can add all your cameras to your lovelace dashboard. 

### Detecting Camera events on ZoneMinder
The ZoneMinder docker install ships with EventServer notificiation system which can be used to generate events. 

Setup your EventServer by editing the file: TBD
```
TBD
```

#### Getting events on ZMNinja App
TBD

#### Getting events on Home Assistant (MQTT)
TBD
