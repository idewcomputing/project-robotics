# Motors

The SparkFun `RedBot` library has a class named `RedBotMotors` which contains methods \(functions\) to control the RedBot's left and right motors \(either as a pair or as independent left and right motors\).

### How to Use the Motors in a Program:

To use the motors, you will need to: 1. Create `RedBotMotors` object for the motors 2. Use the object's methods such as: `drive()`, `pivot()`, `brake()`, etc.

### Coding References in this Section:

* Create RedBotMotors Object
* Drive Forwards \(or Backwards\)
* Coast to Stop
* Brake \(Abrupt Stop\)
* Turn Left or Right
  * Pivot on Both Wheels
  * Turn on One Wheel
  * Gentle Turn
* Drive \(or Turn\) for Specific Amount of Time
* Drive for Specific Distance \(Using Average Driving Speed\)
* Pivot by Specific Angle \(Using Average Turning Speed\)

## Create RedBotMotors Object

In order to use the methods that control the motors, you must first create a `RedBotMotors` object.

**IMPORTANT:** Be sure that your program includes a copy of the SparkFun `RedBot` library. If necessary, see the instructions for [how to include the RedBot library](redbot-library.md).

Before your `setup()` function, create a `RedBotMotors` object by assigning it to a variable name:

```cpp
RedBotMotors motors;
```

* `RedBotMotors` indicates the class of object being created \(this class is part of the `RedBot` library\)
* `motors` represents the variable name of the `RedBotMotors` object. If desired, you could use a different variable name.

**NOTE:** All the code examples for the `RedBotMotors` methods will use `motors` as the name of this object variable. If necessary, just substitute your variable name wherever you see `motors` listed in the code examples.

## Drive Forwards \(or Backwards\)

The `drive()` method rotates **both** motors to move the RedBot either forwards or backwards:

* When moving the RedBot forward, the right motor rotates clockwise \(CW\), while the left motor rotates counter-clockwise \(CCW\).
* When moving the RedBot backwards, the right motor rotates counter-clockwise \(CCW\), while the left motor rotates clockwise \(CW\).

Even though this might seem like the wheels would be moving in opposite directions, it actually makes the wheels move in the **same** direction because the wheels are oriented as mirror images of each other.

### Drive Both Motors

Use the `drive()` method to drive both motors at the same time:

```cpp
motors.drive(power);
```

* `power` represents the power applied to the motors, which can be any integer value between `-255` and `255`.
  * Positive values move the RedBot forwards.
  * Negative values move the RedBot backwards.
  * A larger absolute value results in a faster speed. \(`-255` and `255` are the fastest speeds. `-1` and `1` are the slowest speeds.\)

**IMPORTANT:** Running the motors at high power can sometimes cause the wheels to spin-out \(due to insufficient traction with the surface\). If you notice traction issues between the wheels and the surface, use a lower power \(slower speed\). In general, use a power of about 200 or less, depending on the surface.

You can also drive the left and right motors independently by using different powers for each motor \(or even stopping one motor while the other keeps driving\). In certain situations, this may be useful. For example, this can be used to make the RedBot curve or turn.

### Drive Left Motor

Use the `leftMotor()` method to drive just the left motor:

```cpp
motors.leftMotor(power);
```

* `power` represents the power applied to the left motor, which can be any integer value between `-255` and `255`.
  * Positive values rotate the left motor clockwise \(backwards\).
  * Negative values rotate the left motor counter-clockwise \(forwards\).
  * A larger absolute value results in a faster speed. \(`-255` and `255` are the fastest speeds. `-1` and `1` are the slowest speeds.\)

Alternatively, you can use the `leftDrive()` method, which does the exact **same** thing — except positive values are used to drive forwards \(and negative values are used to drive backwards\):

```cpp
motors.leftDrive(power);
```

