---
title: Introduction to Finite State Machines (FSM) Design
subtitle: Lab 4, ESDM
documentclass: scrartcl
fontsize: 12pt
---

# Objective

Using the Stateflow tool in Simulink to model a simple Finite State Machine.


# Theoretical aspects

TBD. See the Lectures.

# Design Patterns

* Detecting a transition:
    * Detecting a transition on a boolean signal can be done via a Logical Operator checking:
        * the current value of the signal
        * the previous value of the signal (delay the signal with a Unit Delay block)

# Exercises

1. Load the DC Motor Simulink model file that you created at the last lab.
	Alternatively, load the Simulink model file `Lab4_Start.slx`, provided in the current lab.

2. Add a "Chart" block in the Simulink model, open it, and design a Finite State Machine to fulfill 
the following requirements:
	
    1. Initially the motor is stopped and remains stopped
	2. The motor shall be started when the input `StartMotor` transitions to TRUE
    3. The motor shall be stopped when the input `StartMotor` transitions to FALSE
    4. Constant values to not affect the operation of the motor, only the transitions shall be used for start/stop.
	4. A hard-stop condition of the motor shall be detected and the motor shall be stopped immediately.
	5. When hard-stop is detected, the motor supply is shut down
	6. The motor remains stopped until another pulse on the `StartMotor` input arrives
    7. The model shall provide the boolean output `MotorStatus` indicating the current status of the motor, at all times.

3. Set a breakpoint in the chart and read the value of the current and the speed at the moment a hard-stop is detected.

4. Move all the output actions in the chart in the states / on the transitions.

5. Update the previous design with the following requirement:
	* After a hard stop, a motor shall not be started until at least 1 second has passed.
    Any `StartMotor` transition during this time shall be ignored.