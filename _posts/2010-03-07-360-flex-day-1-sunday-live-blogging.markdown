---
layout: post
title: "360 Flex - Day 1 (Sunday) - Live Blogging"
date: 2010-03-07 23:17
comments: true
categories: flex
---
We just had a great breakfast at Peggy Sue's Dinner...and moved over to the Ebay Headquarters where the conferences is about to start. 

I'll be taking notes during the day and updating this page as we go one.

UPDATE: Now that I typed all that I realized that Justin put up the slides and code on his blog: <a href="http://blog.classsoftware.com/">http://blog.classsoftware.com/</a>. 
 
<!--more-->

<h1>Connecting Arduino Hardware to Flex: Justin Mclean</h1>

twitter: justinmclean
Justin is from Sydney, Australia.

Content:
* Arduino platform, how to program and how to connect to Flex
* 2/3 Arduino 1/3 Flex
* Hands on 

<h3>So we'll go through the followings:</h3>

* Digital Inputs
* Digital Outputs
* Analogue Inputs
* Pulse Width Modulation
* Serial Communication
* Connecting to Flex
* Review and wrap up

So Justin gave each attendee one board and a set of components. The board is open source hardware. I think that's pretty cool. Feels like the hardware kit I bought for my 6 years son. The board is $25 and with all the components it's about $40.

<div style="text-align:center;"><img src="http://onrails.org/files/arduino.png" alt="arduino.png" border="0" width="400" height="300" /></div>

The hardware is provided to all participants by <a href="http://sparkfun.com"><strong>sparkfun.com</strong></a>

<h3>Software</h3>

http://arduino.cc/en/Main/Software

<div style="text-align:center;"><img src="http://onrails.org/files/arduino_software.png" alt="arduino_software.png" border="0" width="350" height="247" /></div>

Also install the serial driver: FTDIUSBSerialDriver_10_4_10_5_10_6

<h3>Other Hardwares</h3>

* ATmega micro-controller from Atmel. It mostly runs in cars.
* Arduino Duemilanove
* Arduino Pro and Pro mini
* Lyllypad (warable)
* Funnell IO
* Mega
* Many others

<h3>ATMega328</h3>

* Hight performance low power RISC
* 16 Mzh up to 16 mips (faster as your first pc you owned - if you are a bit older)
* 32K of Memory
* SPI and 2 wire serial interfaces
* External interrupts, timers, pulse width modulation

<h3>IDE</h3>

* IDE open sourcee and cross platform. 
* Based on the Processing language
* Many open source sketches (projects) and libraries availables. Ethernet library, servers, ...

<h3>First Program</h3>

``` javascript
int ledPin =  13;    // LED connected to digital pin 13

// The setup() method runs once, when the sketch starts
void setup()   {                
  // initialize the digital pin as an output:
  pinMode(ledPin, OUTPUT);     
}

// the loop() method runs over and over again,
// as long as the Arduino has power

void loop()                     
{
  digitalWrite(ledPin, HIGH);   // set the LED on
  delay(1000);                  // wait for a second
  digitalWrite(ledPin, LOW);    // set the LED off
  delay(1000);                  // wait for a second
}
```

Now this will make the led blink:

<object width="480" height="385"><param name="movie" value="http://www.youtube.com/v/PS5UcEYQdBA&hl=en_US&fs=1&"></param><param name="allowFullScreen" value="true"></param><param name="allowscriptaccess" value="always"></param><embed src="http://www.youtube.com/v/PS5UcEYQdBA&hl=en_US&fs=1&" type="application/x-shockwave-flash" allowscriptaccess="always" allowfullscreen="true" width="480" height="385"></embed></object>

<h3>Programming</h3>

* C like language based o wiring
* Write code and compile in IDE
* Upload compiled code using USB
* Hard to debug

<h3>Circuit Basics</h3>

* Ground and power
* Potential difference required for current ot flow
* Conductors and resistors

<h3>Digital Inputs/Outputs</h3>

* Digital pins on Arduino are dual purpose
* Digital logic and voltage on = 5V off = 0V
* Can be set to be input or output via pinMode

<h3>Variables</h3>

* boolean, char, byte, int, long, float, double, string and array
* int 16 bits, long 32 bits, float 32 bits
* Strings are nul terminated '\0'
* Declare by <datatype> <variable name>; eg int i;

It's actually C++...What?! At a Flex conferences :-)

<h3>Setup Function</h3> 

