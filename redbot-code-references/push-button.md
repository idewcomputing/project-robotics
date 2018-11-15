# Push Button

The RedBot mainboard has a built-in push button that can be detected by your program. The button is hardwired to pin D12 on the RedBot mainboard and is located next to the USB port.

The button can be used as a way for a user to control the RedBot \(e.g., pushing the button to make the RedBot perform a specific task\).

### How to Use the Push Button in a Program:

To detect input on the push button, choose one of the following approaches for your program:

* Read the button pin directly using a `digitalRead()` function
* Read the button using a `RedBotButton` object
* Use the `OneButton` library to detect different types of button presses \(single-press, double-press, or long-press\)

### Coding References in this Section:

* Read Button Pin Directly
* Read Button Using RedBotButton Object
* Pause Robot Program Until Button Pressed
* Use Button to Start \(and Stop\) Robot Program
* Detect Different Types of Button Presses Using OneButton Library

## Read Button Pin Directly

To directly detect button input, you will need to: 1. Declare a variable to store the button pin number 2. Set the pin mode for the button 3. Use the `digitalRead()` function to detect whether the button is being pushed

### 1. Declare Variable for Button Pin Number

Before your `setup()` function, declare a variable to store the push button pin number:

```cpp
const int button = 12;
```

* `const` indicates that the variable will be a constant, which means its value won't change during the program.
* `int` indicates the variable type, which is an **integer** in this case. All Arduino pins are treated as integers \(even analog pins that have a letter in their pin number\).
* `button` represents the name of the variable that stores the button's pin number. If desired, you could use a different variable name.
* `12` is the pin number for the button, which is hardwired to pin D12 on the RedBot mainboard.

### 2. Set Pin Mode for Button

Before your program can use the button, you must set its pin mode \(so the Arduino program knows whether the part connected to the pin is an input or output\).

Within your `setup()` function, use the `pinMode()` function to set the pin mode for the button pin:

```cpp
pinMode(button, INPUT_PULLUP);
```

* `button` represents the variable that stores the button's pin number. If necessary, change this to the variable name you used for your button pin. \(You could list the pin number directly, instead of listing a variable that stores the number. However, your program will be easier to read and understand if you use a variable.\)
* `INPUT_PULLUP` indicates that the button pin will be used for input \(instead of output\) and will use a built-in pullup resistor \(which something that buttons and switches typically require\).

### 3. Use `digitalRead()` to Detect Button Push

To read the button, use a `digitalRead()` function to detect whether or not the button is being pushed: `digitalRead(button)`

If the function returns a value of `LOW`, it means the button is currently being pushed. \(A value of `HIGH` means the button is currently not being pushed.\)

This `digitalRead()` function is typically inserted within an `if` statement, so you can detect which condition is true \(`LOW` or `HIGH`\):

```cpp
if (digitalRead(button) == LOW) {
    // add code to perform when button is pushed

}
else {
    // OPTIONAL: add code to perform if button NOT pushed
    // motors.brake();
}
```

The `else` statement is **optional**. If your program doesn't need to perform any special actions when the button is not being pushed, then don't add any commands inside the `else` statement — or you can remove the `else` statement entirely, including its curly braces `{ }`.

## Read Button Using RedBotButton Object

Another way to read the button is to use a `RedBotButton` object created from the class built into the SparkFun `RedBot` library.

To read the button this way, you will need to: 1. Include the `RedBot` library in your program 2. Create a `RedBotButton` object assigned to a variable 3. Use the object's `read()` method to detect whether the button is being pushed

### 1. Include RedBot Library

Be sure that your program includes a copy of the SparkFun `RedBot` library. If necessary, see the instructions for [how to include the RedBot library](redbot-library.md).

### 2. Create RedBotButton Object

Before your `setup()` function, create a `RedBotButton` object by assigning it to a variable:

```cpp
RedBotButton button;
```

* `RedBotButton` indicates the class of object being created \(this class is part of the `RedBot` library\)
* `button` represents the variable name for the `RedBotButton` object. If desired, you could use a different variable name.

