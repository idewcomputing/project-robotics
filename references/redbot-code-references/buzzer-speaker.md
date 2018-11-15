# Buzzer \(Speaker\)

The RedBot kit includes a "buzzer" — a small speaker that can produce simple sounds. The buzzer can only play one tone \(sound\) at a time, but you can create different sounds or sound patterns. You could even program it to play simple music by playing one note at a time.

Sounds produced by the buzzer could be useful as feedback or information to people interacting with your RedBot device.

### How to Use the Buzzer in a Program:

To produce sounds with the buzzer, you will need to: 1. Declare a variable to store the buzzer pin number 2. Set the pin mode for the buzzer 3. Use the `tone()`, `delay()`, and `noTone()` functions to produce a sound and then stop it

**NOTE:** The SparkFun RedBot library does not have a built-in class for the buzzer.

### Coding References in this Section:

* Declare Variable for Buzzer Pin Number
* Set Pin Mode for Buzzer
* Produce Sound
* Add Delay Before Stopping Sound
* Stop Sound
* Produce Different Sound Patterns
* Play Song Note by Note

## Declare Variable for Buzzer Pin Number

Before your `setup()` function, declare a variable to store the buzzer pin number:

```cpp
const int buzzer = 9;
```

* `const` indicates that the variable will be a constant, which means its value won't change during the program.
* `int` indicates the variable type, which is an **integer** in this case. All Arduino pins are treated as integers \(even analog pins that have a letter in their pin number\).
* `buzzer` represents the name of the variable that stores the buzzer's pin number. If desired, you could use a different variable name.
* `9` is the pin number that the RedBot buzzer is normally plugged into.

## Set Pin Mode for Buzzer

Before your program can control the buzzer, you must set its pin mode \(so the Arduino program knows whether the part connected to the pin is an input or output\).

Within your `setup()` function, use the `pinMode()` function to set the pin mode for the buzzer pin:

```cpp
pinMode(buzzer, OUTPUT);
```

* `buzzer` represents the variable that stores the buzzer's pin number. If necessary, change this to the variable name you used for your buzzer pin. \(You could list the pin number directly, instead of listing a variable that stores the number. However, your program will be easier to read and understand if you use a variable.\)
* `OUTPUT` indicates that the buzzer pin will be used for output \(instead of input\).

## Produce Sound

To produce a sound, use the `tone()` function:

```cpp
tone(buzzer, frequency);
```

* `buzzer` represents the variable that stores the buzzer's pin number. If necessary, change this to the variable name you used for your buzzer pin.
* `frequency` represents the frequency \(in Hertz\) of the sound. The frequency should be an integer value. Lower values \(lower frequencies\) have a lower pitch, while higher values \(higher frequencies\) have a higher pitch.

To produce sounds that most people can easily hear, use a frequency value between 50 and 8000. Try using a value of 3000, and then decide whether you want the sound to have a higher or lower pitch.

**NOTE:** Once this command is performed, the buzzer will keep playing the sound. A separate command has to be used to stop the sound.

## Add Delay Before Stopping Sound

The `delay()` function can be used to add a waiting period \(in milliseconds\) before stopping the sound:

```cpp
delay(time);
```

* `time` represents the amount of time \(in milliseconds\) that the program should wait before performing the next command in the code. List the number of milliseconds for your delay \(1000 ms = 1 second\).

Sounds will typically only need to play for a fraction of a second, so you'll typically use a delay value less than 1000 for sounds.

## Stop Sound

To stop the sound, use the `noTone()` function:

```cpp
noTone(buzzer);
```

* `buzzer` represents the variable that stores the buzzer's pin number. If necessary, change this to the variable name you used for your buzzer pin.

The `noTone()` function is typically used after using the `delay()` function to allow the sound to play for a certain amount of time.

## Produce Different Sound Patterns

You can combine `tone()`, `delay()`, and `noTone()` functions to make the buzzer produce different sounds or sound patterns.

For example, to produce a brief "beep" sound, you would use the `tone()`, `delay()`, and `noTone()` functions in order:

```cpp
tone(buzzer, 3000); // turn on sound
delay(200); // wait 0.2 seconds
noTone(buzzer); // turn off sound
```

