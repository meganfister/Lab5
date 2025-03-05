# Lab 5
## The Brain: Microcontrollers 
Aashika Uppala, Megan Fister

3/5/2025

### Introduction
The purpose of this lab is to explore the fundamentals of microcontrollers using the Arduino RedBoard. Microcontrollers are small computing devices that can process inputs, execute programmed instructions, and control output components. In this experiment, we used the Arduino IDE to program the microcontroller, focusing on key functions such as digital output, analog input, and Pulse Width Modulation (PWM). The primary goal was to control an LED using various input devices, including a potentiometer and a photoresistor. By analyzing different circuit configurations, we gained hands-on experience with converting analog signals to digital outputs and understanding the persistence of vision effect. This lab provided essential knowledge of embedded systems, which are widely used in industrial automation, IoT applications, and consumer electronics.
### Methods
#### Instruments
• A 330Ω resistor

• An oscilloscope

• A Computer running Arduino IDE

• SparkFun Inventor’s kit

&nbsp; &nbsp; &nbsp; &nbsp; o RedBoard

&nbsp; &nbsp; &nbsp; &nbsp; o Photoresistor
  
&nbsp; &nbsp; &nbsp; &nbsp; o An LED
  
&nbsp; &nbsp; &nbsp; &nbsp; o A 10 kΩ potentiometers
  
&nbsp; &nbsp; &nbsp; &nbsp; o A momentary button
  
&nbsp; &nbsp; &nbsp; &nbsp; o Resistors: 10 kΩ
#### Objective: Familiarize yourself with the Arduino IDE and Red Board (Arduino UNO).
Task:

• Upload a program code and successfully blink an LED on your Arduino system.

• Convert analog inputs to digital signals.

