# Web Hooks

## What is a Web Hook

Web hooks allow one application to integrate with another over HTTP. This is commonly done by the external application making a post request to an endpoint provided by the application in which the functionality is performed. 

## Using Web Hooks in our System

In the context of our system, web hooks can be used for both inputs to rules, and outputs from rules.

### Inputs

Using a web hook as a rule input allows a 3rd party application to trigger the web hook rule input by making an HTTP request to our API. When a rule is created with a web hook input, a unique URL is generated. In order to trigger the rule, a post request must be made to this URL. Inherently, the logic that determines when the web hook URL should be invoked must be implemented by the 3rd party developer. For example, if a 3rd party wanted to trigger a rule using a moisture sensor, the 3rd party must implement their own low level code to handle the desired analogue thresholds for the sensor and then send the HTTP request to the web hook URL, which will trigger the rule. 

An example URL is shown below:

`http://ee579-dev-api.azurewebsites.net/webhooks/trigger/{unique_code}`

This is a callback URL to our API where `{unique_code}` is the code used to identify the specific rule input. 

### Outputs

Using a web hook as a rule output allows our system to trigger events on a 3rd party application. This works by our API sending an HTTP post request to your specified URL upon the rule's inputs being triggered. The URL must be public facing and have an appropriate CORS policy to allow the receival of our request. That is, POST request should be allowed and the cross origin polciy should allow for requests from our API.

##  Why use Web Hooks?

Our web hook implementation allows our system to be controlled by, or control, a completely different system, assuming that the different system is capable of sending or receiving HTTP post requests. For a web hook as a rule input it means a rule from any connected device on our system, can be triggered by invoking the web hook URL (that we generate for you) by sending a post request to it. This gives almost limitless potential for input interoperability thereby making our system not subject to the hardware or input implementation limitations on certain microncontrollers such as the MSP430. That is, any complex inputs that we do not support can be still be used where their HIGH event on the 3rd party application, can then invoke the web hook URL, thus triggering a rule where our system need not know of the complex input that might have caused it, only that the web hook has been invoked. Likewise, with using a web hook as a rule output, it can trigger functionality on a different system where the triggered functionality is controled by the rule logic in our own system. 

### Examples and Use Cases

#### IFTTT

[IFTTT](https://ifttt.com/home) (If This Then That) is a popular software platform that connects apps, devices and services from different developers in order to trigger one or more automations involving those apps, devices and services. IFTTT offers web hooks as both logic inputs and outputs. On our system, by specifying the web hook output URL as your IFTTT web hook input URL, you have potential to control hundreds of different services and devices all from our own system. An example of this could be using a device on our system with a rule setup with a button pressed input event, then with a web hook output from the rule that points to a web hook input on IFTTT, you could automatically order a Dominoes, send an SMS for you, turn your heating up, post a tweet and hundreds more options. Likewise, this system interaction can work in reverse, with devices on our system being influenced by your logic on IFTTT such as sounding a buzzer on oone of our devices and a specific time of day. The possibilities are endless. 

#### Azure Logic Apps

The corporate equivalent to IFTTT, is [Logic Apps](https://docs.microsoft.com/en-us/azure/logic-apps/logic-apps-overview). A Logic App allows for automation of business workflow tasks and can be controlled with input triggers and produce some output such as sending an email. In a similar fashion to how our system might interact with IFTTT, there is vast potential for controlling your business logic using devices on our system. 



