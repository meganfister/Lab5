# Lab 5
## The Brain: Microcontrollers 
Aashika Uppala, Megan Fister

3/5/2025

### Introduction
The purpose of this lab is to explore the fundamentals of microcontrollers using the Arduino RedBoard. Microcontrollers are small computing devices that can process inputs, execute programmed instructions, and control output components. In this experiment, we used the Arduino IDE to program the microcontroller, focusing on key functions such as digital output, analog input, and Pulse Width Modulation (PWM). The primary goal was to control an LED using various input devices, including a potentiometer and a photoresistor. By analyzing different circuit configurations, we gained hands-on experience with converting analog signals to digital outputs and understanding the persistence of vision effect. This lab provided essential knowledge of embedded systems, which are widely used in industrial automation, IoT applications, and consumer electronics.
### Methods/Results
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
First, we assembled our RedBoard and breadboard onto the sparkfun base.
Next, we connected the RedBoard to the computer using the USB port and started the Arduino IDE on the computer.
Then, we selected the board Arduino UNO (Tools>Board>Arduino Uno) and the correct COM port (Tools>Port>COM?).
To access the code, we opened the blink program (File>Examples>Basics>Blink) and download it to the Arduino.
After connecting the Arduino, we built a simple circuit by connecting a 330Ω and an LED in series to pin 13 in our RedBoard, making sure to connect the ground. The circuit with the LED light flashing on is pictured below.

