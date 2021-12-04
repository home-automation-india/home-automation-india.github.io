---
parent: NVR
---

## ZoneMinder
Zoneminder is a long runnng reliable project for setting up NVR. 

### Installation
Docker is the easiest way to setup ZoneMinder. 

docker-compose.yaml
```
    zoneminder:
          container_name: zoneminder
          image: dlandon/zoneminder:latest
          restart: 'no'
          shm_size: '1gb'
          ports:
            - 8443:443/tcp
            - 9000:9000/tcp
          network_mode: "bridge"
          environment:
            - TZ=Asia/Kolkata
            - SHMEM=50%
            - PUID=99
            - PGID=100
            - INSTALL_HOOK=0
            - INSTALL_FACE=0
            - INSTALL_TINY_YOLOV3=1
            - INSTALL_YOLOV3=1
            - INSTALL_TINY_YOLOV4=1
            - INSTALL_YOLOV4=1
            - MULTI_PORT_START=0
            - MULTI_PORT_END=0
          volumes:
            - ./config:/config:rw
            - ./data:/var/cache/zoneminder:rw
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
