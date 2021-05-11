# Getting Started

## Registering a device

In order for your device to connect to IoT Hub, it must first retreive credentials. This can be done by sending a ```POST``` request to ```https://ee579-dev-api.azurewebsites.net/devices/register```. This will register your device with our system and return credentials to allow connection over MQTT. The device should make this request when first powered on, but the same endpoint can be used even if a device is already registered in the system. This accounts for situations where the device may have lost it's credentials, and allows the device to make the request every time it powers on, if desired.
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
    "connectionString": "HostName=IFTTT-Iot-Hub.azure-devices.net;DeviceId={deviceId};SharedAccessKey=El50EkQ/S/9qp5dd/V3VpsizIvSv+SA8TVF3QiGc93A=",
    "host": "IFTTT-Iot-Hub.azure-devices.net",
    "port": 8883,
    "topic": "devices/{deviceId}/messages/devicebound/#",
    "password": "SharedAccessSignature sr=IFTTT-Iot-Hub.azure-devices.net%2Fdevices%2F{deviceId}&sig=KOYS9LgCJ9eH7TTlMIGvedxIVI3cXmha7uU6yB4Bs6M%3D&se=88018657115"
}
```

###### Parameters

* **connectionString**: The connection string the broker. {deviceId} should be replace with a unique identifier.  A MAC adress is recommended, but it can take any form - guid, uuid, etc.
* **host**: The MQTT broker url.
* **topic**: The topic that the device should subscribe to, to receive cloud-to-device messages.
* **password**: The password that should be used when connecting to the broker, in the form of a [SAS token](https://docs.microsoft.com/en-us/azure/iot-hub/iot-hub-devguide-security#use-a-shared-access-policy).


## Debugging

It may be neccessary to make this request on a computer, rather than IoT device when debugging. The [API Swagger Docs](https://ee579-dev-api.azurewebsites.net) can be used to make this request and provides a prefilled request body. Any other method of making HTTP requests can also be used - cURL, [Postman](https://postman.com), etc.

## Next Steps

* [Connecting to the broker](mqtt.md)