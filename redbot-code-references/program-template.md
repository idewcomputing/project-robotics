# Program Template

You want to have a clear framework or template for your robot demonstration program. This will make it easier for you \(and others\) to review, understand, and edit the program. For example, break down your program into identifiable chunks and carefully consider what code should belong in each.

Here are the recommended "building blocks" for your robot demonstration program _listed in order from top to bottom of a single program file_:

## REDBOT LIBRARY, GLOBAL VARIABLES, AND OBJECTS

Your program should have a comment block `/* */` at the very top to list your program title, team member names, and other information.

**IMPORTANT:** Your program must `#include` the SparkFun RedBot Library, in order to utilize the built-in classes and methods \(functions\) defined in this library, which will allow you to control your robot's motors, sensors, and other parts.

Your program will need to declare global variables to store certain types of information and assign initial values to the variables. For example, variables are typically declared to store the pin numbers for certain outputs \(such as the buzzer, etc.\).

You'll also need to create objects \(special types of variables\) for the motors and sensors \(wheel encoders, IR line sensors, etc.\) being used in the program. These objects are created from classes defined in the RedBot library.

```cpp
/*
  Robot Program Title
  Team Member Names
*/

// SparkFun RedBot Library
#include <RedBot.h>

// declare global variables and create objects
```

## SETUP FUNCTION

Every program must contain a `setup()` function. The code inside the `setup()` will run one time when your program first starts.

```cpp
// This runs one time only when the program first starts
// This typically sets pin modes for certain sensors and outputs
void setup() {

}
```

## LOOP FUNCTION

Every program must contain a `loop()` function. The code inside the `loop()` will run over and over again in a "loop" after the `setup()` has finished.

Rather than putting all the code for your robot scenarios inside the `loop()`, you'll split the code for the scenarios into separate custom functions which will be "called" by the `loop()` at the appropriate time.

```cpp
// This runs over and over in a loop (after setup finishes) 
// This will contain logic to decide which scenario to run
void loop() {

}
```

## SCENARIO 1 FUNCTION

You should create a custom function that contains the code to perform the actions and decisions to demonstrate your first scenario:

```cpp
// This contains the actions and decisions to demo our 1st scenario
void scenario1() {
  // add code here

  // set global variables for 2nd scenario
  scenario = 2;
  started = false;  
}
```

## SCENARIO 2 FUNCTION

You should create a custom function that contains the code to perform the actions and decisions to demonstrate your second scenario:

```cpp
// This contains the actions and decisions to demo our 2nd scenario
void scenario2() {
  // add code here

  // set global variables for 3rd scenario
  scenario = 3;
  started = false;  
}
```

## SCENARIO 3 FUNCTION

You should create a custom function that contains the code to perform the actions and decisions to demonstrate your third scenario:

```cpp
// This contains the actions and decisions to demo our 3rd scenario
void scenario3() {
  // add code here

  // set global variables for 1st scenario
  scenario = 1;
  started = false;  
}
```

## UTILITY FUNCTIONS

You will need to include pre-built custom functions that contains code to perform specific sub-tasks such as driving, turning, detecting lines, detecting objects, checking the button, making sounds, etc.

These "utility" functions will be run when they are "called" within other functions, such as the `loop()` function and the custom functions for your scenarios.

It is recommended that every robot demo program contain these "utility" functions \(at a minimum\):

```cpp
void checkButton() {
  // add code for this custom function
}

void driveDistance(float distance, int power) {
  // add code for this custom function
}

void pivotAngle(float angle) {
  // add code for this custom function
}
```

The full code for the pre-built custom functions are listed in other sections of the [RedBot Code References](./) — check the "Quick Links".

**IMPORTANT:** Your program will most likely need to include certain other pre-built custom functions \(such as `driveStraight()`, `followLine()`, `countLine()`, `followCountLine()`, `checkBumpers()`, `measureDistance()`, `avoidCollision()`, etc.\). The specific custom functions that you should include depend on your robot's navigation method\(s\) and the specific sensors/features you're using in your demonstration.

Furthermore, you might want or need to create some of your own custom functions to perform specific actions or decisions.