* Used for initialization
* Run when program loaded or board reset
* Best place to place calls to pinMode

<h3>LEDs</h3>

* Current will only flow in one direction
* Longest pin connect to positive side, shortest to ground
* Dont' connect directly to power source use in series with resistors

<div style="text-align:center;"><img src="http://onrails.org/files/leds.png" alt="leds.png" border="0" width="300" height="225" /></div>

<h3>Resistors</h3>

* Resistors limit current flowing through them
* Value and tolerance indicated by cooler bands
* Resistor values for LEDs
* For RGB or LEG digits you need multiple resitors
* REG/GREEN/BLUE 180 oms, WHITE/ULTRAVIOLET 100 oms

<div style="text-align:center;"><img src="http://onrails.org/files/resistors.png" alt="resistors.png" border="0" width="300" height="225" /></div>

<h3>Debugging ia Serial Port</h3>

* Use Serial.begin to set speed
* Serial.print, Serial.println to output
* Use serial monitor in IDE to view

<h3>Blinking LED</h3>

Same program that the first program but this time we just set the led to the pin 3 which is connected to the board.

<object width="480" height="385"><param name="movie" value="http://www.youtube.com/v/H_nD-bWSNuI&hl=en_US&fs=1&"></param><param name="allowFullScreen" value="true"></param><param name="allowscriptaccess" value="always"></param><embed src="http://www.youtube.com/v/H_nD-bWSNuI&hl=en_US&fs=1&" type="application/x-shockwave-flash" allowscriptaccess="always" allowfullscreen="true" width="480" height="385"></embed></object>

<h3>Digital Inputs</h3>

* Some logic as inputs; hight 95V0 or low (0V)
* Simplest digital input switch
* Call pinMode to set as digital input as input

<h3>Connect Switch</h3>

* Wire up push button on breadboard
* Change code to turn light on/off

Now switches have three states (on, off, and in between) to the board needs to be wired to take that into account so you can program it accordingly. We added a very high resistence (10k) next to switch to ensure that the switch reports 0V when not clicked.

``` javascript
int led = 3;
int button = 4;

void setup() {
  Serial.begin(9600);
  pinMode(led, OUTPUT);
  pinMode(button, INPUT);
}

void loop() {
  if (digitalRead(button) == HIGH)  {  
    Serial.println("on"); 
    digitalWrite(led, HIGH);    
  } else {
    Serial.println("off"); 
    digitalWrite(led, LOW);  
  }
}  
```

So let's look at the wiring and how the switch operates:

<object width="480" height="385"><param name="movie" value="http://www.youtube.com/v/45Haml5UCIc&hl=en_US&fs=1&"></param><param name="allowFullScreen" value="true"></param><param name="allowscriptaccess" value="always"></param><embed src="http://www.youtube.com/v/45Haml5UCIc&hl=en_US&fs=1&" type="application/x-shockwave-flash" allowscriptaccess="always" allowfullscreen="true" width="480" height="385"></embed></object>


<h3>Internal Pullup Resistors</h3>

* Set mode to input
* digitalWrite to HIGHT to turn on
* digitalWrite to LOW to turn off

So there is something like the 10K resistor built-in the board to avoid using an extra resistor on the board to make sure the switch values are on or off.

<h3>Switch Issues</h3>

* Switches can bounce and give and off values while switching
* Noise can give false results
* More a problem when switching needs to be counted
* Use timer to solve issue (time = millis())

<h3>Analog Inputs & Potentiometer </h3>

* Can read values via analogRead
* Result is in range 0 to 1023 (10 bits)
* Potentiometer is Variable resistor
* Eg Read potentiometer values with Analog Inputs


``` javascript
int led = 3;
int pot = 0;

void setup() {
  Serial.begin(9600);
  pinMode(led, OUTPUT);
}

void loop() {
    int value = analogRead(pot);
    digitalWrite(led, HIGH);    
    // Set delay based on analog input
    delay(value);
    digitalWrite(led, LOW);  
    delay(value);
}  
```

So now when the potentiometer is turned to the right a value of 1023 is returned and the lights blinks on and off for about 1 seconds. Turning to the left makes the delay shorted (down to 0) and you can get it to run blink really fast.

<div style="text-align:center;"><img src="http://onrails.org/files/potentiometer.png" alt="potentiometer.png" border="0" width="400" height="300" /></div>

<h3>LDR</h3>

