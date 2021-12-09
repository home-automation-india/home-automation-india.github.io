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

Setup your EventServer by editing the file in the `/config` folder: [Documentation Reference](https://zmeventnotification.readthedocs.io/en/latest/guides/install.html#update-the-configuration-files)

#### Getting events on ZMNinja App
The above config is sufficient to receive notifications on ZMNinja. Notifications still work when you are not in the same network but you will need to use ZeroTier / Tailscale / Publicly accessible ZoneMinder instance when you open the app. 

#### Getting events on Home Assistant (MQTT)
- Getting MQTT to work requires additional installation of MQTT Perl libraries. Log into the docker instance using `docker exec --it <container_name> /bin/bash`
- Install the library `perl -MCPAN -e "install Net::MQTT::Simple"`. You might see an error saying `make not found`, you might need to install it first using `apt install make`
- Enable MQTT in the configuration file: [Reference documentation](https://zmeventnotification.readthedocs.io/en/latest/guides/es_faq.html#how-can-i-use-this-with-node-red-or-home-assistant)
- Now you can create sensors using the MQTT information publised by ZoneMinder. For instance, create a Motion detection sensor using 
```
binary_sensor:
  - platform: mqtt
    state_topic: "zoneminder/1"
    name: ZM camera
    value_template: '{% if value_json.state == "alarm" and value_json.eventtype == "event_start" %} ON {% else %} OFF {% endif %}'
    device_class: motion
```
