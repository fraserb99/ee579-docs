# Web Hooks

## What is a Web Hook

Web hooks allow one application to integrate with another over HTTP. This is commonly done by the external application making a post request to an endpoint provided by the application in which the functionality is performed. Following the definition, our web hook implementation allows our system to be controlled by a completely different system, assuming that the different system is capable of sending HTTP post requests. This means, a rule from any connected device on our system, can be triggered by invoking the web hook URL (that we generate for you) by sending a post request to it. This gives almost limitless potential for input interoperability thereby making our system not subject to the hardware or input implementation limitations on certain microncontrollers such as the MSP430. That is, any complex inputs that we do not support can be still be used where their HIGH event on the 3rd party application, can then invoke the web hook URL, thus triggering a rule where our system need not know of the complex input that might have caused it, only that the web hook has been invoked.

## Using Web Hooks in our System

### Inputs

In the context of our system, web hooks can be used for inputs to rules. This allows a 3rd party application to trigger a rule by making an HTTP request to our API. When a rule is created with a web hook input, a unique url is generated. In order to trigger the rule a post request must be made to this url. Inherently however, the thresholds of these additional analogue inputs and trigger logic for digital inputs must be implemented by the 3rd party developer.
 An example URL is shown below:

`http://ee579-dev-api.azurewebsites.net/webhooks/trigger/{unique_code}`

This is a callback URL to our API where `{unique_code}` is the code used to identify the specific rule input. 

### Outputs

##  Use Cases

For example, to implement a moisture sensor input, the 3rd party must write the logic for determing the analogue trigger threshold for what moisture level should trigger the rule, once within this threshold, the system should send the HTTP POST request to the web hook for the respective rule. 



