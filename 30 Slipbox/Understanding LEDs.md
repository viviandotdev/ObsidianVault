---
created: 2024-06-19 07:51 
modified: Wednesday 19th June 2024 07:51:45
alias: 
---
up::  [[Arduino Tutorial]]
type:: #note/atomic🌳 
links::
## Understanding LEDS

Light emiting diode, has a + and - pin.
Attach shorter pin to ground and longer pin to voltage, this creates a current through the diode causing it to emit energy in the form of light as photons

To set up an LED light and turn it on using an Arduino, you'll need the following components:

1. Arduino board (e.g., Arduino Uno)
2. LED
3. 220 ohm resistor
4. Breadboard
5. Jumper wires
![[Screenshot 2024-06-19 at 8.17.19 AM.png]]

1. Connect the components:
   - Insert the LED into the breadboard.
   - Connect the (+)**anode** (longer leg)of the LED to one end of the 220 ohm resistor.
   - Connect the other end of the resistor to digital pin 13 on the Arduino. 
   - Connect the (-)**cathode** (shorter leg) of the LED to the GND (ground) pin on the Arduino.
	   - this is where we write the voltage

2. Open the Arduino IDE and create a new sketch.

3. Write the following code in the sketch:

```cpp
void setup() {
  pinMode(13, OUTPUT);  // Set pin 13 as an output
}

void loop() {
  digitalWrite(13, HIGH);  // Turn on the LED
}
```

4. Explanation of the code:
   - In the `setup()` function, we use `pinMode(13, OUTPUT)` to set digital pin 13 as an output pin. This is the pin where the LED is connected.
   - In the `loop()` function, we use `digitalWrite(13, HIGH)` to set the voltage on pin 13 to HIGH (5V), which turns on the LED.

5. Connect your Arduino board to your computer using a USB cable.

6. In the Arduino IDE, select the appropriate board and port under the "Tools" menu.

7. Click the "Upload" button to compile and upload the code to your Arduino board.

After uploading the code, the LED should turn on and stay on continuously.

You can modify the code to blink the LED or perform other patterns by using functions like `digitalWrite()` and `delay()`. For example, to blink the LED, you can modify the `loop()` function as follows:

```cpp
void loop() {
  digitalWrite(13, HIGH);  // Turn on the LED
  delay(1000);             // Wait for 1 second
  digitalWrite(13, LOW);   // Turn off the LED
  delay(1000);             // Wait for 1 second
}
```

This code will turn the LED on for 1 second, then turn it off for 1 second, and repeat the process indefinitely.

Remember to always include a current-limiting resistor when connecting an LED to prevent damage to the LED and the Arduino board.


### Links to this page
These notes point directly to this note. But this note doesn't point back.
```dataview
LIST
FROM [[#]]
and !outgoing([[#]])
and -#map

SORT file.link asc
```



