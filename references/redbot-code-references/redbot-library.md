# RedBot Library

There is a SparkFun code library called `RedBot` that makes it easier to control the motors and sensors connected to your RedBot. You will need to include a copy of the `RedBot` code library in your programs.

The `RedBot` library contains Arduino code that defines different classes of objects. Each class defines a set of **properties** \(variables\) and **methods** \(functions\) for a specific type of object.

For example, the `RedBot` library defines the following classes:

* `RedBotButton` class — used to control the push button
* `RedBotMotors` class — used to control the left and right motors
* `RedBotBumper` class — used to control the left and right mechanical bumper switches
* `RedBotSensor` class — used to control analog sensors, such as the line-following sensors
* `RedBotEncoder` class — used to control the left and right wheel encoders
* `RedBotAccel` class — used to control the accelerometer

Your programs will use these classes to create objects. An object is a special type of variable that represents a specific **instance** \(member\) of a class. An object has all the properties \(variables\) and methods \(functions\) defined for that class.

## Add RedBot Library to Code Editor \(one-time process\)

### Arduino Create Web Editor

If you're using the Arduino Create web editor, you should add the `RedBot` library to your "Favorites" tab in the "Libraries" menu. **You only need to do this once**, and then you'll be able to quickly and easily include a copy of the `RedBot` library in your programs.

1. Login to the [Arduino Create web editor](https://create.arduino.cc/editor/) using your Arduino account.
2. Click "Libraries" in the navigation menu on the left.
3. Click the "Library Manager" button at the top of the middle panel. This will allow you to search the libraries contributed by Arduino community members.
4. In the pop-up, type `redbot` into the "Search Library" field, and press enter.
5. In the search results, click the star icon to the right of "SparkFun RedBot Library" to add this library to your Favorites. Then click the "Done" button to close the pop-up.

### Arduino IDE Desktop Editor

If you're using the desktop version of the Arduino IDE code editor, you need to download the `RedBot` library to your computer, which will add it to your list of libraries in the "Sketch" menu. **You only need to do this once**, and then you'll be able to quickly and easily include a copy of the `RedBot` library in your programs.

1. Open the Arduino IDE application on your computer.
2. Under the "Sketch" menu, select "Include Library" and then select "Manage Libraries" in the sub-menu.
3. A pop-up will appear. It will list all the Arduino libraries available for downloading. \(If you have a slower Internet connection, it make take a few seconds for the full list to populate\). Type `redbot` into the search field at the top-right, and press enter.
4. In the search results, select the most recent version of the "SparkFun RedBot Library" and then click the "Install" button.
5. After the library has downloaded and installed, click the "Close" button to close the pop-up.

## Include RedBot Library in Program \(once per program\)

### Arduino Create Web Editor

1. Create a new program, or open an existing program.
2. In your library "Favorites" tab, hover over "SparkFun RedBot Library" and click the "Include" button.

### Arduino IDE Desktop Editor

1. Create a new program, or open an existing program.
2. Under the "Sketch" menu, select "Include Library" and then select "SparkFun RedBot Library" in the sub-menu \(the library will be listed toward the bottom under **Contributed Libraries**\).

### Both Editors

The following code should have been **automatically** inserted at the top of your program:

```cpp
#include <RedBot.h>
#include <RedBotSoftwareSerial.h>
```

The `#include` statements shown above actually add two RedBot libraries to your program:

* The first library is the main RedBot library, which is what you need.
* The second library is the RedBot Software Serial library, which can be used to transfer data between the RedBot and certain types of add-on parts \(sold separately\). Unless you added one of these special parts, you don't need this second library.

You can **delete** the second `#include` statement for the RedBot Software Serial library, as you won't need it. \(Arduino already has a built-in Serial class that you can use to send data from your RedBot to your computer.\)

