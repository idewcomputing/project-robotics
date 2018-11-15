# IR Line Sensors

The RedBot has three "line following" sensors \(left, center, and right\). The bottom of each sensor has an LED that transmits infrared \(IR\) light, which is invisible to the human eye. The bottom of each sensor also has an IR detector, which measures how much of the IR light is reflected back by the surface that the RedBot is driving on.

![](../../.gitbook/assets/line-sensor.jpg)

The amount of reflected IR light that is detected depends on several factors, including the color of the surface, as well as the distance between the sensor and the surface:

* A light-colored surface will reflect more IR light, while a dark-colored surface will reflect less IR light.
* If the surface is farther away, the IR light will become more scattered, and less IR light will be reflected back to the detector. Even a small increase in the distance between the sensor and the surface \(as little as 0.25 inch\) will greatly reduce the amount of reflected IR light.

The IR sensors can help the RedBot perform several useful tasks by comparing the measurements from the three IR sensors, in order to detect a line \(or other change in the surface\):

1. The RedBot can **follow a line** by adjusting the left and right motor powers to steer the RedBot and keep it centered on the line as it drives.
2. The RedBot can **avoid a line** by turning away from a line that it detects. In this case, lines act as "borders" to keep the RedBot inside \(or outside\) a certain path or area.
3. The RedBot can **count lines** that it crosses while driving and then stop once it reaches a desired line number.
4. The RedBot can **avoid driving over a drop-off** by stopping the motors if the IR sensor measurements are too high \(which may indicate the front of the RedBot is hanging over a table edge, stair step, or other drop-off\).
5. The RedBot can **detect different types of flat objects** on the surface by detecting their unique IR measurement range.

### How to Use the IR Sensors in a Program:

To use the IR sensors, you will need to: 1. Create `RedBotSensor` objects for each IR sensor 2. Use each sensor object's `read()` method to get a measurement 3. Add code to perform an action based on the IR sensor measurements

### Coding References in this Section:

* Create RedBotSensor Objects
* Check IR Sensor Measurements
* Use Serial Monitor to View IR Sensor Measurements
* Avoid Driving Over Drop-Off
* Follow Line Automatically
* Avoid Line Automatically
* Count Lines and Stop at Target Number
* Follow Line While Counting Lines Crossed
* Detect Flat Objects on Surface

## Create RedBotSensor Objects

The SparkFun `RedBot` library has a class named `RedBotSensor` which contains methods \(functions\) to control analog sensors, such as the IR line following sensors.

**IMPORTANT:** Be sure that your program includes a copy of the SparkFun `RedBot` library. If necessary, see the instructions for [how to include the RedBot library](redbot-library.md).

Before your `setup()` function, create a `RedBotSensor` object for each of line following sensor by assigning each to a variable and indicating its pin number:

```cpp
// IR line following sensors
RedBotSensor leftLine(A3);
RedBotSensor centerLine(A6);
RedBotSensor rightLine(A7);
```

* `RedBotSensor` indicates the class of object being created \(this class is part of the `RedBot` library\)
* `leftLine` represents a variable name for a `RedBotSensor` object, and `A3` indicates the pin number this sensor is connected to. If desired, you could use a different variable name.
* `centerLine` represents a variable name for a `RedBotSensor` object, and `A6` indicates the pin number this sensor is connected to. If desired, you could use a different variable name.
* `rightLine` represents a variable name for a `RedBotSensor` object, and `A7` indicates the pin number this sensor is connected to. If desired, you could use a different variable name.

## Check IR Sensor Measurements

To check the measurements from the IR line following sensors, use the `RedBotSensor` object's `read()` method to get a measurement from each sensor:

* `leftLine.read()`
* `centerLine.read()`
* `rightLine.read()`

The `read()` method will return an analog value between 0-1023 that represents a measurement of how much reflected IR light was detected:

* **Lower values** actually indicate **more** IR light was reflected back. This indicates a lighter-colored surface.
* **Higher values** actually indicate **less** IR light was reflected back. This indicates a darker-colored surface.
* **Very high values** may indicate the sensors are hanging over a "cliff" — i.e., the surface is too far away \(so very little IR light is reflected back\).

Since you will typically want to compare the readings from all 3 sensors at the same time, your program should store the sensor readings in local variables, and then use the readings to perform an action:

