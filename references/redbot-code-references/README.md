# RedBot Code References

{% hint style="danger" %}
**UPDATE IN PROGRESS:** All the robotics coding references are being updated and moved into a [new coding guidebook](https://docs.idew.org/code-robotics/) \(separate from this project guidebook\). This will occur during fall 2018 and be ready for use in January 2019. Please check back later.
{% endhint %}

The following coding references can help you create Arduino programs that use your RedBot's motors, sensors, and other parts:

* [Arduino Programming](arduino-programming.md)
* [RedBot Library](redbot-library.md)
* [LED Light](led-light.md)
* [Buzzer \(Speaker\)](buzzer-speaker.md)
* [Push Button](push-button.md)
* [Motors](motors.md)
* [Mechanical Bumpers](mechanical-bumpers.md)
* [IR Line Sensors](ir-line-sensors.md)
* [Wheel Encoders](wheel-encoders.md)
* [Accelerometer](accelerometer.md)
* [Ultrasonic Sensor](ultrasonic-sensor.md)
* [Demo Program Examples](https://github.com/cxd/robotics-project/tree/fbb39c73504934f9ec46bf26d114575f1e749e00/redbot-code-references/demo-program-examples.md)

### Quick Links to RedBot Custom Functions

Here are direct links to certain custom functions in the coding references that can help you program your robot's tasks and behaviors. Be sure to review the the rest of the sensor's coding reference for additional code that may be necessary for the sensor and the function to work properly.

**TIP:** If any of the links below don't take you directly to the desired custom function on the destination page, just reload the destination page.

#### Driving

These custom functions use the [wheel encoders](wheel-encoders.md):

* [`driveStraight()`](wheel-encoders.md#drive-straight-continuously) — drive straight continuously
* [`driveDistance()`](wheel-encoders.md#drive-straight-for-specific-distance) — drive straight for specific distance at specific motor power

#### Turning

These custom functions also use the [wheel encoders](wheel-encoders.md):

* [`pivotAngle()`](wheel-encoders.md#pivot-both-wheels-by-specific-angle) — pivot on both wheels by specific angle
* [`turnAngle()`](wheel-encoders.md#turn-on-one-wheel-by-specific-angle) — turn on one wheel by specific angle

#### Detecting Lines

These custom functions use the [IR line sensors](ir-line-sensors.md):

* [`followLine()`](ir-line-sensors.md#follow-line-automatically) — follow a line automatically
* [`avoidLine()`](ir-line-sensors.md#avoid-line-automatically) — avoid a line automatically \(acts like border to contain robot\)
* [`countLine()`](ir-line-sensors.md#count-lines-and-stop-at-target-number) — drive straight while counting lines crossed and stop at specific line number
* [`followCountLine()`](ir-line-sensors.md#follow-line-while-counting-lines-crossed) — follow a line while counting lines crossed and stop at specific line number

#### Detecting Objects

These custom functions use the [mechanical bumpers](mechanical-bumpers.md), [ultrasonic sensor](ultrasonic-sensor.md), or [IR line sensors](ir-line-sensors.md):

* [`checkBumpers()`](mechanical-bumpers.md#check-bumpers-for-collisions) — check for bumper collision with object
* [`measureDistance()`](ultrasonic-sensor.md#measure-distance-to-object) — measure distance ahead to nearest object
* [`avoidCollision()`](ultrasonic-sensor.md#avoid-collisions) — avoid colliding with object if it is too close \(also works [while following a line](ultrasonic-sensor.md#avoid-collisions-while-following-line)\)
* [`findClosestObject()`](ultrasonic-sensor.md#find-closest-object) — performs 360° scan to find the closest object and then drive towards it
* [`detectSurfaceObjects()`](ir-line-sensors.md#detect-flat-objects-on-surface) — detects different types of flat paper objects on the surface

## External Links

These external links will also help you with programming your Redbot:

* [Arduino Create Web Editor](https://create.arduino.cc/editor/)
* [Arduino Programming Language Reference](https://www.arduino.cc/reference/en/)
* [SparkFun Experiment Guide for RedBot](https://learn.sparkfun.com/tutorials/experiment-guide-for-redbot-with-shadow-chassis/)
* [SparkFun RedBot Library Quick Reference](https://learn.sparkfun.com/tutorials/experiment-guide-for-redbot-with-shadow-chassis/redbot-library-quick-reference)