Creating a `RedBotButton` object will automatically set the pin number \(`12`\) and pin mode \(`INPUT_PULLUP`\) for the button.

### 3. Use `button.read()` to Detect Button Push

To read the button, use the `RedBotButton` object's `read()` method to detect whether or not the button is being pushed: `button.read()`

If the method returns a value of `true`, it means the button is currently being pushed. \(A value of `false` means the button is currently not being pushed.\)

This `button.read()` method is typically inserted within an `if` statement, so you can detect which condition is true \(`true` or `false`\):

```cpp
if (button.read() == true) {
    // add code to perform when button is pushed

}
else {
    // OPTIONAL: add code to perform if button NOT pushed
    // motors.brake();
}
```

**NOTE:** If you used a different name for your `RedBotButton` object, then change `button` to match the name of your variable. For example, if you used `switch` as your object variable name, your code should use `switch.read()` to detect a button push.

The `else` statement is **optional**. If your program doesn't need to perform any special actions when the button is not being pushed, then don't add any commands inside the `else` statement — or you can remove the `else` statement entirely, including its curly braces `{ }`.

You can either insert this code into your `loop()` function or into a custom function that is called by your `loop()` function.

## Pause Robot Program Until Button Pressed

You can also add "pauses" in your program that will make your RedBot wait until a person presses the button before going on to the next step in your program.

This could be useful in your project demonstration:

* You could add a "pause" for a simulated step in the robot's task. The RedBot will "pause" while someone on your team completes or explains the simulated step. Then the RedBot will continue with the next step in the task when the button is pressed.
* You could have the RedBot pause between tasks or scenarios. This will give your team time to introduce the next task/scenario and make any necessary changes in the testing environment \(such as moving objects, etc.\).

The "pause" is created using a `while()` loop that will keep repeating itself until the button is pressed. The `while()` loop will simply contain a short delay before checking the button again.

```cpp
while (button.read() == false) delay(10); // pause until button pressed
```

Simply add this "pause" `while()` loop anywhere you want the RedBot to pause and wait for the button to be pressed before continuing with the program. You can add as many "pauses" as you need.

For example, the following program `loop()` will start out by waiting until the button is pressed. Once the button is pressed, the RedBot will drive forward for 1 second and stop. Then the RedBot will "pause" and wait for the button to be pressed again. Once the button is pressed again, the RedBot will drive backwards for 1 second and stop. Then the program `loop()` will repeat itself \(by pausing again\).

```cpp
void loop() {
    while (button.read() == false) delay(10); // pause until button pressed
    // drive forward for 1 second and stop
    motors.drive(150);
    delay(1000);
    motors.stop();
    while (button.read() == false) delay(10); // pause until button pressed
    // drive backwards for 1 second and stop
    motors.drive(-150);
    delay(1000);
    motors.stop();
}
```

**NOTE:** Be sure to include a command to stop your RedBot's motors before "pausing" it. Otherwise, if the RedBot was driving, it will continue to do so, even while waiting for the button to be pressed.

## Use Button to Start \(and Stop\) Robot Program

It can be helpful to use the button to "start" the RedBot's program — i.e., to prevent it from doing anything unless someone has "started" it by pushing the button. Once the button is pushed, the RedBot will perform its task \(such as driving in a specific pattern, etc.\). You can also "stop" the RedBot by picking it up and pressing the button again.

To do this, the RedBot needs a way to keep track of whether it has been "started" — one way to do this is to create a variable to store the current state of the RedBot \(started vs. not started\).

Add this global variable before your `setup()` function:

```cpp
boolean started = false;
```

* `boolean` indicates the variable type. A **boolean** variable can have a value of either `true` or `false`.
* `started` represents the name of the variable that will be used to indicate whether or not the RedBot has been started. If desired, you could use a different variable name.
* `false` is the initial value for the variable \(because we want the RedBot to be stopped when the program begins\).

This variable will be used in your `loop()` function to decide whether or not to perform the RedBot's task:

```cpp
void loop() {

    checkButton();

    if (started) {
        // add code for task to perform when device is started

        started = false; // include to only perform task once
    }
    else {
        // add code to stop device
        motors.stop();
    }
}
```