You can modify your code to make the buzzer produce different sound patterns, which might be useful as audio feedback:

* You can change the frequency value used in the `tone()` function to modify the pitch of the sound.
* You can change the `delay()` value to modify how long the sound stays on \(and how long it pauses between sounds\).
* You can use multiple sets of commands — or a `for()` loop that runs a set of commands multiple times — to make the buzzer "beep" a certain number of times in a row.

For example, the buzzer could be used to provide feedback when a person presses the built-in push button on the RedBot mainboard:

```cpp
if (button.read() == true) {
    // single-beep
    tone(buzzer, 3000);
    delay(200);
    noTone(buzzer);

    // add other code to perform when button pushed

}
```

As another example, you can use a `for` loop to make the buzzer beep three times rapidly:

```cpp
// triple-beep
for (int i=0; i < 3; i++) {
    tone(buzzer, 4000);
    delay(100);
    noTone(buzzer);
    delay(100); // pause before next beep
}
```

In fact, it would help to create your own custom functions for particular sounds that you use more than once in your program.

### alertSound\(\) function

For example, you could create a custom function named `alertSound()`:

```cpp
void alertSound() {
    // modify code to play whatever sound pattern you want
    for (int i=0; i < 3; i++) {
        tone(buzzer, 4000);
        delay(100);
        noTone(buzzer);
        delay(100); // pause before next beep
    }
}
```

Then anytime you want to play this particular sound in your program, you can run this custom function simply by "calling" its name:

```cpp
alertSound();
```

**TIP:** You can modify the code inside `alertSound()` to play whatever type of sound you want. The code shown above is simply an example. The instructions at the beginning of this section explain how you can modify the code to produce different types of sounds.

**NOTE:** You can create multiple functions that each play a different type of sound. Just give each custom function its own unique name.

You could program your RedBot to play different sounds or sound patterns as a way to provide feedback or communicate information to people. Some questions to think about:

* When might it be useful for your device to use sound for feedback, alerts, notifications, etc.?
* What kinds of sounds or sound patterns will be most easily heard and understood by people?

## Play Song Note by Note

You can use the buzzer to play simple music by playing a song note by note. Each note corresponds to a specific frequency played for a specific duration \(such as: whole note, half note, quarter note, etc.\).

