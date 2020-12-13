---
title: Generic motor controller
subtitle: Project 5, ESDM
documentclass: scrartcl
fontsize: 12pt
---

# Short description

1. Create and test Simulink model with a state machine implementing a generic motor control module (simplified).

2. Write a small report on the project:
   a. briefly describe the overall design you chose (states, transitions etc).
   b. put screenshots from the tests, to prove the tests work
   
![Generic motor control module](img/GenericMotorController.jpg){.id height=40%}

# Requirements

1. The control module implements the functionality of a simple motor controller.
   
2. The Simulink model has the following inputs and outputs:
    
    Inputs:

    - Command: the command received
      - 0: STOP (no command)
      - 1: OPEN : command to run the motor in one direction
      - 2: CLOSE : command to run the motor in the opposite direction
    - EmergencyStop button (boolean): when TRUE, stops the movement instantly
    - MotorSpeed (number -200 to 2000 rpm): the current motor speed. Positive values indicate speed in the closing direction, negative values means the opening direction.
    - MotorVoltage (number 0 to 1500 mV): the current motor voltage
    - MotorCurrent (number 0 to 2000 mA): the current motor speed
        
    Outputs:
    
    - ActivateHBridge (boolean): activate the motor H-Bridge
      - FALSE: the motor is not controlled, and can spin on its own
      - TRUE: the motor is controlled and is forced to spin according to the PWM provided
      
    - MotorPWM: PWM control signal to the motor
        - 0 = Motor braked
        - 100 = Motor fully active
        - in-between = intermediate speed
        
    - MotorDirection: movement direction
        - 0 = move in open direction
        - 1 = move in close direction
        
    - Status (integer):
        - 0 = IDLE
        - 1 = OPENING
        - 2 = CLOSING
        - 3 = BRAKING
        - 4 = SHORT_CIRCUIT
        - 5 = OPEN_LOAD
        - 6 = OVER_VOLTAGE
        
4. When the OPEN command is received, the motor is commanded in the open direction, as follows:
    - set the PWM to 0 and the direction to open direction
    - activate the H-Bridge
    - wait 10 ms
    - increase the motor PWM from 0 to 100 in 2 seconds
    - afterwards, keep the motor PWM to 100
    - during all this time, the status output shall be set to OPENING
    
6. When the STOP command is received during a movement, the motor is stopped as follows:
    - the motor PWM decreases from its current value to 0, decreasing at a rate of 100 in 2 seconds
    - when the motor PWM reaches 0, wait for 10ms
    - deactivate the H-Bridge

5. When the CLOSE command is received, the motor shall  the door with a similar procedure, but in the closing direction. The status shall be set to CLOSING.
    
6. The user does not send a CLOSE command after an OPEN command. Any movement is always stopped with STOP command.

7. The EmergencyStop input shall terminate a movement immediately: 
    - the motor PWM is set to 0 instantly
    - the bridge is kept active (during this time the motor is braking)
    - the status during all this time is set to BRAKING
    - the bridge is deactivated when EmergencyStop becomes FALSE 

7. Fault control:
   - if the motor is active, and the speed becomes less than 15 in the respective direction, and the current is smaller then 100 mA, we have a Open Load error. Set the status output to OPEN_LOAD.
   - if the motor is active, and the speed becomes is higher than 300 in the respective direction, and the current is higher than 1500 mA, we have a short circuit error. Set the status output to SHORT_CIRCUIT.
   - if the motor is active, and the voltage becomes higher speed becomes is higher than 300 in the respective direction, and the current is higher than 1500 mA, we have an over voltage error. Set the status output to SHORT_CIRCUIT.

**Note:** The fault control can be implemented as a separate Stateflow Chart inside a Simulink module.
   
5. Use parameters from Matlab whenever for all values you deem necessary (e.g. duration of times etc.).
Our customer may want to adjust the parameters at any time.

6. Test as many behaviors of your state machine as possible (use one/multiple separate test models if necessary)