* `power` represents the power applied to the left motor, which can be any integer value between `-255` and `255`.
  * Positive values rotate the left motor forwards \(counter-clockwise\).
  * Negative values rotate the left motor backwards \(clockwise\).
  * A larger absolute value results in a faster speed. \(`-255` and `255` are the fastest speeds. `-1` and `1` are the slowest speeds.\)

For example, if the left motor rotates counter-clockwise \(forwards\) while the right motor is stopped, the RedBot will turn clockwise \(to the right\).

### Drive Right Motor

Use the `rightMotor()` method to drive just the right motor:

```cpp
motors.rightMotor(power);
```

* `power` represents the power applied to the right motor, which can be any integer value between `-255` and `255`.
  * Positive values rotate the right motor clockwise \(forwards\).
  * Negative values rotate the right motor counter-clockwise \(backwards\).
  * A larger absolute value results in a faster speed. \(`-255` and `255` are the fastest speeds. `-1` and `1` are the slowest speeds.\)

Alternatively, you can use the `rightDrive()` method, which does the exact **same** thing:

```cpp
motors.rightDrive(power);
```

* `power` represents the power applied to the right motor, which can be any integer value between `-255` and `255`.
  * Positive values rotate the right motor forwards \(clockwise\).
  * Negative values rotate the right motor backwards \(counter-clockwise\).
  * A larger absolute value results in a faster speed. \(`-255` and `255` are the fastest speeds. `-1` and `1` are the slowest speeds.\)

For example, if the right motor rotates clockwise \(forwards\) while the left motor is stopped, the RedBot will turn counter-clockwise \(to the left\).

**NOTE:** You can accomplish the same results using either the `drive()` method or by combining the `leftMotor()` and `rightMotor()` methods:

```cpp
motors.drive(150); // move forwards
/*  does same as:
    motors.leftMotor(-150);
    motors.rightMotor(150);
*/

motors.drive(-150); // move backwards
/*  does same as:
    motors.leftMotor(150);
    motors.rightMotor(-150);
*/
```

### If RedBot Not Driving in Straight Line

When driving both motors at the same power, you may notice that your RedBot drifts slightly to the left \(or right\), instead of driving in a perfectly straight line. If this occurs, it is because the motors are rotating at slightly different speeds, even though they are receiving the same amount of power.

If necessary, you can use the [wheel encoders](wheel-encoders.md) to help adjust the left and right motor powers while the RedBot is driving, in order to make it drive in a straight line.

## Coast to Stop

The `coast()` method turns off **both** motors and allows the RedBot to coast to a stop.

### Stop Both Motors

```cpp
motors.coast();
```

Alternatively, you can use the `stop()` method, which does the exact **same** thing:

```cpp
motors.stop();
```

You can also stop \(coast\) the left and right motors independently. In certain situations, this may be useful.

### Stop Left Motor

```cpp
motors.leftCoast();
```

Alternatively, you can use the `leftStop()` method, which does the exact **same** thing:

```cpp
motors.leftStop();
```

### Stop Right Motor

```cpp
motors.rightCoast();
```

Alternatively, you can use the `rightStop()` method, which does the exact **same** thing:

```cpp
motors.rightStop();
```

## Brake \(Abrupt Stop\)

The `brake()` method actively brakes **both** motors and causes the RedBot to abruptly stop.

### Brake Both Motors

```cpp
motors.brake();
```

You can also brake the left and right motors independently. In certain situations, this may be useful.

### Brake Left Motor

```cpp
motors.leftBrake();
```

### Brake Right Motor

```cpp
motors.rightBrake();
```

## Turn Left or Right

There are several ways to turn the RedBot left or right, depending on how tight the turn needs to be. The RedBot is capable of pivoting on both wheels, which results in a "zero turn radius" \(tightest possible turn\).

| Type of Turn | How Turn Works |
| :--- | :--- |
| Pivot on Both Wheels | Both wheels rotate in **same** direction \(both CW or both CCW\) at **same** motor power |
| Turn on One Wheel | Only one wheel rotates \(either CW or CCW\) while other wheel is **stopped** |
| Gentle Turn | Wheels rotate in **opposite** directions \(one CW and other CCW\) at **different** motor powers |