* Light dependent resistor (high resistance)
* Set flash rate based on value of LDR

This is a great full day tutorial and everyone seems to have fun. It's pretty basic, but it's the first time I program hardware. 

Now we are writing fadeIn and fadeOut functions and get the light to pulse on and off

<pre>
void fadeIn(int led) {
  for (int i=0; i<256; i++) {
    analogWrite(led, i);
    delayMicroseconds(5000);
  }
}

void fadeOut(int led) {
  for (int i=255; i >= 0; i--) {
    analogWrite(led, i);
    delayMicroseconds(5000);
  }
}

void loop() {
    fadeIn(led);    
    fadeOut(led);  
}  
</pre>

Now we replace the light sensor by a temperature sensor. There are also air quality sensors, breathalyzers.

<h3>Flex</h3>

Communication between Flex and Arduinos. 

* Software on Arduino (Firmata)
* USB serial to socket proxy
* Flex event based library to talk to socket (as3Glue)

Firmata is an Arduino library that support a binary protocol over serial interface. It's Bi-directiona. Use version 2. 

In the Arduino IDE let's load the StandardFirmata program (File|Examples|Firmata|StandardFirmata). It's a 286 lines program similar to the code we wrote so far, but more complex.

Server Proxy

From http://arduino.cc/en/Main/Software the server proxy (end of page)

To configure proxy first find what your serial device is. 
In terminal do: ls /dev/cu*

/dev/cu.Bluetooth-Modem         
/dev/cu.Bluetooth-PDA-Sync      
/dev/cu.usbserial-A600ailA

Then add this line to your serproxy.cfg:
serial_device=/dev/cu.usbserial-A600ailA

Then we just start the server proxy:
$ ./serproxy 
Serproxy - (C)1999 Stefano Busti, (C)2005 David A. Mellis - Waiting for clients

Now in Flex you need to add the as3glue code (http://code.google.com/p/as3glue/) then you can drive arduino as follows:

<pre>
private var arduino:Arduino = new Arduino();

private function init():void {
	arduino.addEventListener(ArduinoEvent.FIRMWARE_VERSION, turnLedOn);			
}

private function turnLedOn(event:ArduinoEvent):void {
	arduino.setPinMode(13, Arduino.OUTPUT);
	arduino.writeDigitalPin(13, Arduino.HIGH);
}
</pre>

A qik look at the class room in the middle of coding their Flex app to drive their Arduino device:

<object classid="clsid:d27cdb6e-ae6d-11cf-96b8-444553540000" codebase="http://download.macromedia.com/pub/shockwave/cabs/flash/swflash.cab#version=9,0,115,0" width="425" height="319" id="qikPlayer" align="middle"><param name="allowScriptAccess" value="sameDomain" /><param name="allowFullScreen" value="true" /><param name="movie" value="http://qik.com/swfs/qikPlayer5.swf" /><param name="quality" value="high" /><param name="bgcolor" value="#333333" /><param name="FlashVars" value="streamID=515f621ccf514b6b8ad9dfb0c62ad851&amp;autoplay=false" /><embed src="http://qik.com/swfs/qikPlayer5.swf" quality="high" bgcolor="#333333" width="425" height="319" name="qikPlayer" align="middle" allowScriptAccess="sameDomain" allowFullScreen="true" type="application/x-shockwave-flash" pluginspage="http://www.macromedia.com/go/getflashplayer" FlashVars="streamID=515f621ccf514b6b8ad9dfb0c62ad851&amp;autoplay=false"></embed></object>



Now we are going to write some Flex code to have some buttons that turn on/off some functions of the board.

<pre>
private var arduino:Arduino = new Arduino();
private const pin:int = 3;
private const button:int = 4;


private function arduinoInit(event:Event):void {
	arduino.enableDigitalPinReporting();
	arduino.setPinMode(pin, Arduino.OUTPUT);
	arduino.setPinMode(button, Arduino.INPUT);
	
	arduino.addEventListener(ArduinoEvent.DIGITAL_DATA, buttonChanged);
}

private function buttonChanged(event:ArduinoEvent):void {
	if (event.pin==button) {
		event.value == Arduino.HIGH ? turnOn() : turnOff();
	}
}

private function turnOn():void {
	arduino.writeDigitalPin(pin, Arduino.HIGH);
}

private function turnOff():void {
	arduino.writeDigitalPin(pin, Arduino.LOW);
}
</pre>


Thanks Justin, great talk!