• Familiarize yourself with the concept of pulse width modulation.
##### Part 1 - Blinking an LED
1. Assemble your RedBoard and breadboard onto the sparkfun base.
2. Connect the RedBoard to the computer and start the Arduino IDE on the computer.
3. Select the board Arduino UNO (Tools>Board>Arduino Uno) and the correct COM port (Tools>Port>COM?).
Figure 1. PWM FOR 0%, 25%, 50%, 75%, AND 100%
(https://docs.arduino.cc/learn/microcontrollers/analog-output/)
4. Open the blink program (File>Examples>Basics>Blink) and download it to the Arduino.
a. What does this program do?
b. What are the major sections of the computer program and what does each section do?

##### Part 2 – Controlling an LED with a potentiometer
1. Open the sample program Analog Read Serial (Examples>Basics>AnalogReadSerial) and run it on the
Arduino.
a. Do not take apart your previous circuit and connect your potentiometer to power (5V and Ground)
with the variable resistance pin connected to A0. This connection is described in the program, the
example page at https://docs.arduino.cc/built-in-examples/basics/AnalogReadSerial/, or in the
SparkFun Inventor’s kit book.
b. Demonstrate this program operating properly using the serial monitor (Tools>Serial Monitor). Verify
that the Baud Rate on the serial monitor is 9600bps.
c. Include the code to control the LED and set the blinking time to the value read from the
potentiometer.
##### Part 3 – Controlling an LED with a photoresistor
1. Use the program from part 2 and replace the potentiometer with a photoresistor in series with a 10 kΩ resistor. Connect the 5V pin to the photoresistor, ground to the resistor, and A0 to the node between them. The analog input should be connected to the node between the photodetector and the resistor.

3. Try different objects to block the light on the photoresistor. What are the minimum and maximum analog values you can detect with this circuit?

4. Use an if else statement as shown in the SparkFun Inventor’s kit book to turn on the LED only when the brightness sensed by the photoresistor is low. As a night light would work.
### Results

Part 1
```c++
/*
  Blink

  Turns an LED on for one second, then off for one second, repeatedly.

  Most Arduinos have an on-board LED you can control. On the UNO, MEGA and ZERO
  it is attached to digital pin 13, on MKR1000 on pin 6. LED_BUILTIN is set to
  the correct LED pin independent of which board is used.
  If you want to know what pin the on-board LED is connected to on your Arduino
  model, check the Technical Specs of your board at:
  https://www.arduino.cc/en/Main/Products

  modified 8 May 2014
  by Scott Fitzgerald
  modified 2 Sep 2016
  by Arturo Guadalupi
  modified 8 Sep 2016
  by Colby Newman



  This example code is in the public domain.

  https://www.arduino.cc/en/Tutorial/BuiltInExamples/Blink
*/

// the setup function runs once when you press reset or power the board
void setup() {
  // initialize digital pin LED_BUILTIN as an output.
  pinMode(LED_BUILTIN, OUTPUT);
}

// the loop function runs over and over again forever
void loop() {
  digitalWrite(LED_BUILTIN, HIGH);  // turn the LED on (HIGH is the voltage level)
  delay(11);                      // wait for a second
  digitalWrite(LED_BUILTIN, LOW);   // turn the LED off by making the voltage LOW
  delay(11);                      // wait for a second
}
```


Part 2
```c++
/*
  AnalogReadSerial

  Reads an analog input on pin 0, prints the result to the Serial Monitor.
  Graphical representation is available using Serial Plotter (Tools > Serial Plotter menu).
  Attach the center pin of a potentiometer to pin A0, and the outside pins to +5V and ground.

  This example code is in the public domain.

  https://www.arduino.cc/en/Tutorial/BuiltInExamples/AnalogReadSerial
*/

// the setup routine runs once when you press reset:
void setup() {
  // initialize serial communication at 9600 bits per second:
  Serial.begin(9600);
    // initialize digital pin LED_BUILTIN as an output.
  pinMode(LED_BUILTIN, OUTPUT);
}

// the loop routine runs over and over again forever:
void loop() {
  
  // read the input on analog pin 0:
  int sensorValue = analogRead(A0);
  // print out the value you read:
  Serial.println(sensorValue);
  delay(1);  // delay in between reads for stability
    digitalWrite(LED_BUILTIN, HIGH);  // turn the LED on (HIGH is the voltage level)
  delay(sensorValue);                      // wait for a second
  digitalWrite(LED_BUILTIN, LOW);   // turn the LED off by making the voltage LOW
  delay(sensorValue);                      // wait for a second

}
```

Part 3
```c++
/*
  AnalogReadSerial

  Reads an analog input on pin 0, prints the result to the Serial Monitor.
  Graphical representation is available using Serial Plotter (Tools > Serial Plotter menu).
  Attach the center pin of a potentiometer to pin A0, and the outside pins to +5V and ground.

  This example code is in the public domain.

  https://www.arduino.cc/en/Tutorial/BuiltInExamples/AnalogReadSerial
*/

// the setup routine runs once when you press reset:
void setup() {
  // initialize serial communication at 9600 bits per second:
  Serial.begin(9600);
    // initialize digital pin LED_BUILTIN as an output.
  pinMode(LED_BUILTIN, OUTPUT);
}

// the loop routine runs over and over again forever:
void loop() {
 
  // read the input on analog pin 0:
  int sensorValue = analogRead(A0);
  // print out the value you read:
  Serial.println(sensorValue);
   if(sensorValue < 600){
//run if true

  delay(1);  // delay in between reads for stability
    digitalWrite(LED_BUILTIN, HIGH);  // turn the LED on (HIGH is the voltage level)
  delay(11);                      // wait for a second
  digitalWrite(LED_BUILTIN, LOW);   // turn the LED off by making the voltage LOW
  delay(11);                      // wait for a second
}
else{
//run if false
}
}
```

Part 4
```c++
/*
  AnalogReadSerial

  Reads an analog input on pin 0, prints the result to the Serial Monitor.
  Graphical representation is available using Serial Plotter (Tools > Serial Plotter menu).
  Attach the center pin of a potentiometer to pin A0, and the outside pins to +5V and ground.

  This example code is in the public domain.

  https://www.arduino.cc/en/Tutorial/BuiltInExamples/AnalogReadSerial
*/

// the setup routine runs once when you press reset:
void setup() {
  // initialize serial communication at 9600 bits per second:
  Serial.begin(9600);
    // initialize digital pin LED_BUILTIN as an output.
  pinMode(LED_BUILTIN, OUTPUT);
  pinMode(10, OUTPUT);
}

// the loop routine runs over and over again forever:
void loop() {
  
  // read the input on analog pin 0:
  int sensorValue = analogRead(A0);
  // print out the value you read:
  Serial.println(sensorValue);

int mappedvalue = map(sensorValue, 0, 1023, 0, 225);

  analogWrite(10, mappedvalue);
}
```

### Discussion
#### Part 1 - Blinking an LED
Open the blink program (File>Examples>Basics>Blink) and download it to the Arduino.

a. What does this program do?

b. What are the major sections of the computer program and what does each section do?

Your LED flashes with a delay from the uploaded code. Decrease this delay (after both write instructions) until the LED just stops blinking—that is until the light is still blinking but appears to stay constantly illuminated.

a. What is the value of your delay now?
11 ms
b. What field may this “persistence of vision” play a greater role in?
In LED displays and signage, "persistence of vision" can play a greater role by creating smooth scrolling texts and images. 
c. Discuss this further in your lab report.
In the lab, when reducing the delay in the LED blink program, the LED eventually appears constantly illuminated rather than visibly blinking. This happens because the human eye can only distinguish individual flashes up to a certain frequency (typically around 60 Hz or 16ms per cycle). When the LED blinks faster than this threshold, the brain perceives it as a steady light rather than a blinking one.
#### Part 2 - Controlling an LED with a potentiometer
a. What is the difference between an analog and a digital signal?
An analog signal is continuous and can take any value within a given range (ex.: sound waves, temperature variations).
A digital signal is discrete, typically represented as binary (0s and 1s) (ex.: computer data, ON/OFF signals).

b. In your lab report, list a few examples of real-world examples that can be described by an analog signal. Likewise, what are the two states which can be conveyed by a digital signal?
Analog Examples:
Sound waves from a microphone.
Temperature variations measured by a thermometer.
Light intensity captured by a photoresistor.
Voltage fluctuations in power supplies.
Digital Signal States:
HIGH (1) – Typically 5V in Arduino.
LOW (0) – Typically 0V in Arduino.

c. What happens to the Serial Monitor Refresh rate as you move the potentiometer to control the LED blinking time?
The Serial Monitor refresh rate changes depending on the delay between each reading. As the potentiometer's resistance changes:
If the delay increases, the serial monitor updates slower.
If the delay decreases, the serial monitor updates faster.
#### Part 3 - Controlling an LED with a photoresistor
a. Does the LED turn on immediately after blocking the light? What about when you remove the object blocking the light, does the LED turn off immediately? Why?
No, the LED does not always turn on or off immediately. This delay happens because: The photoresistor gradually changes resistance instead of instantaneously reacting;
External light intensity variations may cause minor fluctuations; The circuit may have capacitive effects, leading to a slight delay in response.
#### Part 4 - LED dimmer using PWM
a. Observations:
The oscilloscope will show a PWM waveform with a varying duty cycle.
As the potentiometer increases:
The duty cycle increases.
The LED brightness increases (closer to full brightness).
As the potentiometer decreases:
The duty cycle decreases.
The LED dims (closer to OFF state).
The frequency of the PWM signal remains the same, but the ON-time duration changes.
### Conclusion
The purpose of this lab is to explore the fundamentals of microcontrollers using the Arduino RedBoard. Microcontrollers are small computing devices that can process inputs, execute programmed instructions, and control output components. In this experiment, we used the Arduino IDE to program the microcontroller, focusing on key functions such as digital output, analog input, and Pulse Width Modulation (PWM). The primary goal was to control an LED using various input devices, including a potentiometer and a photoresistor. By analyzing different circuit configurations, we gained hands-on experience with converting analog signals to digital outputs and understanding the persistence of vision effect. This lab provided essential knowledge of embedded systems, which are widely used in industrial automation, IoT applications, and consumer electronics.