Here is a visual comparison of pivoting on both wheels versus turning on one wheel:

![](../../.gitbook/assets/pivot-both-vs-turn-one.png)

### Pivot on Both Wheels

The `pivot()` method results in a perfectly tight turn, as the RedBot's axis of rotation is centered between its wheels. As a result, the RedBot doesn't move forward while pivoting.

The `pivot()` method rotates **both** motors to pivot \(turn\) the RedBot either clockwise \(to the right\) or counter-clockwise \(to the left\):

* When pivoting the RedBot clockwise \(to the right\), both motors rotate counter-clockwise \(CCW\) at the same power.
* When pivoting the RedBot counter-clockwise \(to the left\), both motors rotate clockwise \(CW\) at the same power.

To pivot \(either clockwise or counter-clockwise\):

```cpp
motors.pivot(power);
```

* `power` represents the power applied to the motors, which can be any integer value between `-255` and `255`.
  * Positive values pivot the RedBot clockwise \(to the right\).
  * Negative values pivot the RedBot counter-clockwise \(to the left\).
  * A larger absolute value results in a faster speed. \(`-255` and `255` are the fastest speeds. `-1` and `1` are the slowest speeds.\)

**IMPORTANT:** Use a lower power when pivoting the RedBot, as compared to driving the RedBot. A power of about 100 should be sufficient to quickly pivot on most surfaces.

**NOTE:** You can accomplish the same results using either the `pivot()` method or by combining the `leftMotor()` and `rightMotor()` methods:

```cpp
motors.pivot(100); // turn CW to right
/*  same as:
    motors.leftMotor(-100);
    motors.rightMotor(-100);
*/

motors.pivot(-100); // turn CCW to left
/*  same as:
    motors.leftMotor(100);
    motors.rightMotor(100);
*/
```

### Turn on One Wheel

Alternatively, you can turn the RedBot on one wheel by driving only one motor forward while stopping the other motor.

This will help retain more of the RedBot's forward momentum \(whereas pivoting requires the RedBot to stop moving forward\). However, the turn radius will be larger compared to using the `pivot()` method because the RedBot's axis of rotation is centered on the stopped wheel.

```cpp
// turn CW to right
motors.leftDrive(100);
motors.rightStop();

// turn CCW to left
motors.leftStop();
motors.rightDrive(100);
```

### Make Gentle Turn

Furthermore, you can make gentle turns or curves by simply applying different amounts of power to the two motors:

* Applying more power to the **left motor** will cause the RedBot to curve to the **right**.
* Applying more power to the **right motor** will cause the RedBot to curve to the **left**.
* A larger difference in the motor powers will make the RedBot curve more sharply, while a smaller difference will make the RedBot curve more gently.

This will help maintain even more of the RedBot's forward momentum, compared to turning on one wheel \(which is an extreme version of using different motor powers that applies a power of zero to one wheel\).

```cpp
// curve to left
motors.leftMotor(-100);
motors.rightMotor(150);

// curve to right
motors.leftMotor(-150);
motors.rightMotor(100);

// curve to right more sharply
motors.leftMotor(-175);
motors.rightMotor(100);

// curve to right more gently
motors.leftMotor(-125);
motors.rightMotor(100);
```

## Drive \(or Turn\) for Specific Amount of Time

If you make the motors drive or turn, the RedBot will keep driving or turning until you tell it to stop.

Often, you will only want to drive or turn the RedBot for a certain amount of time, and then make it stop. This gives you control over how far it moves or turns.

This also allows you to program a step-by-step "route" for RedBot to follow: e.g., drive for a certain amount of time, then stop, then turn right, then drive for a certain amount of time, then stop again, then turn left, etc.

You can use the `delay()` function to allow the RedBot to drive or turn for a specific amount of time \(in milliseconds\), and then use the `motors.brake()` method to stop the RedBot.

