# MQTT Messaging Schema

## Device to Cloud Messages

### Button Pushed

This message is sent to the broker whenever a button is pushed on the microcontroller.

* **Property Bag** - `/InputType=ButtonPushed`  
* **Message Body** - ```Duration: int - length the button is held in ms``` 

### Switch Flipped

This message is sent to the broker whenever the state of a switch changes. 

* **Property Bag** - `/InputType=SwitchFlipped&Peripheral={[Switch1, Switch2]}`  
* **Message Body** - ```Value: bool – whether the switch is on or off ``` 

### Potentiometer Input

This message is sent every time the analogue value from the potentiometer is read. The value is sent with this message.

* **Property Bag** - `/InputType=PotentiometerValue `  
* **Message Body** - ```Value: int (0 - 1023) - the analogue value of the potentiometer  ``` 

### Temperature Input

This message is sent every time the analogue value from the temperature sensor is read. The value is sent with this message.

* **Property Bag** - `/InputType=PotentiometerValue `  
* **Message Body** - ```Value: int (-50 to 100) - the degrees celcius read from the temperature sensor ``` 



## Cloud to Device Messages

### Turn LED On

This message is sent to notify the microcontroller to turn an LED on/off and with the specified colour. 

* **Property Bag** - `/OutputType=LedOutput&Peripheral={[Led1, Led2, Led3]}  `  
* **Message Body** - 
```
{
    Value: bool – the desired state of the LED.
    Colour (Led3 only): enum - [Red/green/blue/purple/yellow/white]
}
``` 

### Breath LED

This message is sent to notify the microcontroller to breathe an LED at a specified speed and colour.

* **Property Bag** - `/OutputType=LedBreathe&Peripheral={[Led1, Led2, Led3]}  `  
* **Message Body** - 
```
{
    Period: int – how long the period of the cycle should be in ms.
    Colour (Led3 only): enum - [Red/green/blue/purple/yellow/white]
}
``` 

### Blink LED

This message is sent to notify the microcontroller to blink an LED at a specified speed and colour.

* **Property Bag** - `/OutputType=LedBlink&Peripheral={[Led1, Led2, Led3]} `  
* **Message Body** - 
``` 
{
    Period: int – how long the period of the cycle should be in ms.
    Colour (Led3 only): enum - [Red/green/blue/purple/yellow/white]
}
``` 

### Fade LED

This message is sent to notify the microcontroller to fade an LED to a desired state at a specified speed and colour.

* **Property Bag** - `/OutputType=LedFade&Peripheral={[Led1, Led2, Led3]} `  
* **Message Body** - 
``` 
{
    Value: bool – the desired state of the LED. Duration: int – the duration the fade should take in ms.
    Colour (Led3 only): enum - [Red/green/blue/purple/yellow/white]
}
``` 

### Cycle LED

This message is sent to notify the microcontroller to cycle the LED colour in the specified direction. 

* **Property Bag** - `/OutputType=LedCycle  `  
* **Message Body** - 
```
{
    Direction: bool – cycle forwards or backwards.
    Period: int – how long the period of the cycle should be in ms 
} 
``` 

### Sound Buzzer

This message is sent to notify the microcontroller to turn the piezo buzzer on for the specified length of time. 

* **Property Bag** - `/OutputType=BuzzerOn   `  
* **Message Body** - ``` Duration: int - the duration the buzzer should be on in ms ``` 

### Beep Buzzer

This message is sent to make the microcontroller toggle a buzzer at the desired rate. 

* **Property Bag** - `/OutputType=BuzzerBeep    `  
* **Message Body** - 
``` 
{
    OnDuration: int - the duration the buzzer should be on in ms 
    OffDuration: int - the duration the buzzer should be off in ms 
}
``` 

### Configure Device

This message is sent to notify the microcontroller which input devices to configure for sending input messages.  

* **Property Bag** - `/MessageType=DeviceConfig    `  
* **Message Body** - 
```
{
    Button1: bool 
    Button2: bool 
    Potentiometer: bool 
    Temperature: bool 
}
```