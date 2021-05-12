# MQTT Broker

## Connecting

To connect to IoTHub there are multiple different protocols that can be used, you can either directly connect to these protocols or prefferably use one of the IoTHub device SDKs.

### Connecting using the IotHub SDKs

Connecting to IoTHub using one of Microsoft's SDKs use a connection string to connect. The connection string can be garnered from the response from our API's register request. Using the SDKs is the recommended way of connecting for its ease of use, especially regarding certificate handling as IoTHub forces TLS/SSL.

Some of the available SDKs include:

* [C SDK](https://github.com/Azure/azure-iot-sdk-c)

* [Python SDK](https://github.com/Azure/azure-iot-sdk-python)

* [Node.js SDK](https://github.com/Azure/azure-iot-sdk-node)

* [Java SDK](https://github.com/Azure/azure-iot-sdk-java)

* [.NET SDK](https://github.com/Azure/azure-iot-sdk-csharp)


#### Using our Example Code for an ESP8266

We have provided some example code for registering a device with the API and sending/receiving messages from IoTHub. This example code is for the ESP8266 Wifi Module, but the methods will be similar on alternative devices. The code can be pulled from this [repository](https://github.com/fraserb99/ee579-msp430.git). Cd into the esp_iothub_client directory for the example code. By following the instructions [here](https://github.com/Azure/azure-iot-arduino), you can setup the Arduino IDE with functionality for flashing our example code to the ESP8266.

### Connecting directly to the protocols

As MQTT is usually implemented on memory restricted devices, it is possible that the memory required to implement broker connection/interaction using an SDK is unavailable. For this reason, directly connecting to the protocol might be required. Below is a mosquitto subscribe command showing the parameters required to manually connect to the cloud device topic.

```
mosquitto_sub \
    -h IFTTT-Iot-Hub.azure-devices.net \
    -p 8883 \
    -t "devices/00:0a:95:9d:68:16/messages/devicebound/#" \
    -i 00:0a:95:9d:68:16 \
    -u "IFTTT-Iot-Hub.azure-devices.net/00:0a:95:9d:68:16" \
    -P "SharedAccessSignature sr=IFTTT-Iot-Hub.azure-devices.net%2Fdevices%2F00%3A0a%3A95%3A9d%3A68%3A16&sig=ulc08e%2FYp%2FMLJdyMLxsV7pqTQ12XamytzQjxFFithNg%3D&se=1618623078" \
    --cafile C:\Users\Fraser\GitHub\ee579-api\EE579\EE579.Core\Slices\Devices\Simulate\iotHubCert.pem 
    -V mqttv311 \
    -q 1
```

* **-h**: The host name for the broker. 

* **-p**: The port number of the broker.

* **-t**: The topic the cloud to device messages will be received on.

* **-i**: The unique identifier for the device. Recommended as the device MAC address.

* **-u**: The MQTT username which here is just set to the hostname/deviceId.

* **-P**: The password for the broker. Can be retrieved from the register API response.

* **--cafile**: Path to the IotHub Certificate.

* **-V**: The MQTT version. IotHub only supports MQTT version 3.1.1.

* **-q**: This is for the quality of service. IoTHub only supports a quality service of 1.