Notice that the first command in the `loop()` is to call a custom function named `checkButton()`, which will check whether the button is being pushed, and if so, it will reverse the value of `started` \(e.g., changing `false` to `true`\).

Notice that the second command in the `loop()` is an `if` statement that will only be performed when the value of `started` is `true`. You will need to add code inside the `if` statement to provide instructions for whatever task the RedBot should perform once it is started.

Notice that inside the `if` statement, the value of `started` was changed back to `false` at the end of the task. This will ensure the task is performed only once per button press. However, if you want the task to keep being performed in a continuous loop, then just remove this line of code.

An `else` statement is included that will only be performed when the value of `started` is `false`. It simply stops the motors. If you want, you could add other code. For example, you could make the LED blink as a signal to let the person know the robot is in "standby" mode, waiting to be started.

### checkButton\(\) function

Be sure to include the custom function named `checkButton()` after your `loop()` function:

```cpp
void checkButton() {
    if (button.read() == true) {
        // reverse value of "started"
        started = !started;

        // single-blink and single-beep as feedback
        digitalWrite(led, HIGH);
        tone(buzzer, 3000);
        delay(200);
        digitalWrite(led, LOW);
        noTone(buzzer);
    }
}
```

If the button is pressed, the custom function will reverse the value of `started` by setting its value to `!started` \(which represents its opposite value\):

* If the current value of `started` is `false`, it will change it to `true`, which will "start" the RedBot.
* If the current value of `started` is `true`, it will change it to `false`, which will "stop" the RedBot.

The `if` statement in the custom function uses a `RedBotButton` object to read the button. However, you could modify the `if` statement to read the button directly using a `digitalRead()` command.

**NOTE:** In order to make the `led` blink and `buzzer` beep, you'll need to include additional code to declare these global variables, assign their pin numbers, and set their pin modes.

## Detect Different Types of Button Presses Using OneButton Library

The RedBot mainboard only has one button. However, it is possible to detect different types of input events using this one button. For example, you could detect the difference between a single-press, double-press, or long-press. Each input event could make your RedBot perform a different task.

The easiest way to detect these different button input events is to use the `OneButton` library, which was created specifically for this purpose.

To read the button this way, you will need to: 1. Include the `OneButton` library in your program 2. Create a `OneButton` object assigned to a variable 3. Designate custom functions for each button input event 4. Add the code for the custom functions 5. Use the object's `tick()` method to check for button input events

### 1. Include OneButton Library

In order to use the `OneButton` library, you must include a copy of the library at the beginning of your Arduino program.

If necessary, you might need to first add the library to your code editor \(this is a one-time process\).

### Add OneButton Library to Code Editor \(one-time process\)

#### Arduino Create Web Editor

If you're using the Arduino Create web editor, you should add the `OneButton` library to your "Favorites" tab in the "Libraries" menu. **You'll only need to do this once**, and then you'll be able to quickly and easily include a copy of this library in your programs: 1. In the Arduino Create web editor, click "Libraries" in the navigation menu on the left. 2. Click the "Library Manager" button near the top-left \(in order to search the libraries contributed by Arduino community members\). 3. In the pop-up, type `onebutton` into the "Search Libraries" field, and press enter. 4. In the search results, click the star icon to the right of "OneButton" in order to add this library to your Favorites. Then click the "Done" button to close the pop-up. 5. The "OneButton" library should now be listed in your "Favorites" tab of the "Libraries" menu.

#### Arduino IDE Desktop Editor

If you're using the desktop version of the Arduino IDE code editor, you need to download the `OneButton` library to your computer, which will add it to your list of libraries in the "Sketch" menu. **You only need to do this once**, and then you'll be able to quickly and easily include a copy of the `OneButton` library in your programs.

1. Open the Arduino IDE application on your computer.
2. Under the "Sketch" menu, select "Include Library" and then select "Manage Libraries" in the sub-menu.
3. A pop-up will appear. It will list all the Arduino libraries available for downloading. \(If you have a slower Internet connection, it make take a few seconds for the full list to populate\). Type `onebutton` into the search field at the top-right, and press enter.
4. In the search results, select the most recent version of the "OneButton" library and then click the "Install" button.
5. After the library has downloaded and installed, click the "Close" button to close the pop-up.

