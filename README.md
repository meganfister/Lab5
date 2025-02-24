# Lab5
Laboratory 4. Go Big: Operational Amplifiers 
Aashika Uppala, Megan Fister
2/24/2025
Part 1
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
Introduction
Operational amplifiers (Op-Amps) are fundamental components in analog electronics, used for signal amplification, filtering, and mathematical operations. 
This lab explores the functionality and limitations of Op-Amps through various circuit configurations, including inverting amplifiers, voltage followers, integrators, and differentiators. The LM741, a widely used general-purpose Op-Amp, serves as the primary component in these experiments.
The objectives of this lab contain:
Understand the behavior of Op-Amps in different circuit configurations.
Measure and compare the experimental gain with theoretical values.
Investigate the voltage and frequency limitations of the LM741 Op-Amp.
Analyze how Op-Amps perform mathematical operations such as integration and differentiation.
By constructing and testing these circuits, students will develop a deeper understanding of the practical considerations and limitations of Op-Amp-based designs in real-world applications.

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



Part 2
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


Part 3
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


Part 4
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

Discussion
Part 1
a. The moderate gain amplifier (with a higher resistor ratio) should exhibit a larger gain, and oscilloscope measurements should confirm it.
The high gain amplifier may show deviations at extreme voltages due to saturation effects. For the unity gain inverting amplifier, the expected gain is -1, and measured values should confirm this. Deviations may arise due to tolerances in resistor values, non-ideal characteristics of the LM741 (e.g., offset voltage and input bias currents), and limitations in measurement accuracy.
b. The LM741 cannot output voltages equal to the supply rails due to output voltage swing limitations. Typically, the output voltage is limited to within 1-2V of the supply voltage. At high gain settings, the output may saturate quickly when the input voltage exceeds a certain threshold, leading to distortion.
c. Ideally, an op-amp should have symmetric performance. n reality, LM741 may show asymmetry due to differences in internal transistor behavior, bias currents, and small mismatches in fabrication. This can be observed by checking if the positive and negative output swings reach the same absolute voltage levels. In this case, we saw some asymmetry due to internal transistor behavior. 
Part 2
The integrator performed by for a sine wave input, the output should be a cosine wave (phase-shifted by 90°). For a triangle wave input, the output should be a parabolic wave. Deviations can occur due to DC drift and practical limits of the op-amp. 
The differentiator performed for a sine wave input, the output should be a cosine wave (also phase-shifted by 90°).
For a triangle wave input, the output should be a square wave. At high frequencies, the differentiator may become unstable due to noise amplification.

Conclusion
This lab provided hands-on experience with various Op-Amp circuits and demonstrated their theoretical and practical behaviors. The experimental gain values generally aligned with theoretical calculations, though minor deviations occurred due to component tolerances and Op-Amp limitations. The voltage follower exhibited unity gain as expected, but the LM741’s bandwidth constraints became evident at higher frequencies.
The inverting amplifier circuits demonstrated predictable gain characteristics, but output voltage limitations prevented full utilization of the supply range.
The integrator and differentiator circuits effectively performed mathematical operations on input signals, though performance degraded at high frequencies due to noise amplification and slew rate limitations.
Overall, this lab highlighted the capabilities and practical constraints of Op-Amps, reinforcing key concepts in analog circuit design. Understanding these limitations is crucial for designing stable and efficient amplifier circuits in real-world applications.