```cpp
// get IR sensor readings
int leftSensor = leftLine.read();
int centerSensor = centerLine.read();
int rightSensor = rightLine.read();

// add code to do something based on sensor readings
```

You will need to add code to do something with the sensor readings. For example, you might use `if` statements to perform certain actions if one or more sensor readings are greater than \(or less than\) a specific value.

**NOTE:** If you used different variable names for your `RedBotSensor` objects, then change `leftLine`, `centerLine`, and `rightLine` to match the names of your variables. For example, if you used `rSensor` as your object variable name for the right sensor, your code should use `rSensor.read()` to get that sensor's measurement.

You can either insert this code into your `loop()` function or into a custom function that is called by your `loop()` function.

## Use Serial Monitor to View IR Sensor Measurements

To test out your IR sensors, you can view the sensor measurements using the serial monitor in the Arduino code editor.

### 1. Start Serial Connection

Add this code into your `setup()` function to start a serial connection between your RedBot and the code editor:

```cpp
// start serial connection to view sensor data
Serial.begin(9600);
```

### 2. Send Data Over Serial Connection

Add this custom function named `testLineSensors()` after your `loop()` function. This custom function will send \(print\) the sensor measurements over the serial connection:

### testLineSensors\(\) function

```cpp
void testLineSensors() {
    // get IR sensor readings
    int leftSensor = leftLine.read();
    int centerSensor = centerLine.read();
    int rightSensor = rightLine.read();

    // send data to serial monitor
    Serial.print("L: ");
    Serial.print(leftSensor);
    Serial.print("\tC: ");
    Serial.print(centerSensor);
    Serial.print("\tR:");
    Serial.println(rightSensor);

    // small delay before next test reading
    delay(100);
}
```

Then be sure to call this custom function in your `loop()` function:

```cpp
void loop() {
    testLineSensors();
}
```

**NOTE:** Be sure that your program also contains the necessary code to create the `RedBotSensor` objects named `leftLine`, `centerLine`, and `rightLine`.

### 3. View Data in Serial Monitor

After uploading the program to the RedBot, **keep the RedBot connected to your computer using the USB cable** \(because the serial data is transferred over USB\).

Open the Serial Monitor window in your Arduino code editor:

* **Arduino Create Web Editor**: Click the "Monitor" menu in the left navigation panel.
* **Arduino IDE Desktop Editor:** Under the "Tools" menu, select "Serial Monitor".

It may take a few seconds for the serial connection to be detected by the editor. Then you should see the sensor measurements being displayed in the serial monitor window.

Try the following tests to see how the sensor measurements change:

* Place the RedBot on a light-colored surface \(e.g., place a white sheet of paper on a table\) to see what the measurements are. Then place the RedBot on a dark-colored surface to see how the measurements change. Try different colors to compare the measurements.
* Use a marker to draw a thick dark line on a white sheet of paper. Then manually roll the RedBot over the line to see how the sensor measurements change. See if you can position the RedBot so that only one sensor detects the line. Then see if you can adjust the position so a different sensor detects the line. Make the line wider to see how this affects the measurements.
* Use opaque tape \(masking tape, painting tape, electrical tape, etc.\) to make a "line" on a surface \(such as a table or floor\). Ideally, the colors of the tape and the surface should contrast: either use light-colored tape on a dark-colored surface, or use dark-colored tape on a light-colored surface. Then manually roll the RedBot over the line to see how the sensor measurements change.
* Try slowly lifting the front edge of the RedBot off the table to see how the sensor measurements change with distance.
* Manually roll the RedBot towards the edge of a table to see how the measurements change when the sensors are hanging over the edge.

## Avoid Driving Over Drop-Off

Even a small increase in the distance between the IR sensors and the surface \(as little as 0.25 inch\) will greatly reduce the amount of reflected IR light that is detected.

You can use this fact to prevent the RedBot from driving over a "cliff" by stopping the motors if the measurements from the IR sensors are too high, which might indicate the sensors at the front of the RedBot are hanging over a table edge, stair step, or other drop-off.

### checkDropOff\(\) function

Here is a custom function named `checkDropOff()` that will check the IR sensor readings and then perform a set of actions \(brake, etc.\) if it detects the RedBot is about to drive over a "cliff" such as a table edge or other drop-off:

```cpp
void checkDropOff() {

    // set IR threshold indicating drop-off (table edge, etc.)
    int dropOff = 900; // change value if necessary

    // get IR sensor readings
    int leftSensor = leftLine.read();
    int centerSensor = centerLine.read();
    int rightSensor = rightLine.read();

    // see if any IR sensors detect drop-off
    if (leftSensor > dropOff || centerSensor > dropOff || rightSensor > dropOff) {
        // add code to perform (brake, reverse, change direction, etc.)
        motors.brake();

    }
}
```

You can call this custom function in your `loop()` function \(or within another custom function\).

The custom function has a local variable named `dropOff` set to a value of `900`. Any IR sensor reading greater than this is treated as indicating a "cliff" drop-off.

You should do a test with your RedBot to verify if this value \(`900`\) is accurate. Use the serial monitor to view the IR sensor data as you roll the front of your RedBot towards a drop-off \(such as a table edge\). If necessary, change the value of `dropOff` from `900` to whichever value is more accurate to indicate a drop-off has been detected.

You will also need to decide what code to perform if the IR sensors detect a drop-off. Most likely, the first thing that you should do is make the RedBot motors brake.

You could also make the RedBot produce a sound as feedback. This would be useful for testing your code by moving the RedBot's front edge over a drop-off \(such as a table edge\) to verify the sound is produced when the IR sensors detect the drop-off. What type of sound \(frequency, duration, number of beeps, etc.\) would make the most sense for an "warning" event like approaching a drop-off?

Finally, you will most likely need to make the RedBot change direction to avoid driving off the "cliff" that it detected. For example, make the RedBot back away from the drop-off by driving backwards for a short distance. Then make the RedBot turn away from the drop-off before proceeding forward again.

## Follow Line Automatically

The IR sensors can be used to make the RedBot follow a line on the surface:

* If the RedBot is **aligned with the line**, the line will be under the **center** IR sensor. The RedBot should **drive straight** to stay on the line.
* If the RedBot has started to **move off the line towards the right**, the line will under the **left** IR sensor. The RedBot should **curve slightly to the left** to get back on the line.
* If the RedBot has started to **move off the line towards the left**, the line will under the **right** IR sensor. The RedBot should **curve slightly to the right** to get back on the line.

**NOTE:** Line following works best with a very dark line on a very light surface \(or vice versa\). The line also needs to be the right width: not too wide, but not too narrow. A line between 0.25—0.75 inch is ideal. Electrical tape \(traditionally black, but also available in colors like white\) works well — it can be easily applied \(and removed\) on a variety of surfaces.

In order to make the RedBot curve to the left or to the right, you can use different motor powers for the left and right motors. We'll use variables to keep track of each motor's power. Add these global variables before your `setup()` function:

```cpp
int leftPower, rightPower;
```

### followLine\(\) function

This custom function will use the IR sensors to adjust the `leftPower` and `rightPower` as needed to try to make the RedBot follow a line:

```cpp
void followLine() {

    /* FOLLOW LINE
    To follow dark line on light surface:
    Use high threshold & see if sensors greater than threshold

    To follow light line on dark surface:
    Use low threshold & see if sensors less than threshold

    Take test readings of line to determine best value for threshold
    */

    // change values if necessary
    int lineThreshold = 800;
    int power = 100;
    int powerShift = 50;

    // get IR sensor readings
    int leftSensor = leftLine.read();
    int centerSensor = centerLine.read();
    int rightSensor = rightLine.read();

    // when line under center sensor, drive straight to stay aligned
    if (centerSensor > lineThreshold) {
        // set both motors to same power
        leftPower = power;
        rightPower = power;
    }
    // when line under left sensor, curve slightly left to realign
    else if (leftSensor > lineThreshold) {
        // decrease left motor, increase right motor
        leftPower = power - powerShift;
        rightPower = power + powerShift;
    } 
    // when line under right sensor, curve slightly right to realign
    else if (rightSensor > lineThreshold) {
        // increase left motor, decrease right motor
        leftPower = power + powerShift;
        rightPower = power - powerShift;
    }

    // drive motors using power values from above
    motors.leftDrive(leftPower);
    motors.rightDrive(rightPower);

    delay(25);  // change delay to adjust line following sensitivity    
}
```

You can call this custom function in your `loop()` function \(or within another custom function\).

Once the program is uploaded to your RedBot, just place the RedBot on the line to see if it follows the line automatically.

