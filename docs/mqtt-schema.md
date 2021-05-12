# MQTT Messaging Schema

This page shows schema for messages between device and cloud. All message parameters should be sent in the message body, in JSON format as detailed below. It should be noted that the JSON is case-sensitive so all JSON key and values must be formatted as shown in the 'Message Body' schema.

## Device to Cloud Messages

Device-to-cloud messages should be sent when an input has been triggered. These messages will be used to trigger rules if the conditions are met.

### Button Pushed

This message is sent to the broker whenever a button is pushed on the microcontroller.

**Message Body**
``` json
{
    "InputType": enum, // [Button1, Button2]
    "Value": int // The length the button is held in ms
}
``` 

### Potentiometer Input

This message is sent every time the analogue value from the potentiometer is read. The value is sent with this message.

**Message Body**:
```
{
    "InputType": "Potentiometer",
    "Value": int // (0 - 1023) - the analogue value of the potentiometer  
}
``` 

### Temperature Input

This message is sent every time the analogue value from the temperature sensor is read. The value is sent with this message.

**Message Body**:
```
{
    "InputType": "Temperature",
    "Value": int // (-50 to 100) - the temperature in degrees celsius
}
```

## Cloud to Device Messages

Cloud-to-device messages are used to perform outputs on the device as a result of a rule being triggered. There is also a message used to configure the device's inputs to reduce the number of messages sent.

### LED Output

This message is sent to notify the microcontroller to turn an LED on/off and with the specified colour. 

**Message Body**:
```
{
    "OutputType": "LedOutput",
    "Peripheral": enum, // [Led1, Led2, Led3]
    "Value": bool, // the desired state of the LED.
    "Colour" enum // (Led3 only) [Red/Green/Blue/Purple/Yellow/White]
}
``` 

### Breath LED

This message is sent to notify the microcontroller to breathe an LED at a specified speed and colour.

**Message Body**:
```
{
    "OutputType": "LedBreathe",
    "Peripheral": enum, // [Led1, Led2, Led3]
    "Period": int, // how long the period of the breathing should be in ms.
    "Colour": enum // (Led3 only) [Red/Green/Blue/Purple/Yellow/White]
}
``` 

### Blink LED

This message is sent to notify the microcontroller to blink an LED at a specified speed and colour.

**Message Body**:
``` 
{
    "OutputType": "LedBlink",
    "Peripheral": enum, // [Led1, Led2, Led3]
    "Period": int, // how long the period of the blinking should be in ms.
    "Colour": enum // (Led3 only) [Red/Green/Blue/Purple/Yellow/White]
}
``` 

### Fade LED

This message is sent to notify the microcontroller to fade an LED to a desired state at a specified speed and colour.

**Message Body**:
``` 
{
    "OutputType": "LedFade",
    "Peripheral": enum, // [Led1, Led2, Led3]
    "Value": bool, // the desired state of the LED.
    "Duration": int, // the duration the fade should take in ms.
    "Colour": enum // (Led3 only): [Red/Green/Blue/Purple/Yellow/White]
}
``` 

### Cycle LED 3

This message is sent to notify the microcontroller to cycle the LED colour in the specified direction. 

**Message Body**:
```
{
    "OutputType": "LedCycle",
    "Direction": bool, // cycle forwards or backwards - [true/false] respectively
    "Period": int // how long the period of the cycle should be in ms 
}
``` 

### Buzzer On

This message is sent to notify the microcontroller to turn the piezo buzzer on for the specified length of time. 

**Message Body**:
```
{
    "OutputType": "BuzzerOn",
    "Duration": int, // the duration the buzzer should be on in ms 
}
``` 

### Beep Buzzer

This message is sent to make the microcontroller toggle a buzzer at the desired rate. 

**Message Body**:
``` 
{
    "OutputType": "BuzzerBeep",
    "OnDuration": int, // the duration the buzzer should be on in ms 
    "OffDuration": int // the duration the buzzer should be off in ms 
}
``` 

### Configure Device

This message is sent to notify the microcontroller which input devices are involved in rules. This is used to limit the number of messages sent by devices - if an input device is not involved in any rules, messages should not be sent to the broker when its value changes. 

This message is sent whenever a device connects to the broker, or if a rule is created, updated, or deleted involving the device.

**Message Body**:
```
{
    "MessageType": "DeviceConfig",
    "Button1": bool,
    "Button2": bool,
    "Potentiometer": bool,
    "Temperature": bool
}
```