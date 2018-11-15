# LED Light

The RedBot mainboard has a built-in green LED light that can be controlled by your program. The LED is hardwired to pin D13 on the RedBot mainboard and is located near the center-right of the mainboard.

The LED light is often used for testing purposes \(e.g., to verify that your program is running\). However, the LED light can also be used to provide visual feedback.

### How to Use the LED in a Program:

To control the built-in LED, you will need to: 1. Declare a variable to store the LED pin number 2. Set the pin mode for the LED 3. Use the `digitalWrite()` and `delay()` functions to turn the LED on and off.

**NOTE:** The SparkFun RedBot library does not have a built-in class for the LED.

### Coding References in this Section:

* Declare Variable for LED Pin Number
* Set Pin Mode for LED
* Turn LED On \(and Off\)
* Produce Different LED Blinking Patterns

## Declare Variable for LED Pin Number

Before your `setup()` function, declare a variable to store the LED pin number:

```cpp
const int led = 13;
```

* `const` indicates that the variable will be a constant, which means its value won't change during the program.
* `int` indicates the variable type, which is an **integer** in this case. All Arduino pins are treated as integers \(even analog pins that have a letter in their pin number\).
* `led` represents the name of the variable that stores the LED's pin number. If desired, you could use a different variable name.
* `13` is the pin number for the LED. \(Most Arduino devices have a built-in LED hardwired to pin D13.\)

## Set Pin Mode for LED

Before your program can control the LED, you must set its pin mode \(so the Arduino program knows whether the part connected to the pin is an input or output\).

Within your `setup()` function, use the `pinMode()` function to set the pin mode for the LED pin:

```cpp
pinMode(led, OUTPUT);
```

* `led` represents the variable that stores the LED's pin number. If necessary, change this to the variable name you used for your LED pin. \(You could list the pin number directly, instead of listing a variable that stores the number. However, your program will be easier to read and understand if you use a variable.\)
* `OUTPUT` indicates that the LED pin will be used for output \(instead of input\).

## Turn LED On \(and Off\)

To turn on the LED light, use the `digitalWrite()` function to set the LED pin to a value of `HIGH` \(which will **allow** electric current to flow through the LED pin\):

```cpp
digitalWrite(led, HIGH); // turn on
```

This command could be used in your `setup()` function, `loop()` function, and/or a custom function.

Once this command is performed, the LED will stay on until your program turns the LED off again.

### Add Delay Before Turning LED Off

The `delay()` function can be used to add a waiting period \(in milliseconds\) before turning the LED off:

```cpp
delay(time);
```

* `time` represents the amount of time \(in milliseconds\) that the program should wait before performing the next command in the code. List the number of milliseconds for your delay \(1000 ms = 1 second\).

To produce a quick "blink" of the LED only requires a fraction of second, so you'll often use a delay value less than 1000.

### Turn Off LED

To turn off the LED light, use the `digitalWrite()` function to set the LED pin to a value of `LOW` \(which will **prevent** electric current from flowing through the LED pin\):

```cpp
digitalWrite(led, LOW); // turn off
```

This command could be used in your `setup()` function, `loop()` function, and/or a custom function.

Once this command is performed, the LED will stay off until your program turns the LED on again.

## Produce Different LED Blinking Patterns

You can combine `digitalWrite()` and `delay()` commands to make the LED turn on and off in whatever pattern you want.

For example, to make the LED blink once:

```cpp
digitalWrite(led, HIGH); // turn on
delay(500); // leave on for 0.5 seconds
digitalWrite(led, LOW); // turn off
```

You can modify your code to make the LED light blink in different patterns, which might be useful as visual feedback:

* You can use different `delay()` values to determine how long the LED stays on \(and how long it pauses between blinks\).
* You can use multiple pairs of `digitalWrite()` and `delay()` commands — or a `for()` loop that runs a set of commands multiple times — to make the LED blink a certain number of times in a row.

For example, the LED could be used to provide visual feedback when a person presses the built-in push button on the RedBot mainboard:

```cpp
if (button.read() == true) {
    // single-blink
    digitalWrite(led, HIGH);
    delay(200);
    digitalWrite(led, LOW);

    // add other code to perform when button pushed

}
```

As another example, you can use a `for` loop to make the LED blink three times rapidly:

```cpp
// triple-blink
for (int i=0; i < 3; i++) {
    digitalWrite(led, HIGH);
    delay(100);
    digitalWrite(led, LOW);
    delay(100); // pause before next blink
}
```

You could program your RedBot to use different LED patterns as a way to provide feedback or communicate information to people. Some questions to think about:

* When might it be useful for your device to use the LED for feedback, alerts, notifications, etc.?
* What kinds of blinking patterns will be most easily seen and understood by people?

