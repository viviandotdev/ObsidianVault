---
created: 2024-06-22 12:10 
modified: Saturday 22nd June 2024 12:10:10
alias: 
---
up::  [[Arduino Tutorial]]
links::
## 20 Understanding RGB LED's
![[Screenshot 2024-06-22 at 12.20.35 PM.png]]
```c++
// Define the RGB LED pins
const int redPin = 6;
const int greenPin = 5;
const int bluePin = 3;

void setup() {
  // Set the LED pins as outputs
  pinMode(redPin, OUTPUT);
  pinMode(greenPin, OUTPUT);
  pinMode(bluePin, OUTPUT);

  // Start serial communication
  Serial.begin(9600);
}

void loop() {
  // Prompt the user to enter a color
  Serial.println("What color would you like? (red, green, blue)");

  // Wait for user input
  while (Serial.available() == 0) {
    // Do nothing until input is received
  }

  // Read the color input from the serial monitor
  String color = Serial.readStringUntil('\n');

  // Convert the input to lowercase for case-insensitive comparison
  color.toLowerCase();

  // Update LED color based on the user input
  if (color == "red") {
    setColor(255, 0, 0);
    Serial.println("LED color set to red.");
  } else if (color == "green") {
    setColor(0, 255, 0);
    Serial.println("LED color set to green.");
  } else if (color == "blue") {
    setColor(0, 0, 255);
    Serial.println("LED color set to blue.");
  } else {
    // Turn off the LED for invalid input
    setColor(0, 0, 0);
    Serial.println("Invalid color entered. LED turned off.");
  }
}

// Function to set the RGB LED color
void setColor(int redValue, int greenValue, int blueValue) {
  analogWrite(redPin, redValue);
  analogWrite(greenPin, greenValue);
  analogWrite(bluePin, blueValue);
}
```