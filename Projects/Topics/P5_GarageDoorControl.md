---
title: Garage door controller
#subtitle: Project 5, ESDM
subtitle: ESDM Project
documentclass: scrartcl
fontsize: 12pt
---

![Garage door control module](img/GarageDoorControl.jpg){.id height=40%}

## General description

1. Create and test Simulink model with a state machine implementing the control logic of a garage door control module (only the motor control, not the full input buttons logic).

2. Write a report on the project, containing:

   a. An overall description of the design (how it works, states, transitions etc, ).
   b. Some tests of the functionality (2-3 tests, depending on complexity, covering normal usage and some error scenario)

      For each test, indicate:

      - The test scenario: what are the inputs, what are the desired outputs
      - The test results: include screenshots from the tests, to prove the tests work

## Requirements

1. The control module implements the functionality of an automatic garage door controller.

1. The Simulink model has the following inputs and outputs:

    Inputs:

    - Command: the command received via the remote control:
      - 0: STOP (no command)
      - 1: OPEN : command to open the door
      - 2: CLOSE : command to close the door
    - EmergencyStop button (boolean): when TRUE, stops the movement instantly
    - CurrentPosition (real number between 0 and 3): the current position of the door
        - 0 = Fully open
        - inbetween: The door is partly open
        - 3 = Fully closed
    - MotorSpeed (number -100 to 100): the current motor speed, given by a speed sensor. Positive values indicate speed in the closing direction, negative values means the opening direction.
    - MotorTemp (number 0 to 150): the current motor temperature

    Outputs:

    - MotorPWM: fill factor of PWM signal to the motor
        - 0 = Motor stopped
        - 100 = Motor fully active
        - in-between = intermediate speed

    - MotorDirection: movement direction
        - 0 = move in open direction
        - 1 = move in close direction

    - Status (integer):
        - 0 = STOPPED
        - 1 = OPENING
        - 2 = CLOSING
        - 3 = MOTOR_ERROR_OR_OBSTACLE
        - 4 = OVERTEMPERATURE

1. The system operates as follows. When the OPEN command is received, the system opens the door:

    - the motor is activated in the opening direction
    - the motor PWM increases gradually from 0 to 100 in 2 seconds
    - after the first 2 seconds, the motor PWM is kept to 100
    - with 0.5 meters before the final position, the motor PWM is decreased from 100 to 10 in 2 seconds
    - the motor remains at 10 PWM until the final position is reached
    - the motor is turned off by setting PWM to 0
    - during all this time, the status output shall be set to OPENING

1. When the CLOSE command is received, the system closes the door with a similar procedure, but in the closing direction. The status shall be set to CLOSING.

1. When the STOP command is received during any movement, the motor is stopped as follows:
    - the motor PWM decreases from its current value to 0, decreasing at a rate of 100 in 2 seconds
    - when the motor PWM reaches 0, the motor is stopped, 

1. The EmergencyStop shall terminate a movement immediately: the motor PWM is set to 0 instantly.

1. The EmergencyStop shall be debounced in both directions, with a duration of 0.1 seconds.

1. Fault control:
   - if the motor is active and the absolute value of the speed becomes less than 15, for at least 200ms, something is wrong.
   The movement shall be terminated, and the status output shall be set to MOTOR_ERROR_OR_OBSTACLE.
   - if the motor is active and the temperature is higher than 100, the movement shall be terminated instantly, and the status output shall be set to OVERTEMPERATURE.

1. Use parameters from Matlab whenever for all values you consider necessary (e.g. duration of times etc.).
Our customer may want to adjust the parameters at any time.

1. Test your state machine (use one/multiple separate test models if necessary)
