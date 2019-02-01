# jpo-sdw-depositor [![Build Status](https://travis-ci.org/usdot-jpo-ode/jpo-sdw-depositor.svg?branch=dev)](https://travis-ci.org/usdot-jpo-ode/jpo-sdw-depositor) [![Quality Gate Status](https://sonarcloud.io/api/project_badges/measure?project=usdot.jpo.ode%3Ajpo-sdw-depositor%3Adev&metric=alert_status)](https://sonarcloud.io/dashboard?id=usdot.jpo.ode%3Ajpo-sdw-depositor%3Adev)

Subscribes to a Kafka topic and deposits messages to the SDW.

# Overview

This is a submodule of the [jpo-ode](https://github.com/usdot-jpo-ode/jpo-ode) repository. It subscribes to a Kafka topic and listens for incoming messages. Upon message arrival, this application deposits it over REST to the Situation Data Warehouse.

# Installation and Operation

### Requirements

- Docker

### Option 1: Standalone

Use this option when you want to run the depositor by itself. This will listen to any Kafka topic you specify and deposit messages to the Situation Data Warehouse.

1. Configure your desired properties. See **Configuration Reference** at the bottom of this README.
2. Rename your `sample.env` file to `.env` if you haven't already done so
3. Execute the `run.sh` script OR execute these commands:

```
docker build -t jpo-sdw-depositor . 
docker run --rm  --env-file .env jpo-sdw-depositor:latest
```


### Option 2: As ODE submodule

** IN PROGRESS! Further instructions pending ODE compatibility. **

Use this option when you want to run this module in conjuction with the [jpo-ode](https://github.com/usdot-jpo-ode/jpo-ode). The only action you must take here is to set the configuration properties in the env file. See the bottom of this README for a reference.




# Configuration Reference

**SOME OF THESE PROPERTIES ARE SENSITIVE. DO NOT PUBLISH THEM TO VERSION CONTROL**

You may configure these values in `jpo-sdw-depositor/src/main/resources/application.properties` or by editing them in the `sample.env` file.

**IMPORTANT** When using the env file method, you must You must rename or duplicate the `sample.env` file to `.env`


| Value in `application.properties` | Value as env var (in sample.env) | Description                                           | Example Value               |
|-----------------------------------|----------------------------------|-------------------------------------------------------|-----------------------------|
| sdw.kafkaBrokers                | DOCKER_HOST_IP              | Host IP ([instructions](https://github.com/usdot-jpo-ode/jpo-ode/wiki/Docker-management#obtaining-docker_host_ip))                   | 10.1.2.3                   || sdw.groupId                       | SDW_GROUP_ID                     | The Kafka group id to be used for message consumption | usdot.jpo.sdw               |            |
| sdw.kafkaPort                     | SDW_KAFKA_PORT                   | Port of the Kafka instance                            | 9092                        |
| sdw.subscriptionTopic             | SDW_SUBSCRIPTION_TOPIC           | Kafka topic to listen to                              | topic.J2735TimBroadcastJson |
| sdw.destinationUrl                | SDW_DESTINATION_URL              | Full path of the SDW server address                   | 127.0.0.1                   |
| sdw.username                | SDW_USERNAME              | SDW HTTP basic auth username                  | (n/a)  
| sdw.password                | SDW_PASSWORD             | SDW HTTP basic auth password                  | (n/a)  
