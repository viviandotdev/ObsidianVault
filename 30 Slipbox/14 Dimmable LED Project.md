---
created: 2024-06-22 11:22 
modified: Saturday 22nd June 2024 11:22:08
alias: 
---
up::  [[Arduino Tutorial]]
type:: #note/atomic🌳 
links::
## 14 Dimmable LED Project

**Circuit Diagram**
![[Screenshot 2024-06-22 at 11.27.02 AM.png|800]]

**Code**
```c++
int potPin =  A1; //analog read 
int rPin = 3; //analog write pin (~) 
int potVal; //(0, 1023) 
float LEDVal; //(0, 255)

// setup the pins
void setup() {
	pinMode(potPin, INPUT);
	pinMode(rPin, OUTPUT);
	Serial.begin(9600);
}

void loop() {
	// read data from the potentiometer
	potVal = analogRead(potPin)
	//Convert that input data to a values from (0, 255)
	LEDVal = (255./1023.) * potVal
	analogWrite(rPin, LEDVal)
	Serial.println(LEDVal);
	
}
```

Find on the slope of the line to get the equation to to the potVal to the LEDVal
![[Screenshot 2024-06-22 at 11.35.58 AM.png]]
### Links to this page
These notes point directly to this note. But this note doesn't point back.
```dataview
LIST
FROM [[#]]
and !outgoing([[#]])
and -#map

SORT file.link asc
```



