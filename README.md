# MQTT Dasher
_This project was forked from:_
https://github.com/stjohnjohnson/mqtt-dasher

_I am adapting it for my own user with docker and ansible._

# Description 
***Emits events to MQTT when an Amazon Dash button is pressed.***

[![GitHub tag](https://img.shields.io/github/tag/m3ki/mqtt-dasher.svg)](https://github.com/stjohnjohnson/mqtt-dasher/releases)
[![Build Status](https://travis-ci.org/m3ki/mqtt-dasher.svg?branch=master)](https://travis-ci.org/m3ki/mqtt-dasher)

#Docker Configuration
TODO

#Ansible
```
- name: Install Mqtt Dasher
  docker_container:
    name: mqttd
    image: m3ki/mqtt-dasher:latest
    state: started
    restart_policy: always
    recreate: yes
    network_mode: host
    privileged: yes
    volumes:
      - "{{data_directory}}/mqttd/config/config.yml:/config/config.yml:rw"
```

# Configuration

The dash bridge has one yaml file for configuration:

```

---
mqtt:
    # Specify your MQTT Broker's hostname or IP address here
    host: mqtt
    port: 1883
    #leave empty if none
    username:
    password:
    # Preface for the topics $PREFACE/$TOPIC
    preface: dash

buttons:
    44:65:0d:dc:51:50:
        name: nerf_supplies
        interface: eth0     # optional
        timeout: 5000   # optional (time in ms)
        protocol: arp   # optional (one of {udp, arp, all})


```

# The underlying code makes use of this [this library](https://github.com/hortinstein/node-dash-button#installation-instructions).
