# IoT Agents

**Note:** Before setting up IoT Agents make sure that orion and the mongoDB is
**up and running!

## Introduction and general information

For connecting IoT-devices, send their data and be managed from a FIWARE based
platform using thier native protocol FIWARE offers a selection of IoT Agents
based on a node.js library that you can find here
([Link](https://github.com/telefonicaid/iotagent-node-lib)). The corresponding
manual is available under
https://github.com/telefonicaid/iotagent-node-lib/blob/master/doc/usermanual.md

An overview of the concept is given in the figure below:

![FIWARE IoT Device Management GE architecture (_source_: https://fiwaretourguide.readthedocs.io/en/latest/iot-agents/introduction/)](../docs/figures/iot-agents_zoom.png)

***Figure 1:*** *FIWARE IoT Device Management GE architecture (_source_: https://fiwaretourguide.readthedocs.io/en/latest/iot-agents/introduction/)*

Generally, the library offers developers the opportunity to build custom agents
for their devices and specific protocols that then can easily connect to NGSI
Context Brokers (such as Orion).

However, before starting implementing your own agents you should first check if
the already exiting agents may fit your needs. Here
([Link](https://www.fiware.org/developers/catalogue/)) you find a list of
exiting agents and their documentation.

On low level the agents can be configured via a config.js file. However, in this
tutorial we use docker as framework for our platform. Therefore, it is important
how the configuration via docker-compose and environment variables. An overview
of the commonly allowed variables is given here
([Link](https://iotagent-node-lib.readthedocs.io/en/latest/installationguide/index.htmlµ)).
If needed this list is extended by the individual agents because not all of them
need e.g. a configuration for MQTT.

## How to start

Before you start you should think about some general questiions about the
configuration and services you need for your specific purposes.
1. What type of device do I want to connect to the platform?
2. What type of transportation protocol do I want to use? - e.g. HTTP, MQTT, AMQP etc.
3. How is the sent data formated? - e.g. JSON, Ultralight etc.

Depending on your needs you have to choose the right agent. In this repository
you will find a configuration for an IoT Agent for JSON and LWM2M, which should
be suffcient for most needs. Additionally, you will find quick start files for
an MQTT-Broker named Mosquitto. The choice of MQTT-Broker depends also on your
needs. However, Mosquitto is an realtively simple open-source implementation and
free to use. If you need something real fast with of sampling rates down to
milliseconds and high scalability you should think about using RabbitMQ and its
MQTT extension ([Link](https://www.rabbitmq.com/mqtt.html))

**WARNING:** Please be aware of the fact that we do not cover security aspects
here.

## Troubleshooting

For troubleshooting the FIWARE community offers a quite good webinar on youtube
where they explain how to solve common mistakes and problems with iot agents.
https://www.youtube.com/watch?v=FRqJsywi9e8&feature=youtu.be

However, if you simply want to check for traffic you can use the integrated pm2 tool. Execute in the chosen iot-agent folder:

      make exec
      
      pm2 monit