[RedBot Experiment 4.2](https://learn.sparkfun.com/tutorials/experiment-guide-for-redbot-with-shadow-chassis/experiment-4-push-to-start--making-sounds-sik) includes an example program that can play "Twinkle Twinkle Little Star" or "It's A Small World".

The example program uses a file named `notes.h` that defines the specific frequencies for each note on a piano keyboard. It also defines durations \(in milliseconds\) for a whole note, half note, quarter note, etc.

**IMPORTANT:** You will need to include a copy of the `notes.h` file in your program, similar to including a library.

The `notes.h` file should be located inside the SparkFun RedBot Library folder:  
**examples &gt; Exp4\_2\_Music &gt; notes.h**

* If necessary, [download a ZIP file of the SparkFun RedBot Library](https://cdn.sparkfun.com/assets/learn_tutorials/3/5/6/SparkFun_RedBot_Arduino_Library-V_2.1.0.zip), and then unzip it to find the file.

### How to Play Song in Program:

1. Add `notes.h` file to program as separate tab
2. Include `notes.h` file in program code using: `#include "notes.h"`
3. Add custom function named `playNote()` to play musical notes
4. Create custom function named `playSong()` that calls the `playNote()` function for each note \(or rest\) in your song
5. Play your song by calling the `playSong()` function in your `setup()` or `loop()` function

**IMPORTANT:** You will need to know the specific piano notes \(and their durations\) for the song. You'll have to find this information on your own by using sheet music or searching online.

### 1. Add `notes.h` File to Program as Separate Tab

Add the `notes.h` file as a separate tab in your current program:

* **Arduino Create Web Editor:** Click the tab with a drop-down icon, and select "Import File Into Sketch."
* **Arduino IDE Desktop Editor:** Under the “Sketch” menu, select “Add File…”

A file upload window will appear. Navigate to where the `notes.h` file is located on your computer. Select the `notes.h` file, and click the "Open" button to close the window.

The `notes.h` file should now appear in your program as a separate tab.

### 2. Include `notes.h` File in Program Code

In the code editor, click the tab that contains your main program. Then add this line of code before your `setup()` function:

```cpp
#include "notes.h"
```

### 3. Add Custom Function to Play Musical Notes

You will use a custom function named `playNote()` to play one musical note at a time. When calling the function, you include parameters for the note and its duration.

Add the `playNote()` custom function **after** your `loop()` function:

```cpp
void playNote(int note, int duration) {
    // variable names for notes and durations defined in "notes.h"
    tone(buzzer, note, duration);
    delay(duration);
}
```

Variable names for the possible notes and durations are defined in the `notes.h` file:

* Each note on a piano keyboard is defined in the file with a variable name that represents a specific frequency. For example, `noteC4` \("Middle C"\) is defined as representing a frequency of 262 Hertz.
* Durations \(whole note, half note, quarter note, etc.\) are defined in the file with variable names that represent a specific amount of time \(in milliseconds\) to play the note.  For example, `WN` represents a whole note, which is defined as 800 milliseconds \(i.e., 4 beats when each beat is 200 milliseconds\).

For example, to play a note, call the `playNote()` function by passing in variable names for the specific note and its duration:

```cpp
playNote(noteC4, WN);
```

### 4. Create Custom Function to Play Song Note by Note

To play a song, you play each note in order, one at a time, by calling the `playNote()` function separately for each note \(or rest\) in the song.

You should create a custom function that contains all the `playNote()` statements for your song.

Add your `playSong()` custom function **after** your `loop()` function:

```cpp
void playSong() {
    // add code to play each note of song in order using playNote()

}
```

So in order to play a specific song, you'll have to find out how it would be played on a piano: i.e., what are the specific notes \(in order\) and their durations \(whole note, half note, etc.\).

Then you'll have to use the `notes.h` file to determine what variable names to list for the note and its duration when calling the `playNote()` function for each note.

### 5. Call Custom Function to Play Song

You can play your song by calling the `playSong()` function inside your `setup()` or `loop()` function:

```cpp
playSong();
```

If you want to play the song faster or slower, you can change the value for the `beatLength` defined in the `notes.h` file. By default, `beatLength` has been set to 200 milliseconds. For example, if the song should be played slightly faster, try a lower value such as 150.

### Example Program — Do You Recognize This Song?

For example, here's a program that will play a song that you might recognize:

```cpp
#include "notes.h"

const int buzzer = 9;
const int button = 12;

void setup() {
    pinMode(buzzer, OUTPUT);
    pinMode(button, INPUT_PULLUP);
}

void loop() {
    // when button pushed, play song
    if (digitalRead(button) == LOW) {
        playSong();
    }
}

// custom functions

void playNote(int note, int duration) {
    // variable names for notes and durations defined in "notes.h"
    tone(buzzer, note, duration);
    delay(duration);
}

void playSong() {
    // play each note of song in order using playNote()
    // Do you recognize this song?
    playNote(noteC4, QN);
    playNote(noteD4, QN);
    playNote(noteF4, QN);
    playNote(noteD4, QN);
    playNote(noteA4, QN);
    playNote(Rest, QN);
    playNote(noteA4, WN);
    playNote(noteG4, WN);
    playNote(Rest, HN);
    playNote(noteC4, QN);
    playNote(noteD4, QN);
    playNote(noteF4, QN);
    playNote(noteD4, QN);
    playNote(noteG4, QN);
    playNote(Rest, QN);
    playNote(noteG4, WN);
    playNote(noteF4, WN);
    playNote(Rest, HN);
}
```

Upload this example program to your RedBot, and push the D12 button on the mainboard to play the song. [Do you recognize the song?](https://www.youtube.com/watch?v=dQw4w9WgXcQ)

To speed up this particular example song to better match the beat of the original song, click the tab for the `notes.h` file, and change the value defined for `beatLength` from its default of `200` to `125` instead. Then re-upload the program to your RedBot, and test it.

