# Arduino Programming

![](../../.gitbook/assets/arduino_logo.png)

The RedBot device runs programs written in a computer language called [Arduino](https://www.arduino.cc/reference/en/).

To be more accurate, Arduino is actually a code library written in another computer language called [C++](https://en.wikipedia.org/wiki/C%2B%2B) \(similar to how jQuery is a code library written in JavaScript\). If needed, your Arduino program can incorporate code written directly in C++.

The Arduino "language" is designed to make it easier to write programs for microcontrollers, which are small, low-cost, low-power computers that control physical inputs and outputs \(such as sensors, lights, motors, etc.\).

![](../../.gitbook/assets/arduino-uno.jpg)

An Arduino microcontroller board contains a processor \(CPU\), memory \(RAM\), storage \(Flash\), input/output pins, a USB port \(for data transfer\), and a power supply input \(typically battery-powered\). A microcontroller doesn't have a keyboard, monitor, or other peripherals that full-size computers usually have. A microcontroller is also much less powerful than a full-size computer: a microcontroller has a slower processor, less memory, less storage, etc.

So why even use a microcontroller if it seems so limited in power? Microcontrollers are perfectly suited for performing dedicated computing tasks that don't require a full-size computer. Microcontrollers are also small enough \(and cheap enough\) that they can be embedded inside other devices. Want to create a "smart" device? Use a microcontroller, and create a program for it.

An Arduino program is also referred to as a **sketch** because the Arduino language is designed to allow you to quickly create a program — just like a sketch is a quick drawing.

The [Arduino Programming Language Reference](https://www.arduino.cc/reference/en/) is helpful for understanding the structure and syntax of Arduino code.

## Arduino Code Editor

It is highly recommended that you use the online [Arduino Create Web Editor](https://create.arduino.cc/editor/) to create and save your Arduino programs in the cloud. This web editor is free-to-use, always up-to-date, and allows you can access your programs from any browser.

Alternatively, you can download a desktop version of the [Arduino IDE](https://www.arduino.cc/en/Main/Software) code editor, which saves your programs locally on your computer.

There are different types of [Arduino microcontroller boards](https://www.arduino.cc/en/Main/Products), which have slightly different capabilities. The Arduino code editor will need to know which Arduino board you are using:

* The RedBot mainboard is equivalent to: **Arduino/Genuino Uno**

## Arduino Devices Run One Program at a Time

Arduino devices, such as the RedBot, can only store and run **one** program at a time. If you want to change the program running on the device, you have to upload a different program onto the device.

However, you can create and save **multiple** programs in your Arduino account \(if using the online Arduino Create Web Editor\) or on your computer \(if using the desktop Arduino IDE\).

A USB cable is used to connect your Arduino device to your computer, in order to upload an Arduino program onto the device.

The USB connection can also be used to transmit data between the Arduino device and your computer while a program is running on the Arduino device. This data communication can be displayed in a serial monitor available in the Arduino code editor. This is often used as a way to troubleshoot programs \(by displaying messages or data\) or to verify that sensors are working correctly \(by displaying sensor measurements\).

Some Arduino devices have a built-in WiFi chip that allows them to wirelessly update their program and transmit data. However, the RedBot does not have WiFi capabilities built-in.

## Arduino Program Structure

All Arduino programs include these two core functions:

* **setup function** — which runs one-time when your program first starts. The `setup()` function is typically used to set pin modes for the device's inputs and outputs, initialize certain settings or variables, and perform any other code that should occur at the start of the program.
* **loop function** — which starts to run when the `setup()` function is done, and then runs over and over in an endless loop. The `loop()` function typically contains the main tasks of your program.

```cpp
void setup() {
    // add code here

}

void loop() {
    // add code here

}
```

In fact, if you wanted your device to only perform a task one-time, you could list all your code inside the `setup()` function and just leave the `loop()` function empty. However, in nearly all cases, you'll put the code for your tasks into the `loop()`, so the device can continuously perform whatever tasks you've programmed it to do.

If your device is restarted — by pressing its "reset" button or by turning the power off and then back on — the device's program will start over by running the `setup()` function one-time and then running the `loop()` function repeatedly.

Here's two simple rules to follow when coding an Arduino program: 1. Your program **must** have a `setup()` function and a `loop()` function, even if there is no code inside the function. 2. Your program **cannot** have more than one `setup()` function or more than one `loop()` function.

Besides having the required `setup()` and `loop()` functions, most Arduino programs will also have:

* **libraries** — which are included as "links" at the very beginning of the program. These external code libraries provide additional functions that your program can utilize. For example, your robot programs will need to include the SparkFun `RedBot.h` library, which has methods \(functions\) used to control the RedBot motors and sensors.
* **global variables and objects** — which are typically declared before the `setup()` function. These variables are used to store data that will be used in your program's functions. In your robot program, some of your variables will be objects created from classes defined in the RedBot library.
* **custom functions** — which are typically listed at the very end of your program, after the `loop()` function. Custom functions are used to contain code that performs specific tasks. Custom functions are optional, but they can help break up your code into smaller modules that can be easier to understand \(and easier to re-use\). The code inside a custom function is only run if and when the custom function is "called" within the `setup()` or `loop()` function. A custom function can also be "called" within another custom function.
* **comments** — which can be embedded throughout a program wherever they may be helpful. Comments are just notes that help explain the code to people reading the program. Comments are optional, but they can help clarify portions of the code to yourself or to others. You decide if and where to add comments. Any comments in the program are ignored when the program is compiled and uploaded to the device. Comments can be [single-line](https://www.arduino.cc/reference/en/language/structure/further-syntax/singlelinecomment/) or [multi-line](https://www.arduino.cc/reference/en/language/structure/further-syntax/blockcomment/).

To summarize, the code structure \(in order\) for an Arduino program is: 1. Included Libraries 2. Global Variables and Objects 3. Setup Function 4. Loop Function 5. Custom Functions 6. Comments \(embedded throughout\)

Here's an example of a simple Arduino program, so you can see how its code structure follows this pattern:

```cpp
/*
Example Arduino Program
Push Button to Produce Beep
*/

// SparkFun RedBot Library - Version: Latest
#include <RedBot.h>

// global variables
const int buzzer = 9; // buzzer connected to pin 9
RedBotButton button;

// setup function runs one-time at start
void setup() {
    pinMode(buzzer, OUTPUT);
}

// loop function runs over and over after setup done
void loop() {
    // see if button pushed
    if (button.read() == true) {
        singleBeep(); // call custom function
    }
}

// custom function runs only when it is called
void singleBeep() {
    tone(buzzer, 3000); // turn on sound at frequency 3000 Hz
    delay(200); // wait 0.2 seconds
    noTone(buzzer); // turn off sound
}
```

For comparison, here's a modified version of the same program. It does the **exact same task**, except the program does not include any comments, libraries, global variables, or custom functions. It just has the `setup()` and `loop()` functions:

```cpp
void setup() {
    pinMode(12, INPUT_PULLUP);
    pinMode(9, OUTPUT);
}

void loop() {
    if (digitalRead(12) == LOW) {
        tone(9, 3000);
        delay(200);
        noTone(9);
    }
}
```

While this second version of the program is obviously much more concise, it is actually more difficult to understand what the program is supposed to do. This is one reason \(among many other reasons\) why comments, libraries, variables, and custom functions are useful in programming.

## Create New Program

### Arduino Create Web Editor

To create a new sketch \(program\) in the Arduino Create Web Editor: 1. If necessary, click the "Sketchbook" menu in the left navigation panel to display your list of existing sketches. 2. Click the "New Sketch" button at the top of the middle panel.

### Arduino IDE Desktop Editor

To create a new sketch \(program\) in the desktop version of the Arduino IDE code editor, do one of the following:

* Under the "File" menu, select "New"
* Alternatively, you can click the "New" icon \(looks like a document\) at the top of the code editor window.

### Both Editors

The editor will create a new sketch that **automatically** contains starter code similar to below:

```cpp
void setup() {
  // put your setup code here, to run once:

}

void loop() {
  // put your main code here, to run repeatedly:

}
```

## Add Comment Block for Program Title & Info

It is recommended to insert a comment block at the very top of your program to list a title for your program, as well as any information that might be helpful to you or to anyone else reviewing the program code.

A blank comment block is created with slashes and asterisks like this:

```cpp
/*

*/
```

In between the asterisks, you can list as many lines of comments as you want or need. This would be a good place to name your program and if necessary, describe its purpose. You could also include other information, such as your class period, name, etc. Your teacher might have specific information that should be listed in this block comment.

For example, your block comment might look like this:

```cpp
/*
Experiment 7 - Wheel Encoder Test
Period 2, Team 1 - Destiny, Katya, Lucas, Miguel
January 18, 2018
*/
```

## Rename Program

By default, the new sketch will be given a generic filename that starts with `sketch_` and includes the current date \(plus a letter, such as: a, b, c, etc.\).

You should rename your new sketch to give it a filename that will make it easy for you or anyone else to identify and find the program later.

### Arduino Create Web Editor

1. Hover over the 3-dot button at the top of the right panel, and then select "Rename Sketch..."
2. In the pop-up, replace the generic sketch name with a unique filename.
   * Use a name that will make it easy for anyone to identify this sketch later \(especially once you have multiple sketches saved in your Arduino account\).
   * The filename cannot contain any spaces \(instead you can use the underscore character as a "space"\).
   * Your teacher might have a specific filename format that you should use for certain programs.
3. Save the new name by closing the pop-up: either press enter, or click the "OK" button.

### Arduino IDE Desktop Editor

**Rename New Program \(not yet saved\):** Under the "File" menu, select "Save". A pop-up dialog window will appear. Enter a new filename, and then click the "Save" button.

**Rename Existing Program \(previously saved\):** Click the down arrow icon in the top-left of the code editor window, and then select "Rename" in the drop-down list. A small dialog will appear at the bottom of the code editor window. Enter a new filename, and then click the "OK" button.

## Add Other Code to Complete New Program

To complete your program's code, you will need to:

* include any necessary libraries \(such as the `RedBot.h` library\)
* declare any necessary global variables, and assign values as necessary
* add any necessary code into the `setup()` function
* add any necessary code into the `loop()` function
* add any necessary code for custom functions
* add comments where it may be helpful to explain the code

As needed, consult the [Arduino Programming Language Reference](https://www.arduino.cc/reference/en/) for help understanding the structure and syntax of Arduino code.

## "Hello World" Test Program

When learning a new coding language, many people first create what is called a "Hello World" program. Traditionally, this involves displaying the text "Hello World" on the screen. The purpose is to demonstrate that you can create a simple working program in the new coding language. It's basically a "test" program before you start getting more ambitious.

Obviously, the RedBot doesn't have a screen for displaying text. However, the RedBot mainboard — like most other microcontroller boards — has a built-in LED light hardwired to its D13 pin.

So for physical computing devices, a common "Hello World" program is to make its built-in LED blink on and off in a repeating pattern. In fact, [RedBot Experiment 1](https://learn.sparkfun.com/tutorials/experiment-guide-for-redbot-with-shadow-chassis/experiment-1-software-install-and-basic-test) uses this type of "Hello World" program to verify that: \(1\) your device is working correctly, and \(2\) you are able to program it successfully.

```cpp
/*
  Hello World
  Make built-in LED blink
*/

const int led = 13;

void setup() {
  // put your setup code here, to run once:
  pinMode(led, OUTPUT);
}

void loop() {
  // put your main code here, to run repeatedly:
  digitalWrite(led, HIGH);
  delay(500);
  digitalWrite(led, LOW);
  delay(500);
}
```

After uploading this program to your RedBot, you should see that its built-in LED light blinks on and off every 0.5 seconds \(500 milliseconds\).

Next, try modifying the code to change the LED blinking pattern. Upload your modified program to your RedBot to see what your changes do.

* Can you make the LED blink faster?
* Can you make it blink slower?
* Can you make it blink in a different patterns \(maybe similar to Morse code\)?

