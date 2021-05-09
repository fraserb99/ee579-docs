# EE579 Group 4 Documentation

This site provides documentation to allow integration with our API and MQTT Broker.

Read the [Getting Started](register-device.md) docs if you would like information on how to integrate your IoT device with our system.

## System Overview
### Admin Interface
Our admin interface is available here: [https://www.ee579-group4.net](https://www.ee579-group4.net). This site enables users to login and configure rules, devices, and device groups.

Our system is multi-tenant, with users able to create multiple tenants and invite other users. Rules and devices are then scoped to these tenants, meaning users only have permission to access and edit resources belonging one of their tenants.

### API
Our API is written in C# using ASP.NET Core. Full Swagger OpenAPI documentation is available here: [https://ee579-dev-api.azurewebsites.net](https://ee579-dev-api.azurewebsites.net/swagger)

### MQTT Broker
We are using [Azure IoT Hub](https://docs.microsoft.com/en-us/azure/iot-hub/iot-hub-mqtt-support) as our MQTT Broker. Information on connecting and recieving/publishing messages can be found [here](mqtt.md)
