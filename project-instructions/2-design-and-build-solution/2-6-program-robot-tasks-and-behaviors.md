# 2-6 Program Robot Tasks and Behaviors

## Objectives

* Program your robot to perform the necessary tasks and behaviors to demonstrate your testing scenarios.
* Use your testing environment to verify the programming of your robot’s tasks and behaviors.

## Instructions

**NOTE:** You will create one program that contains all the code to demonstrate your robot scenarios.

1. **Confirm that your pseudocode correctly describes the robot tasks and behaviors needed for your robot’s demonstration.** Use your team’s testing scenario descriptions, paper prototype, and evaluation findings to confirm your pseudocode.
   * Keep in mind that your team can simulate certain steps as long your robot can meaningfully demonstrate the core functions of the scenarios. For example, a team member could act as a "robotic arm" to pick up objects, as long as your robot performs the other necessary actions.
   * Make any necessary revisions to your pseudocode. Have another team member confirm that the steps described in the pseudocode match the scenarios for your team's demonstration.
   * Create a new Arduino program. Refer to this [Program Template](../../references/redbot-code-references/program-template.md) to copy-and-paste the basic "building blocks" \(in order\) to start your program. Then add your pseudocode for each scenario as [comments](https://www.arduino.cc/reference/en/language/structure/further-syntax/singlelinecomment/) within the custom function for the scenario: `scenario1()`, `scenario2()`, and `scenario3()`. Eventually, you can delete some or all of your pseudocode if it is no longer needed to clarify your program code.
2. **Confirm which robotic components \(motors, sensors, etc.\) will be used in your program.** Use your team's hardware specifications to confirm the components.
   * Create any necessary global variables or objects for the motors, sensors, etc. Refer to the [RedBot Code References](../../references/redbot-code-references/) for each component being used.
   * Certain components \(e.g., LED, buzzer, ultrasonic sensor, etc.\) require code in the `setup()` function to set their pin modes.
3. **Decide how your robot will navigate within your testing environment, and then determine what custom functions will be used in your program.** Refer to this section about different [robot navigation methods](../../references/redbot-code-references/navigation-methods.md), which includes links to example programs showing how each navigation works. In addition, the [RedBot Code References](../../references/redbot-code-references/) has "Quick Links" to pre-built custom functions for driving, turning, detecting lines, detecting objects, etc. These custom functions can be added to your program after the `loop()` function.
   * **Some of these functions require you to add missing code.** For example, the `checkBumpers()` function can detect collisions but needs code added to describe what actions to perform when a collision occurs.
   * **Some of these functions may need you to adjust the values of certain local variables.** For example, the `followLine()` function has a local variable named `lineThreshold` whose value may need to be tested and adjusted.
   * **Some of these functions can be modified to better match the specific tasks and behaviors you need for your robot demonstration.** For example, the `avoidCollision()` function can be modified to better match the behavior your robot needs to perform in your scenarios.
   * **You can also create your own custom functions to perform specific tasks or behaviors.** For example, you could create a custom function named `alertSound()` that contains code to produce a double-beep sound.
4. **Code your program in steps, and use your team's testing environment to periodically test and verify your program.** Your team will most likely find it necessary to modify your robot's program and/or your testing environment, in order for the robot to successfully complete its tasks and perform its behaviors.
   * It may be helpful to have your robot produce distinct sounds as feedback when certain events or conditions occur in your demonstration.
   * It is recommended to code your program so your robot will demonstrate different tasks or scenarios in response to button inputs. This will give your team more control over the pace and sequence of the demonstration. \(The example programs show a way to accomplish this.\)
5. **Record a video showing your robot performing the necessary tasks and behaviors in your testing environment to demonstrate your scenarios.**
   * If necessary, have a team member perform any simulated steps during the demonstration.
   * If necessary, edit the video, and add any necessary captions or narration.

## ✓ Standard Deliverables

Share your Arduino program code \(`.ino` file\) and your robot demo video with your teacher.

## ✓+ Advanced Deliverables

Write and practice a narration for the robot demonstration to help explain it to an audience and make it more compelling. The narration should introduce each scenario and explain what the robot is doing. Be sure the narration is clear, concise, and engaging. Add the narration to your robot demo video.

