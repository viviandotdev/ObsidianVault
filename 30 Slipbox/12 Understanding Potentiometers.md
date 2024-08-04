---
created: 2024-06-22 11:39 
modified: Saturday 22nd June 2024 11:39:46
alias: 
---
up::  [[Arduino Tutorial]]
type:: 
links::
## 12 Understanding Potentiometers
It has two resistors in it, as you turn the knob the voltage measured between the two resistors change.
V = IR
Vout = IR
![[Screenshot 2024-06-22 at 11.45.52 AM.png]]

Output read from the potentiometer will be from 0 - 5V depending on which way the knob is turned.
If the knob is in the middle the output will be 2.5V
![[Screenshot 2024-06-22 at 11.41.17 AM.png]]
```c++
const int potPin = A0; // Analog pin connected to the potentiometer

void setup() {
  Serial.begin(9600); // Initialize serial communication
}

void loop() {
  int sensorValue = analogRead(potPin); // Read the voltage from the potentiometer
  float voltage = sensorValue * (5.0 / 1023.0); // Convert the reading to voltage

  Serial.print("Potentiometer Voltage: ");
  Serial.print(voltage);
  Serial.println(" V");

  delay(100); // Delay for stability
}
```
**Notes**
`float voltage = sensorValue * (5.0 / 1023.0);` This line converts the raw analog value (sensorValue) to a voltage value. It does this by multiplying the sensor value by the conversion factor (5.0 / 1023.0). The Arduino's analog input reads values between 0 and 1023, representing a voltage range of 0 to 5 volts.

### Links to this page
These notes point directly to this note. But this note doesn't point back.
```dataview
LIST
FROM [[#]]
and !outgoing([[#]])
and -#map

SORT file.link asc
```



