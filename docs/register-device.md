# Getting Started

## Registering a device

In order for your device to connect to IoT Hub, it must first retreive credentials. This can be done by sending a ```POST``` request to ```/devices/register```. This will register your device with our system and return credentials to allow connection over MQTT.
#### Request Format
###### Example Body
```
{
    "deviceId": "<string>"
}
```

###### Parameters

* **deviceId**: This should be a unique identifier. A MAC adress is recommended, but it can take any form - guid, uuid, etc.

#### Response Format
###### Example Body
```
{
    "deviceId": "<string>"
}
```

###### Parameters

* **host**: This should be a unique identifier. A MAC adress is recommended, but it can take any form - guid, uuid, etc.