### Include OneButton Library in Program \(once per program\)

#### Arduino Create Web Editor

In your library "Favorites" tab, hover over "OneButton" and click the "Include" button.

#### Arduino IDE Desktop Editor

Under the "Sketch" menu, select "Include Library" and then select "OneButton" in the sub-menu \(the library will be listed toward the bottom under **Contributed Libraries**\).

#### Both Editors

The following code should have been **automatically** inserted at the top of your program:

```cpp
#include <OneButton.h>
```

### 2. Create OneButton Object

Before your `setup()` function, create a `OneButton` object by assigning it to a variable:

```cpp
OneButton button(12, true);
```

* `OneButton` indicates the class of object being created \(this class is part of the `OneButton` library\)
* `button` represents the variable name for the `OneButton` object. If desired, you can use a different variable name.
* `12` is the pin number for the button, which is hardwired to pin D12 on the RedBot mainboard.
* `true` indicates that the button pin has a value of `LOW` when the button is pushed. This will be used to set the button's pin mode to `INPUT_PULLUP`.

### 3. Designate Custom Functions for Button Input Events

In your `setup()` function, you must designate the names of the custom functions you want to be called when the various button input events are detected \(single-press, double-press, or long-press\).

```cpp
void setup() {

    // add any other code needed in setup

    // designate custom functions for button input events
    button.attachClick(singlePress);
    button.attachDoubleClick(doublePress);
    button.attachPress(longPress);
}
```

* `singlePress` is the name of the custom function to call when a single-press is detected. If desired, you can change the name of this function.
* `doublePress` is the name of the custom function to call when a double-press is detected. If desired, you can change the name of this function.
* `longPress` is the name of the custom function to call when a long-press is detected. If desired, you can change the name of this function.

**NOTE:** If you used a different name for your `OneButton` object, then change `button` to match the name of your variable. For example, if you used `switch` as your object variable name, your code should use `switch.attachClick()` to designate the name of the custom function for a single-press, etc.

If you don't want to detect a specific button input event, just exclude it \(either delete it or make it into a comment\). For example, if you don't want to detect a long-press, then simply exclude the line of code that attaches a custom function to that input event.

### 4. Add Code for Custom Functions

After your `loop()` function, add the code for each of the custom functions for the various button input events:

```cpp
// custom functions for different button input events

void singlePress() {
    // add code to perform when single-press detected

}

void doublePress() {
    // add code to perform when double-press detected

}

void longPress() {
    // add code to perform when long-press detected

}
```

Be sure the names of the custom functions match the names that you designated in the `setup()` function for the button input events.

Inside each custom function, you need to add code for the specific actions you want performed for that input event.

**TIP:** You may want to include feedback for each input event to confirm to the person that the input was correctly detected. For example, the buzzer \(speaker\) and/or built-in LED light could be could be used to provide feedback by mimicking the button input pattern that was detected:

* the buzzer could be made to produce a single-beep, double-beep, or long-beep
* the LED light could be made to produce a single-blink, double-blink, or long-blink

For example:

```cpp
void singlePress() {

    // single-blink and single-beep as feedback
    digitalWrite(led, HIGH);
    tone(buzzer, 3000);
    delay(200);
    digitalWrite(led, LOW);
    noTone(buzzer);

    // add other code to perform when single-press detected

}
```

### 5. Use `button.tick()` to Detect Button Input Events

In your `loop()` function, use the `OneButton` object's `tick()` method to check for button input events. Whenever a specific button input event is detected, the custom function that you previously designated will automatically be called.

```cpp
void loop() {

    button.tick(); // check for button input events

    // OPTIONAL: can add other code to perform

}
```

**NOTE:** If you used a different name for your `OneButton` object, then change `button` to match the name of your variable. For example, if you used `switch` as your object variable name, your code should use `switch.tick()` to detect button input events.

