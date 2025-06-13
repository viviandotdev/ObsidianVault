---
created: 2024-06-22 12:22
modified: 2025-06-13T06:27:16-04:00
alias: 
---
**up**::  [[Arduino Tutorial]]
links::
## 30 Understanding and Using Servos in Projects

![[Screenshot 2024-06-22 at 12.22.41 PM.png]]
```c++
#include <Servo.h>

Servo myservo;  // create servo object to control a servo

int servoPin = 2; // Servo is connected to pin 2

void setup() {
  myservo.attach(servoPin);  // attaches the servo on pin 9 to the servo object
}

void loop() {
  myservo.write(90); // Set servo to middle position (stop for continuous rotation servos)
  delay(1000);
  // For continuous rotation servos, use these values to control direction and speed:
  // myservo.write(0);   // Full speed clockwise
  // myservo.write(180); // Full speed counter-clockwise
  // myservo.write(90);  // Stop
}
```


### Links to this page
These notes point directly to this note. But this note doesn't point back.
```dataview
LIST
FROM [[#]]
and !outgoing([[#]])
and -#map

SORT file.link asc
```



