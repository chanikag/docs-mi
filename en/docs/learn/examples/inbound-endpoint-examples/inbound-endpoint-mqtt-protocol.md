# How to Use an MQTT Inbound Endpoint

This sample demonstrates how the MQTT connector publishes a message on a
particular topic and how a MQTT client that is subscribed to that topic
receives the message. 
Following sections demonstrate how you can try this sample using the
Mosquitto server as the Message Broker.

## Synapse configuration

Following are the integration artifacts that we can used to implement this scenario. See the instructions on how to [build and run](#build-and-run) this example.

=== "Inbound Endpoint"
    ```xml
    <?xml version="1.0" encoding="UTF-8"?>
    <inboundEndpoint name="SampleInbound" onError="fault" protocol="mqtt" sequence="TestIn" statistics="enable" suspend="false" trace="enable" xmlns="http://ws.apache.org/ns/synapse">
        <parameters>
            <parameter name="sequential">true</parameter>
            <parameter name="mqtt.connection.factory">mqttConFactory</parameter>
            <parameter name="mqtt.server.host.name">localhost</parameter>
            <parameter name="mqtt.server.port">1883</parameter>
            <parameter name="mqtt.topic.name">esb.test</parameter>
            <parameter name="content.type">application/xml</parameter>
            <parameter name="mqtt.subscription.qos">0</parameter>
            <parameter name="mqtt.session.clean">false</parameter>
            <parameter name="mqtt.ssl.enable">false</parameter>
            <parameter name="mqtt.reconnection.interval">1000</parameter>
        </parameters>
    </inboundEndpoint>
    ```
=== "Sequence"    
    ```xml
    <?xml version="1.0" encoding="UTF-8"?>
    <sequence name="TestIn" trace="disable" xmlns="http://ws.apache.org/ns/synapse">
       <log level="full"/>
       <drop/>
    </sequence>
    ```

## Build and run

Create the artifacts:

{!includes/build-and-run.md!}
3. Create a [mediation sequence]({{base_path}}/develop/creating-artifacts/creating-reusable-sequences) and [inbound endpoint]({{base_path}}/develop/creating-artifacts/creating-an-inbound-endpoint) with configurations given in the above example.

Set up the MQTT server:

1. Install Mosquitto. (This sample is tested for [Mosquitto1.6.7 version](https://mosquitto.org/download/)). The Mosquitto server will run automatically in the background.
2. Add [MQTT client library](https://mvnrepository.com/artifact/org.eclipse.paho/mqtt-client/0.4.0) to pom.xml file in the integration project.
    ```xml
    <dependency>
        <groupId>org.eclipse.paho</groupId>
        <artifactId>mqtt-client</artifactId>
        <version>0.4.0</version>
    </dependency>
    ```

3. [Deploy the artifacts]({{base_path}}/develop/deploy-artifacts) in your Micro Integrator.

Open a new terminal and enter the below command to send an MQTT message using mosquitto-pub. Be sure to enter the MQTT Topic Name you entered when creating the inbound endpoint as shown below.

```bash
mosquitto_pub -t <MQTT Topic Name>  -m "<msg><a>Testing123</a></msg>"
```

You will see that the Micro Integrator receives a message when the Micro Integrator Inbound is set as the ultimate receiver.