Sometimes it can be challenging to get your RedBot to follow a line consistently. Here are some troubleshooting tips:

* You may need to change the value for `power`. A lower power \(such as `100`\) generally works better for line following. However, you may need to try different powers to find the value that works best.
* You may need to change the value for `lineThreshold` based on your line and surface. Test your line using the IR sensors \(view the data in the serial monitor\).
* You may need to change the value for `powerShift`, which is used to realign the RedBot by shifting the value of the left and right motor powers.
* You may need to change the `delay()` value at the end of the function to adjust the sensitivity \(i.e., how long is the RedBot allowed to drive before the IR sensors are checked again\).
* You may need to try different types of lines and surfaces to find the right combination that works effectively. You need high contrast between the line and the surface:  either a dark line on a light surface \(or the opposite\). The line should be between 0.25—0.75 inch in width.
* You may need to try different angles or paths to see what works best. Lines that have sharp angles or turns \(e.g., 90° turns\) may be difficult to follow closely.

If you have an ultrasonic sensor connected to your RedBot, you can also [avoid obstacles while following a line](ultrasonic-sensor.md#avoid-collisions-while-following-line).

## Avoid Line Automatically

You can also use the IR sensors to avoid a line. The line can act as a border to keep the RedBot out of an area surrounded by a line — or to keep the RedBot within an area enclosed by a line:

* If the line is detected under the left IR sensor, the RedBot should stop and turn right to avoid the line.
* If the line is detected under the right IR sensor, the RedBot should stop and turn left to avoid the line.
* If the line is detected under both \(or all\) IR sensors, the RedBot should stop and turn around to avoid the line.

### avoidLine\(\) function

This custom function will use the IR sensors to stop and turn the RedBot if it detects a line:

```cpp
void avoidLine() {

    /* AVOID LINE
    To avoid dark line on light surface:
    Use high threshold & see if sensors greater than threshold

    To avoid light line on dark surface:
    Use low threshold & see if sensors less than threshold

    Use test readings from line to determine best value for threshold
    */

    // adjust value if necessary
    int lineThreshold = 800;

    // get IR sensor readings
    int leftSensor = leftLine.read();
    int rightSensor = rightLine.read();

    // when either sensor on line, first brake motors
    if (leftSensor > lineThreshold || rightSensor > lineThreshold) {
        motors.brake();
        delay(250);
    }

    // when both sensors on line, turn around
    if (leftSensor > lineThreshold && rightSensor > lineThreshold) {
        long rnd = random(750, 1250);
        motors.pivot(100);
        delay(rnd);
        motors.stop();
    }
    // when line under left sensor only, pivot right
    else if (leftSensor > lineThreshold) {
        long rnd = random(500, 750);
        motors.pivot(100);
        delay(rnd);
        motors.stop();
    }
    // when line under right sensor only, pivot left
    else if (rightSensor > lineThreshold) {
        long rnd = random(500, 750);
        motors.pivot(-100);
        delay(rnd);
        motors.stop();
    }
    // otherwise, keep driving straight
    else {
        motors.drive(100);
    }

    delay(25);  // change delay to adjust line detection sensitivity
}
```

Although the concept of avoiding a line is similar to following a line, you can see that the custom function works differently:

* To follow a line, the left and right motor powers are adjusted to gently turn the RedBot so it will be centered on the line.
* However, to avoid a line, the RedBot is stopped using the brakes and then pivoted away from the line, before it is allowed to drive forward again.

When the IR sensors detect a line, the Arduino `random()` method is used to [generate a random number](https://www.arduino.cc/reference/en/language/functions/random-numbers/random/) that will become the delay time while the RedBot pivots. At a pivot power of 100, a delay between 500 ms to 750 ms will allow the RedBot to pivot about 90° to 135°, while a random delay between 750 ms to 1250 ms will allow the RedBot to pivot about 135° to 225°. If desired, you can change the range for the random numbers — but the RedBot should always pivot for at least 500 ms \(90°\) to ensure it will point away from the line.

## Count Lines and Stop at Target Number

You can also use the IR sensors to count the number of lines that the RedBot crosses as it drives. You can make the RedBot automatically stop once it reaches a specific line number \(such as the 1st line, 2nd line, 3rd line, 4th line, etc.\).

In this case, you use short lines as "markers" to indicate possible stopping points along a path. The lines should be placed **perpendicular** to the RedBot's path. The lines do not have to be spaced out evenly — just place the lines wherever you need a possible stopping \(or turning\) point. Once the RedBot reaches the desired line number, it will stop. Then you can perform other desired actions, such as turning, etc.

![](../../.gitbook/assets/line-counting.png)

### countLine\(\) function

This custom function will use the IR sensors to count lines and then stop at a specific line number:

```cpp
void countLine(int target) {

    /* COUNT LINES
    To count dark lines on light surface:
    Use high threshold & see if sensors greater than threshold

    To count light lines on dark surface:
    Use low threshold & see if sensors less than threshold

    Use test readings from line to determine best value for threshold
    */

    int lineThreshold = 800;  // adjust value as necessary

    // variables for IR sensor readings and line counting
    int leftSensor, centerSensor, rightSensor;
    int lineCount = 0;
    boolean lineDetected = false;

    // keeps looping while line count is less than target
    while (lineCount < target) {

        driveStraight();

        // get IR sensor readings
        leftSensor = leftLine.read();
        centerSensor = centerLine.read();
        rightSensor = rightLine.read();

        // toggle between checking for line vs. checking for no line
        if (lineDetected == false) {
            // when all 3 sensors detect line, increase line count and toggle to checking for no line
            if (leftSensor > lineThreshold && centerSensor > lineThreshold && rightSensor > lineThreshold) {
                lineCount++;
                lineDetected = true;
            }
        }
        else if (lineDetected) {
            // when all 3 sensors detect no line, toggle back to checking for line
            if (leftSensor < lineThreshold && centerSensor < lineThreshold && rightSensor < lineThreshold) {
                lineDetected = false;
            }
        }
    }
    // line count target reached
    motors.brake();
    delay(250);
    driveDistance(3.5, 100); // drive forward to be centered on target line
}
```

You can call this custom function in your `loop()` function \(or within another custom function\).

When calling this function, you will need to pass in a number representing the target line number where the RedBot should stop. For example, to make the RedBot drive straight until it reaches the 3rd line:

```cpp
countLine(3);
```

The custom function uses a `while` loop to keep driving straight and counting lines as long as the total number of detected lines is less than the target number of lines. Once the line count reaches the target number, the `while` loop ends and the motors are stopped. Then the RedBot drives forward a short distance \(3.5 inches\) in order to center itself on the stopped line.

You will notice that within this `while` loop, the value of a variable named `lineDetected` is toggled back and forth between `true` and `false`. The reason for this is to ensure accurate line counting, so the code doesn't accidentally count the same line more than once:

* Once a line has been detected, the code will increase the line count and immediately start checking for no line \(i.e., giving the RedBot time to drive past the current line\).
* Once it detects that the RedBot has completely crossed the current line \(i.e., once **no** line is detected\), the code will start checking again for a new line.

**IMPORTANT:** This `countLine()` function uses two other custom functions: `driveStraight()` and `driveDistance()`. Be sure to [follow the instructions in the Wheel Encoder section](https://cxd.gitbooks.io/robotics-project/content/redbot-code-references/wheel-encoders.html) to include the necessary code for the `driveStraight()` and `driveDistance()` functions.

### Grid-Like Line Marker Patterns

If necessary, you can also place line markers in a "grid-like" pattern, in order to allow your RedBot to travel between different locations. For example, this diagram shows a series of line markers with a starting location plus a set of locations labeled with letters A-I:

![](../../.gitbook/assets/line-counting-grid.png)

Imagine this diagram represents a top-down view of a grocery store layout with three aisles of food \(i.e., the three vertical columns of markers\). The top horizontal row \(i.e., with the "plus" markers\) is used to travel from one aisle to another. How could the RedBot travel from the starting location to location E?

```cpp
// travel from Start to location E
countLine(3); // start line + line A + line B
pivotAngle(90); // turn 90 degrees clockwise
// note: after turning, IR sensors no longer on line B
countLine(1); // next line will be location E
```

Note that after making a turn \(i.e., rotating\), the IR sensors at the front of the RedBot will no longer be directly on the line that the RedBot stopped at. \(Try this out with your RedBot to visually understand why this is true.\)

How could the RedBot then travel from location E to location G?

```cpp
// travel from location E to location G
pivotAngle(180); // turn around 180 degrees to face towards B
countLine(1); // next line will be line B
pivotAngle(-90); // turn 90 degrees counter-clockwise
countLine(1); // next line will be line A
pivotAngle(-90); // turn 90 degrees counter-clockwise
countLine(2); // line D + line G
```

So how could the RedBot get from location G back to the Start?

The line markers make it easy to create flexible pathways for your RedBot to travel to and from different locations. Of course, your team would design your line marker pattern to best fit the specific needs of your robot's testing scenarios.

**NOTE:** Another way to create flexible pathways for your RedBot is to program it to drive specific distances \(instead of counting a specific number of lines\). What might be the advantages \(or disadvantages\) of counting numbers of lines versus driving specific distances?

## Follow Line While Counting Lines Crossed

You can also use the IR sensors to make your RedBot follow a line while also counting the number of lines that the RedBot crosses as it drives. You can make the RedBot automatically stop once it reaches a specific line number \(such as the 1st line, 2nd line, 3rd line, 4th line, etc.\).

This will allow you to create a more complex line pattern that has different paths for the RedBot to follow. The key is to make sure the lines cross each other at **perpendicular** angles \(90° right angles\).

![](../../.gitbook/assets/follow-count-lines-ex1.png)

### followCountLine\(\) function

This custom function will use the IR sensors to follow a line while counting other lines crossed and then stop at a specific line number:

```cpp
void followCountLine(int target) {

    /* NOTES
    Follow line while counting lines that are crossed while driving
    Will stop once target line count has been reached

    To follow and count dark lines on light surface:
    Use high threshold & see if sensors greater than threshold

    To follow and count light lines on dark surface:
    Use low threshold & see if sensors less than threshold

    Use test readings from line to determine best value for threshold
    */

    int lineThreshold = 800;  // adjust value as necessary

    // variables for IR sensor readings and line counting
    int leftSensor, centerSensor, rightSensor;
    int lineCount = 0;
    boolean lineDetected = false;

    // while line count is less than target, follow current line and count lines crossed
    while (lineCount < target) {

        followLine();

        // get IR sensor readings
        leftSensor = leftLine.read();
        centerSensor = centerLine.read();
        rightSensor = rightLine.read();

        // toggle between checking for line versus checking for no line
        if (lineDetected == false) {
            // when all 3 sensors detect line, increase line count and toggle to checking for no line
            if (leftSensor > lineThreshold && centerSensor > lineThreshold && rightSensor > lineThreshold) {
                lineCount++;
                lineDetected = true;
            }
        }
        else if (lineDetected) {
            // when all 3 sensors detect no line, toggle back to checking for line
            if (leftSensor < lineThreshold && centerSensor < lineThreshold && rightSensor < lineThreshold) {
                lineDetected = false;
            }
        }
    }
    // line count goal reached
    motors.brake();
    delay(250);
    driveDistance(3.5, 100); // drive forward to be centered on target line
}
```

You can call this custom function in your `loop()` function \(or within another custom function\).

When calling this function, you will need to pass in a number representing the target line number where the RedBot should stop. For example, to make the RedBot follow its current line until it reaches the 3rd cross line:

```cpp
followCountLine(3);
```

The custom function uses a `while` loop to keep following the current line and counting lines it crosses as long as the total number of detected lines is less than the target number of lines. Once the line count reaches the target number, the `while` loop ends and the motors are stopped. Then the RedBot drives forward a short distance \(3.5 inches\) in order to center itself on the stopped line.

You will notice that within this `while` loop, the value of a variable named `lineDetected` is toggled back and forth between `true` and `false`. The reason for this is to ensure accurate line counting, so the code doesn't accidentally count the same line more than once:

* Once a line has been detected, the code will increase the line count and immediately start checking for no line \(i.e., giving the RedBot time to drive past the current line\).
* Once it detects that the RedBot has completely crossed the current line \(i.e., once **no** line is detected\), the code will start checking again for a new line.

**IMPORTANT:** This `followCountLine()` function uses two other custom functions: `followLine()` and `driveDistance()`. Be sure to include the necessary code \(listed in a previous section above\) for the `followLine()` function. Be sure to [follow the instructions in the Wheel Encoder section](https://cxd.gitbooks.io/robotics-project/content/redbot-code-references/wheel-encoders.html) to include the necessary code for the `driveDistance()` function.

### Complex Line Patterns

You can create more complex line patterns that have multiple paths intersecting each other. You can even have a path form a loop and cross itself. You can also add short lines as "markers" for specific destinations along a path. Again, the key is to make sure the lines always cross each other at **perpendicular** angles \(90° right angles\).

![](../../.gitbook/assets/follow-count-lines-ex2.png)

Based on the diagram above, how could the RedBot travel from the starting location to Destination 2, pause at Destination 2 \(perhaps for a simulated step\), and then head back to the Start?

There are actually multiple ways to accomplish this. Here's one possible way:

```cpp
// possible way to travel from Start to Destination 2
followCountLine(1); // stop at 1st line (Side Path 1)
pivotAngle(-90); // turn 90 degrees counter-clockwise
followCountLine(2); // 2nd line will be Destination 2

// pause at Destination 2 for simulated step
doubleBeep(); // make sound
delay(3000); // wait 3 seconds

// travel back to Start
followCountLine(1); // next line will be Main Path
pivotAngle(90); // turn 90 degrees clockwise
followCountLine(3); // 3rd line will be Start
pivotAngle(180); // turn around to be ready for next task
```

How could the RedBot travel from the starting location, loop around Destination 3, and then head back to the Start?

Here's a possible way:

```cpp
// possible way to travel from Start to Destination 3 loop
followCountLine(2); // stop at 2nd line (Side Path 2)
pivotAngle(90); // turn 90 degrees clockwise
followCountLine(1); // top of loop
pivotAngle(90);
followCountLine(1); // travel once around loop

// turn and travel back to Start
pivotAngle(90); // turn 90 degrees counter-clockwise
followCountLine(1); // next line will be Main Path
pivotAngle(-90);
followCountLine(2); // 2nd line will be Start
pivotAngle(180); // turn around to be ready for next task
```

## Detect Flat Objects on Surface

Another way to use the IR sensors is to detect different types of flat paper objects on the surface. This would be useful for a demonstration of a robot that is intended to detect specific types of objects on the ground.

Some examples might include:

* A road-repair robot that detects potholes.
* A hazardous materials robot that detects chemical spills.
* A military robot that detects buried landmines or other explosives.
* A disaster rescue robot that detects people that are unconscious or trapped.
* etc.

For the purposes of the demo, the robot will use the IR sensor to detect the "objects", even though a real-life version of the robot might use a different sensor \(such as a camera, chemical sensor, etc.\).

In order to work, the IR sensor needs to be able to detect the difference between the objects, the surface, and any lines on the surface. Therefore each type of object must have an range of IR sensor values that does not overlap with the value range for another type of object, the surface, or lines.

As a reminder, there are two main factors that affect the IR sensor readings:

* The **color or shade** of the surface \(or a flat object on the surface\) affects the IR reading value.  Light colors reflect more IR light \(sensor reading will be a lower number\), while dark colors reflect less IR light \(sensor reading will be a higher number\).
* The **distance** between the IR sensor and the surface \(or a flat object on the surface\). If the surface or object is closer to the sensor, more IR light will be reflected \(sensor reading will be a lower number\).

### Color of Paper Object

If your robot demonstration will be using the IR sensors to detect lines \(i.e., follow lines, count lines, or avoid lines\), then you need to have either black lines on a light-colored surface or white lines on a dark-colored surface. The goal is to have as much contrast between the lines and surface as possible, so the IR sensors can reliably detect the difference between them.

Assuming that your lines and surface are, respectively, close to black and white in color, then you need to find colors or shades in between that are distinct to the IR sensor, so you can use them for your paper objects.

You can test out different colors \(red, green, blue, yellow, etc.\), but you might be surprised to find out that many of these colors actually have similar IR sensor readings, even though the colors are visually distinct to our eyes. \(Our eyes see visible light, whereas the IR sensor detects infrared light.\)

You will actually have more luck testing out different shades of gray. Black is the equivalent of 100% gray, while white is the equivalent of 0% gray. In between, different grayscale colors will register as different IR values. You can [download and print this PDF of grayscale colors](https://drive.google.com/open?id=18TWQMY_RerLaqExrfIoakATcg6mZ8eVH) to test them using your RedBot's IR sensors. Use the serial monitor and the `testLineSensors()` custom function \(one of the previous sections on this page\) to conduct the tests.

**Here are suggested IR sensor value ranges that you could use in your robot demo program:**

* **IR values greater than 950 will typically indicate 100% gray \(i.e., black\)**, which might represent lines on your surface \(e.g., lines made with black electrical tape\).
* **IR values less than 400 will typically indicate 0% gray \(i.e., white\)**, which might represent your surface \(e.g., large sheets of white paper\).
* **IR values between 750-850 will typically indicate 60% gray \(hex color \#666666\)**, which could represent one type of surface object.
* **IR values between 500-650 will typically indicate 10% gray \(hex color \#E6E6E6\)**, which could represent a second type of surface object \(if you need a second type for your demo\).

You could print out shapes with the appropriate grayscale color, cut them out, and then place them on the surface of your robot's testing environment.

### Distance to IR Sensor \(Thickness of Paper Object\)

Normally, the distance between the IR sensors and the surface is fixed because the IR sensors on the RedBot are attached about 3/16 of an inch above the surface.

However, if you make a paper object on the surface thicker by constructing it out of multiple sheets of paper, you can lower its IR sensor reading because the "object" is now closer to the IR sensor. Even a few sheets of paper can be enough increase in thickness to significantly change the value.

You can test this out with your RedBot with different thicknesses of paper \(1 sheet, 2 sheets, 3 sheets, etc.\). For the purposes of your robot demonstration, you will probably want the top sheet of paper to have a particular color, so it will be visually distinct to your audience.

### Custom Function to Detect Objects on Surface

Once you have identified the appropriate colors and/or thicknesses of paper objects for your robot demonstration, you can used a custom function named `detectSurfaceObjects()` to detect one or more types of objects.

This function can perform one of two possible behaviors when a particular object type is detected:

* A `while()` loop can be used to make the RedBot stop when it detects a particular object type. The RedBot will stop, make an alert sound, and then wait until you physically remove the paper object from the surface \(which can represent a _simulated_ step in your robot demo, such as the robot cleaning up a chemical spill, etc.\). Once the paper object has been removed, the RedBot will continue on to the next code instruction in your program \(such as start driving again, etc.\).
* An `if` statement can be used to make the RedBot pause when it detects a particular object type. The RedBot will stop, make an alert sound, pause briefly, and then continue on to the next code instruction in your program \(such as start driving again, etc.\).

### detectSurfaceObjects\(\) function

```cpp
void detectSurfaceObjects() {
    /*
    Checks for different types of flat paper objects on surface
    Different types of objects must vary in color and/or paper thickness
    IR sensor ranges for objects, surface, and lines should not overlap

    while() loop can be used to make robot stop until object removed
    if() statement can be used to make robot pause briefly
    */

    // adjust min and max values based on IR sensor tests
    int object1_min = 750;
    int object1_max = 850;

    int object2_min = 500;
    int object2_max = 650;

    // get IR sensor reading
    int centerSensor = centerLine.read();

    // while object type 1 detected - stop and wait until object removed
    while (centerSensor > object1_min && centerSensor < object1_max) {
        motors.stop();
        object1Sound();
        delay(250); // brief wait before checking sensor again
        centerSensor = centerLine.read(); // get new sensor reading
    }

    // if object type 2 detected - pause briefly and move on
    if (centerSensor > object2_min && centerSensor < object2_max) {
        motors.stop();
        object2Sound();
        delay(2000); // pause for 2 seconds
    }
}
```

You can call this custom function in your `loop()` function \(or within another custom function\).

If desired, you can place multiple copies of an object type on the surface \(as long as each copy has the same color and thickness\).

**IMPORTANT:** You may need to modify some of the code within this custom function:

* You will need to test the IR sensor values for your particular objects, and if necessary, adjust the minimum and maximum values listed in the function. Use the serial monitor and the `testLineSensors()` function to test and view the values.
* If you only need to detect one type of object, you can remove the code for `object2`.
* If you need to detect more than two types of objects, you can add code for `object3`, etc. Just be sure each object type has a distinct range of values that can be detected by the IR sensor.
* For each object type, you can use either a `while()` loop \(to stop and wait until the object is removed\) or an `if` statement \(to pause briefly while leaving the object in place\). Modify the function to use whichever option you want for each object type.
* It is recommended that you create a unique alert sound for each object type. These are the custom functions referred to as `object1Sound()` and `object2Sound()` in the code shown above. You will need to create these yourself. 

