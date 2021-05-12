# EE579 Group 4 Documentation

This site provides documentation to allow integration with our API and MQTT Broker.

If you would like to learn the web interface and functionality provided by the system you can start by [Creating an Account](create-account.md). Then you can get started adding [Devices](devices.md) and [Rules](rules.md)

If you would like information on how to develop your own IoT device and integrate with our system, start by reading the [Register a Device](register-device.md) page.

!!! tip
    **This PDF has been generated from the documentation site here - [docs.ee579-group4.net](https://docs.ee579-group4.net). We would strongly recommend that the documentation is viewed on the interactive site, rather than this PDF, for the best experience.**

## System Overview
### Admin Interface
Our admin interface is available here: [https://www.ee579-group4.net](https://www.ee579-group4.net). This site enables users to login and configure rules, devices, and device groups.

Our system is multi-tenant, with users able to create multiple tenants and invite other users. Rules and devices are then scoped to these tenants, meaning users only have permission to access and edit resources belonging one of their tenants.

### API
Our API is written in C# using ASP.NET Core. Full Swagger OpenAPI documentation is available here: [https://ee579-dev-api.azurewebsites.net](https://ee579-dev-api.azurewebsites.net/swagger)

### MQTT Broker
We are using [Azure IoT Hub](https://docs.microsoft.com/en-us/azure/iot-hub/iot-hub-mqtt-support) as our MQTT Broker. Information on connecting and recieving/publishing messages can be found [here](mqtt.md)

## GitHub Repos

* [ee579-api](https://github.com/fraserb99/ee579-api) - C# API repository
* [ee579-web](https://github.com/fraserb99/ee579-web) - React web interface repository
* [ee579-msp430](https://github.com/fraserb99/ee579-msp430) - Repository containing msp430 and ESP8266 code
* [ee579-docs](https://github.com/fraserb99/ee579-docs) - Repository containing the markdown files used to create these docs