For example:

```cpp
// drive straight for 3 seconds and then stop
motors.drive(200);
delay(3000);
motors.brake();

// pivot right for 0.5 seconds to change direction
motors.pivot(100);
delay(500);
motors.brake();

// drive in new direction for 2 seconds and then stop
motors.drive(200);
delay(2000);
motors.brake();
```

## Drive for Specific Distance \(Using Average Driving Speed\)

It is extremely useful to be able to control how far your RedBot drives, so it can follow a planned route or navigate through its environment.

One way to do this is to determine the average driving speed of your RedBot \(at a specific motor power\), and then use this to calculate how much time it will take to make your RedBot drive any specific distance.

**NOTE:** Alternatively, you can use the [wheel encoders](wheel-encoders.md) to make your RedBot drive a specific distance. This will typically be more accurate than using your RedBot's average driving speed.

The last activity in [RedBot Experiment 2](https://learn.sparkfun.com/tutorials/experiment-guide-for-redbot-with-shadow-chassis/experiment-2-drive-forward-) requires you to conduct a test to determine the average speed of your RedBot.

You do this by measuring how far your RedBot travels in a specific amount of time \(such as 2 seconds\) at a specific motor power \(such as 200\). Conduct multiple trials \(at least 5\) to calculate the average distance traveled by the RedBot. For each trial, be sure to use the same amount of time and the same motor power.

Then use your average distance and the amount of time to calculate the average speed of your RedBot \(at that specific motor power\):

**Speed = Distance / Time**

For example, your average speed might be:

**Speed = 33.4 inches / 2 seconds = 16.7 inches per second**

Once you know the average speed of your RedBot \(at that specific motor power\), you could calculate how much time it would take for your RedBot to drive a specific distance \(using the same motor power\):

**Time = Distance / Speed**

For example, if your RedBot's average speed were 16.7 inches per second and you wanted it to travel 24 inches, it would need to travel for this much time:

**Time = 24 inches / 16.7 inches per second = 1.437 seconds**

So your program could set the RedBot motors to drive \(at the same motor power used in your speed test\), wait 1.437 seconds \(1437 ms\), and then brake the motors. The RedBot should have traveled about 24 inches.

In fact, your program could include a custom function that will calculate the amount of time required to travel any specified distance. The custom function could also automatically turn on the motors for the calculated amount of time and then brake.

### driveCalcDist\(\) function

Here's a custom function named `driveCalcDist()` that would accomplish this:

```cpp
void driveCalcDist(float distance) {
    // calculates driving time for specified distance based on average driving speed
    // positive distance = forwards, negative distance = backwards

    // change these numbers to match your driving speed test results
    int power = 200; // motor power used in driving speed test
    int avgSpeed = 16.7; // average speed (inches per second)

    // if negative distance, reverse driving direction by using negative power
    if (distance < 0) power = power * -1;

    // calculate driving time (in milliseconds) based on distance and average speed
    long driveTime = (long) 1000 * abs(distance) / avgSpeed;

    // drive for calculated amount of time
    motors.drive(power);
    delay(driveTime);
    motors.brake();
}
```

**IMPORTANT:** You will need to change the numbers in the custom function for the `power` and `avgSpeed` so they match your speed test results. Not all RedBots will have the exact same average speed \(even if they use the same motor power\). Be sure to conduct a speed test using your specific RedBot.

You call this custom function by passing in a number representing the desired travel distance \(in inches\).

For example, to make the RedBot drive forward 36 inches:

```cpp
driveCalcDist(36);
```

You can also use this custom function to drive backwards by passing a **negative** number into the function.

For example, to make the RedBot drive backwards 12 inches:

```cpp
driveCalcDist(-12);
```

Of course, you might find that your Redbot doesn't always travel the exact distance that you specified. There are several factors that can affect the actual speed of your RedBot: the remaining battery power, the friction of the surface it is driving on, etc.

## Pivot by Specific Angle \(Using Average Turning Speed\)

It is extremely useful to be able to make your RedBot turn by a specific angle \(e.g., turn 90° to the right, etc.\), so it can follow a planned route or navigate through its environment.

One way to do this is to determine the average turning speed of your RedBot \(at a specific motor power\), and then use this to calculate how much time it will take to make your RedBot turn by any specific angle.

**NOTE:** Alternatively, you can use the [wheel encoders](wheel-encoders.md) to make your RedBot turn by a specific angle. This will typically be more accurate than using your RedBot's average turning speed.

The last activity in [RedBot Experiment 3](https://learn.sparkfun.com/tutorials/experiment-guide-for-redbot-with-shadow-chassis/experiment-3-turning) requires you to conduct a test to determine the average turning speed of your RedBot.

You can do this by measuring how far \(in degrees\) your RedBot turns in a specific amount of time \(such as 1 second\) at a specific motor power \(such as 100\). Conduct multiple trials \(at least 5\) to calculate the average angle turned by the RedBot. For each trial, be sure to use the same amount of time and the same motor power.

Alternatively, you can conduct multiple trials to determine which specific amount of `delay()` will make your RedBot turn by a specific angle \(recommend either 90° or 180°\) at a specific motor power \(such as 100\).

Then use your values for the angle and time to calculate the average turning speed of your RedBot \(at that specific motor power\):

**Turning Speed = Angle / Time**

For example, your average turning speed might be:

**Turning Speed = 180 degrees / 1.30 seconds = 138.5 degrees per second**

Once you know the average turning speed of your RedBot \(at that specific motor power\), you could calculate how much time it would take for your RedBot to turn by a specific angle \(using the same motor power\):

**Time = Angle / Turning Speed**

For example, if your RedBot's average turning speed were 138.5 degrees per second and you wanted it to turn by 45 degrees, it would need to turn for this much time:

**Time = 45 degrees / 138.5 degrees per second = 0.325 seconds**

So your program could set the RedBot motors to pivot \(at the same motor power used in your speed test\), wait 0.325 seconds \(325 ms\), and then brake the motors. The RedBot should have turned about 45 degrees.

In fact, your program could include a custom function that will calculate the amount of time required to turn by any specified angle. The custom function could also automatically pivot the motors for the calculated amount of time and then brake.

### pivotCalcAngle\(\) function

Here's a custom function named `pivotCalcAngle()` that would accomplish this:

```cpp
void pivotCalcAngle(float angle) {
    // calculates pivoting time for specified angle based on average turning speed
    // positive angle = turn CW to right, negative angle = turn CCW to left

    // change these numbers to match your turning speed test results
    int power = 100; // motor power used in turning speed tests
    int avgTurnSpeed = 138.5; // average turning speed (degrees per second)

    // if negative angle, reverse pivot direction by using negative power
    if (angle < 0) power *= -1;

    // calculate pivot time based on angle and average turning speed
    long turningTime = (long) 1000 * abs(angle) / avgTurnSpeed;

    // pivot to specified angle
    motors.pivot(power);
    delay(turningTime);
    motors.brake();
}
```

**IMPORTANT:** You will need to change the numbers in the custom function for the `power` and `avgTurnSpeed` so they match your turning speed test results. Not all RedBots will have the exact same average turning speed \(even if they use the same motor power\). Be sure to conduct a turning speed test using your specific RedBot.

You call this custom function by passing in a number representing the desired turning angle \(in degrees\).

For example, to make the RedBot turn clockwise to the right by 90°:

```cpp
pivotCalcAngle(90);
```

You can also use this custom function to turn counter-clockwise by passing a **negative** number into the function.

For example, to make the RedBot turn counter-clockwise to the left by 90°:

```cpp
pivotCalcAngle(-90);
```

Of course, you might find that your Redbot doesn't always turn by the exact angle that you specified. There are several factors that can affect the actual turning speed of your RedBot: the remaining battery power, the friction of the surface it is driving on, etc.