![LED On](https://github.com/meganfister/Lab5/blob/main/Lab%205%20LED%20On.jpg)

With the uploaded code, our LED flashes with a delay. We gradually reduced the initial 1000 ms delay until the blinking was so rapid that the LED appeared to stay continuously illuminated. The final delay was set to 11 ms. The updated code is shown below.
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


##### Part 2 – Controlling an LED with a potentiometer
Next, without taking apart our previous circuit, we connected our potentiometer to power (5V and Ground) with the variable resistance pin connected to A0. This connection is described in the program, the
example page at https://docs.arduino.cc/built-in-examples/basics/AnalogReadSerial/, or in the SparkFun Inventor’s kit book. Then, we opened the sample program Analog Read Serial (Examples>Basics>AnalogReadSerial) and ran it on the Arduino. To demonstrate this program operating properly, we opened the serial monitor (Tools>Serial Monitor) and watched the values vary between 0 and 1023 as we turned the potentiometer. We made sure to verify that the Baud Rate on the serial monitor is 9600bps. Pictured below is the circuit we built to control an LED with a potentiometer.

![Potentiometer](https://github.com/meganfister/Lab5/blob/main/Lab%205%20Potentiometer.jpg)

Bloew is the code to control the LED and set the blinking time to the value read from the potentiometer.
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

##### Part 3 – Controlling an LED with a photoresistor
Using the program from part 2, we replaced the potentiometer with a photoresistor in series with a 10 kΩ resistor. We connected the 5V pin to the photoresistor, ground to the resistor, and A0 to the node between them. The analog input is connected to the node between the photodetector and the resistor. We used different objects to block the light on the photoresistor. The minimum value we detected with this circuit was 532 and the maximum analog value we detected was 826. Pictured below is the circuit with both the photoresistor covered and uncovered.

![Photoresistor Covered](https://github.com/meganfister/Lab5/blob/main/Lab%205%20Covering%20PR.jpg)

![Photoresistor Uncovered](https://github.com/meganfister/Lab5/blob/main/Lab%205%20Uncovering%20PR.jpg)

We added an if else statement to our code (as shown in the SparkFun Inventor’s kit book) to turn on the LED only when the brightness sensed by the photoresistor is low, as a night light would work. The updated code is shown below.
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
##### Part 4 - LED Dimmer Using PWM
Using the circuit from Part 2 with the potentiometer, we changed the LED connection to a PWM-capable pin to enable brightness control. We read the voltage from the potentiometer and used the map() function to scale its value from the 0–1023 range (analog input) to a 0–255. Finally, we used the analogWrite() function to send the mapped value to the LED pin, allowing the LED’s brightness to vary based on the potentiometer’s position.
The built circuit is pictured below.

![LED Dimmer using PWM](https://github.com/meganfister/Lab5/blob/main/Lab%205%20LED%20Dimmer%20using%20PWM.jpg)

Finally, we connected the oscilloscope to the LED pin and observed that the signal and LED brightness both increased as we turned the knob of the potentiometer. The graphs from the oscilloscope are pictured below.

![PWM Low](https://github.com/meganfister/Lab5/blob/main/Lab%205%20PWM%20Low.jpg)

![PWM High](https://github.com/meganfister/Lab5/blob/main/Lab%205%20PWM%20High.jpg)

Below is the adjusted code for adjusting the brightness of the LED with the potentiometer.

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

_a. What does this program do?_

Turns an LED on for one second, then off for one second, repeatedly.

_b. What are the major sections of the computer program and what does each section do?_

The first section of the program is setup. It initializes digital pin LED_BUILTIN as an output. The next section is a loop that runs forever. It turns the LED on by making the voltage high, waits for a set period of time (currently one second) and then it turns the LED off by making the voltage slow and waits another second before repeating.

_a. What is the value of your delay now?_

11 ms

_b. What field may this “persistence of vision” play a greater role in?_

In LED displays and signage, "persistence of vision" can play a greater role by creating smooth scrolling texts and images. 

_c. Discuss this further in your lab report._

In the lab, when reducing the delay in the LED blink program, the LED eventually appears constantly illuminated rather than visibly blinking. This happens because the human eye can only distinguish individual flashes up to a certain frequency (typically around 60 Hz or 16ms per cycle). When the LED blinks faster than this threshold, the brain perceives it as a steady light rather than a blinking one.
#### Part 2 - Controlling an LED with a potentiometer
_a. What is the difference between an analog and a digital signal?_

An analog signal is continuous and can take any value within a given range (ex.: sound waves, temperature variations).

A digital signal is discrete, typically represented as binary (0s and 1s) (ex.: computer data, ON/OFF signals).

_b. In your lab report, list a few examples of real-world examples that can be described by an analog signal. Likewise, what are the two states which can be conveyed by a digital signal?_

**Analog Examples:**

- Sound waves from a microphone.

- Temperature variations measured by a thermometer.

- Light intensity captured by a photoresistor.

- Voltage fluctuations in power supplies.


**Digital Signal States:**

HIGH (1) – Typically 5V in Arduino.

LOW (0) – Typically 0V in Arduino.

_c. What happens to the Serial Monitor Refresh rate as you move the potentiometer to control the LED blinking time?_

The Serial Monitor refresh rate changes depending on the delay between each reading. 

As the potentiometer's resistance changes:

If the delay increases, the serial monitor updates slower.

If the delay decreases, the serial monitor updates faster.
#### Part 3 - Controlling an LED with a photoresistor
_a. Does the LED turn on immediately after blocking the light? What about when you remove the object blocking the light, does the LED turn off immediately? Why?_

No, the LED does not always turn on or off immediately. This delay happens because: The photoresistor gradually changes resistance instead of instantaneously reacting;
External light intensity variations may cause minor fluctuations; The circuit may have capacitive effects, leading to a slight delay in response.
#### Part 4 - LED dimmer using PWM
_a. Observations:_

The oscilloscope will show a PWM waveform with a varying duty cycle.

**As the potentiometer increases:**

The duty cycle increases.

The LED brightness increases (closer to full brightness).

**As the potentiometer decreases:**

The duty cycle decreases.

The LED dims (closer to OFF state).

The frequency of the PWM signal remains the same, but the ON-time duration changes.
### Conclusion
The purpose of this lab is to explore the fundamentals of microcontrollers using the Arduino RedBoard. Microcontrollers are small computing devices that can process inputs, execute programmed instructions, and control output components. In this experiment, we used the Arduino IDE to program the microcontroller, focusing on key functions such as digital output, analog input, and Pulse Width Modulation (PWM). The primary goal was to control an LED using various input devices, including a potentiometer and a photoresistor. By analyzing different circuit configurations, we gained hands-on experience with converting analog signals to digital outputs and understanding the persistence of vision effect. This lab provided essential knowledge of embedded systems, which are widely used in industrial automation, IoT applications, and consumer electronics.
