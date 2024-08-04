---
created: 2024-06-20 07:12 
modified: Thursday 20th June 2024 07:12:07
alias: 
---
up::  
type:: #note/atomic🌳 
links::
## 35 Stepper Motors


# Arduino Tutorial 35: Understanding How to Use a Stepper Motor
![](https://i.ytimg.com/vi/CEz1EeDlpbs/hqdefault.jpg)



[Source URL](https://www.youtube.com/watch?v=CEz1EeDlpbs&list=PLGs0VKk2DiYw-L-RibttcvK-WBZm8WLEP&index=35)

## What are stepper motors [(00:01:05)](https://www.youtube.com/watch?v=CEz1EeDlpbs&t=65s)
- Stepper motors allow for precise control of position and have high torque at low RPMs.
- Unlike servos, stepper motors have limited range of motion and are not as positionally accurate or strong.
- Stepper motors are tricky to use, draw a lot of current, and require an external power supply.
- Each stepper motor has unique parameters and requires a matching stepper motor driver.
- Larger stepper motors, like those used in 3D printers and CNC machines, require specialized drivers like the Easy Driver or Big Easy Driver.
- Stepper motors are used in various applications such as CNC machines, 3D printers, and laser engravers.
- These applications require precise movement with high torque, which stepper motors provide.
## What you will need [(00:05:12)](https://www.youtube.com/watch?v=CEz1EeDlpbs&t=312s)
- Power supply from the Lego kit.
- Switch.
- Stepper motor driver.
- Stepper motor.
- Arduino.
- 9-volt battery.
- Clip to connect the 9-volt battery to the power supply.
- Ribbon cable.
- All components must share a common ground to function properly.
- Arduino has a ground that must be connected to the ground of other components.
- Power supply has positive and negative rails that must match the positive and negative labels on the Arduino.
- Connect a ground wire from the power supply to the GND pin on the Arduino to establish a common ground.
## Connecting the stepper motor [(00:08:00)](https://www.youtube.com/watch?v=CEz1EeDlpbs&t=480s)
- Connect the stepper motor to the stepper driver, ensuring proper alignment.
- Connect the stepper motor driver to the Arduino using a ribbon cable, matching the corresponding pins.
- Power the stepper motor driver by connecting the negative pin to the ground rail and the second outside pin to the 5V power supply rail.
- Ensure that the power supply is turned on and the battery is plugged in.
- Verify all connections: the motor is connected to the driver, the driver is powered, and the Arduino pins are correctly connected.
- The stepper motor requires a 5-volt power supply.
## Load a library [(00:15:00)](https://www.youtube.com/watch?v=CEz1EeDlpbs&t=900s)
- To use a stepper motor, load the stepper library using the `#include` directive.
- Unlike other directives, `#include` does not end with a semicolon.
## Stepper motor parameter [(00:16:00)](https://www.youtube.com/watch?v=CEz1EeDlpbs&t=960s)
- Determine the steps per revolution for the specific stepper motor being used.
- This value is unique to each motor and can be found in its datasheet.
- For the 28BYJ-48 stepper motor used in the video, the steps per revolution is 2048.
## Stepper command [(00:17:00)](https://www.youtube.com/watch?v=CEz1EeDlpbs&t=1020s)
- Create a stepper object using the `Stepper` command from the stepper library.
- Specify the steps per revolution for the motor.
- Define the pin sequence for the motor driver.
- The pin sequence depends on the specific motor and driver combination.
## Stepper speed [(00:18:00)](https://www.youtube.com/watch?v=CEz1EeDlpbs&t=1080s)
- Set the speed of the stepper motor using the `setSpeed()` method.
- The speed is measured in revolutions per minute (RPM).
- Stepper motors typically have a limited maximum speed.
## mote speed [(00:19:00)](https://www.youtube.com/watch?v=CEz1EeDlpbs&t=1140s)
- Define the variable `moteSpeed` as an integer and assign it a value in RPM.
- In the example, `moteSpeed` is set to 10 RPM.
## Move the stepper motor [(00:20:00)](https://www.youtube.com/watch?v=CEz1EeDlpbs&t=1200s)
- Use the `step()` method to move the stepper motor.
- The number of steps specified determines the amount of rotation.
- For example, specifying 2048 steps would cause the motor to complete one full revolution.
## steps per revolution [(00:20:00)](https://www.youtube.com/watch?v=CEz1EeDlpbs&t=1200s)
- The `steps per revolution` is a variable that determines the number of steps the stepper motor takes to complete one revolution.
- In the example, the `steps per revolution` is set to 2048.
## holdyourbreath [(00:22:00)](https://www.youtube.com/watch?v=CEz1EeDlpbs&t=1320s)
- The stepper motor successfully runs one revolution in the positive direction and one revolution in the negative direction.
## maketoorder [(00:23:00)](https://www.youtube.com/watch?v=CEz1EeDlpbs&t=1380s)
- The stepper motor takes 6 seconds to complete one revolution, which is 10 RPM.
- Changing the `steps per revolution` to half the value makes the stepper motor rotate half a revolution.
- Changing the motor speed to 2 RPM and 3 RPM changes the speed of the stepper motor accordingly.
## toggle [(00:25:00)](https://www.youtube.com/watch?v=CEz1EeDlpbs&t=1500s)
- The homework assignment is to incorporate a button into the project that toggles the direction of the stepper motor.
- Pressing the button once makes the motor run forward continuously, pressing it again makes the motor run backward continuously.
- Hints are provided on where to find information about buttons in previous lessons.
## Leave a comment [(00:26:00)](https://www.youtube.com/watch?v=CEz1EeDlpbs&t=1560s)
- The instructor encourages viewers to try the project on their own and share their results in the comments section.
- Viewers are asked to specify if they were able to complete the project without watching the video, and if they used the same method or a different approach.
## Connecting the ground [(00:28:00)](https://www.youtube.com/watch?v=CEz1EeDlpbs&t=1680s)
- The instructor connects one leg of the button to pin 2 on the Arduino and the other leg to the common ground.
## Motor direction [(00:29:00)](https://www.youtube.com/watch?v=CEz1EeDlpbs&t=1740s)
- The instructor explains the need for a variable to keep track of the motor's direction.
- The variable `motor_direction` is introduced, with a value of 1 indicating clockwise direction and -1 indicating counterclockwise direction.
- The initial direction is set to clockwise.
## Where was the button [(00:30:00)](https://www.youtube.com/watch?v=CEz1EeDlpbs&t=1800s)
- The instructor discusses the need to track the button's state (pressed or not pressed) and introduces the variables `button_val_new` and `button_val_old`.
- `button_val_new` represents the current state of the button, while `button_val_old` represents the state of the button during the previous loop iteration.
- To initialize the program, `button_val_old` is set to a value of 1 (not pressed).
## The crazy thing [(00:31:00)](https://www.youtube.com/watch?v=CEz1EeDlpbs&t=1860s)
- To use a button as an input, set the pin mode to input and then do a digital read from it.
- Setting the pin mode to input and then writing to it high effectively puts a pull-up resistor in there, which is what is needed.
## The void loop [(00:32:00)](https://www.youtube.com/watch?v=CEz1EeDlpbs&t=1920s)
- In the void loop, the first thing to do is to figure out where the button is by doing a digital read of the button and storing the value in a variable.
- If the previous value of the button was 1 (not pressed) and the new value is 0 (pressed), it means the button has been pressed and the direction should be changed.
## Changing directions [(00:33:00)](https://www.youtube.com/watch?v=CEz1EeDlpbs&t=1980s)
- To avoid changing directions multiple times while the button is held down, the direction should only be changed when the button transitions from not pressed to pressed.
## Changing motor direction [(00:34:00)](https://www.youtube.com/watch?v=CEz1EeDlpbs&t=2040s)
- To change the motor direction, multiply the `motorDirection` variable by -1.
- This will reverse the direction of the motor.
- The `motorDirection` variable can be either 1 or -1, indicating the positive or negative direction, respectively.
## Troubleshooting [(00:38:00)](https://www.youtube.com/watch?v=CEz1EeDlpbs&t=2280s)
- After updating the `buttonValNew` variable, it's important to assign it to the `buttonValOld` variable to keep track of the previous button state.
- This ensures that the button press is detected correctly and the motor direction changes as expected.
## Conclusion [(00:39:00)](https://www.youtube.com/watch?v=CEz1EeDlpbs&t=2340s)
- Palmer asks viewers if they were able to complete the project on their own.
- He encourages viewers to like the video and subscribe to the channel.
- Palmer suggests sharing the video with others.

### Links to this page
These notes point directly to this note. But this note doesn't point back.
```dataview
LIST
FROM [[#]]
and !outgoing([[#]])
and -#map

SORT file.link asc
```



