---
title: Extended Finite State Machines (EFSM)
subtitle: Lab 5, ESDM
documentclass: scrartcl
fontsize: 12pt
---

# Objective

Using the Stateflow tool in Simulink to model an extended Finite State Machine, 
that implements a complex motor control logic.

# Theoretical aspects

TBD. See the Lectures.

New things in this lab:

- Hierarchical states
- Time-based conditions
- OR (exclusive) / AND (parallel) decompositions

# Exercises

1. Load the DC Motor Simulink model file that you created at the last lab.
	Alternatively, load the Simulink model file `Lab5_Start.slx`, provided in the current lab.

2. Add/Open a "Chart" block in the Simulink model, and design a Finite State Machine to fulfill 
the following requirements:
	
  1. The motor shall be started when the input `StartMotor` transitions to TRUE
  2. Upon starting, the motor speed shall increase linearly from 0 to **CP_MaxSpeed** during an interval of **CP_RampUpTime**
  3. Once the motor has reached **CP_MaxSpeed**, it shall hold this speed until a stop request is received
  4. A stop request is received when the input `StartMotor` transitions to FALSE
  5. Upon receiving a stop request, the motor speed shall decrease linearly from **CP_MaxSpeed** to 0 during an interval of **CP_RampDownTime**
  6. A hard-stop condition of the motor shall be detected, and in this case the motor shall be stopped immediately, without and ramping down of speed 
  7. The model shall provide the boolean output `MotorStatus` indicating the current status of the motor, at all times. `MotorStatus` shall be set to TRUE when motor is started, and shall be set to FALSE after a delay **CP_SafeOffTime** after becomes 0.

3. Test your state machine and show that is works properly. In particular, check 2 different values for each parameter, and see that the outputs react properly.

4. Implement a parallel state for checking motor errors:

	- Open-load in ON state: When the motor is running, if motor speed becomes 0 and motor current is below **CP_OpenLoadDebounceTime**, the model shall set the output flag **MotorError_OpenLoad** to TRUE
	- If an open-load error is detected, the motor shall be stopped immediately, without and ramping down of speed
	- The **MotorError_OpenLoad** output flag shall be reset to FALSE after expiration of the **CP_SafeOffTime** delay
	
5. Update the previous design with the following requirement:
	* After a hard stop, a motor shall not be started until at least 1 second has passed.
    Any `StartMotor` transition during this time shall be ignored.
