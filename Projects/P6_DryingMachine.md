---
title: Drying Machine
subtitle: Project 6, ESDM
documentclass: scrartcl
fontsize: 12pt
---

# Short description

1. Create and test Simulink model with a state machine implementing the behavior of a washing machine.

2. Write a small report on the project:
   a. briefly describe the overall design you chose (states, transitions etc).
   b. put screenshots from the tests, to prove the tests work
   

# Requirements

1. The drying machine has 3 programs

   - wearing:
       - dry for 2 hours
   - storage:
       - dry for 1.5 hours
   - quick:
       - dry for 1.5 hours
       
2. The Simulink model has the following inputs and outputs:
    
    Inputs:
    - ProgramSelection (number, 0 to 3)
        - 0 = no program selected
        - 1/2/3 = the three programs above
    - Cancel button
    - WaterLevel (real number, 0 to 100=MAX)
    - AirFlow (number, 0 to 100=MAX)
    - AirTemperature (number, 0 to 100 degrees)

    Outputs:
    - ActivateFan (boolean): when TRUE, fan is started
    - Rotate(number, -1 / 0 /1): control the rotating motor:
        - 0 = stop
        - 1 = rotate clockwise
        - $-1$ = rotate counterclockwise
    - HeatAir (boolean): when TRUE, the air heater is activated
    
    - Machine Status (integer):
        - 0 = IDLE
        - 1 = WORKING
        - 2 = WATER FULL
        - 3 = FILTER FULL 
        - 4 = HEATER FAULT

3. Each drying consists of the following steps:

   - rotating the drum continuously
   - fan running continuously
   - the heater is activated continuously
   - every 3 minutes, stop for 5 seconds and change rotation direction

4. Error detection

    - if Water Level reaches 90, stop and set status to WATER FULL
        - do not start until Water Level is below 10
        - afterwards, continue from when the program was paused
        
    - if AirFlow drops below 30, stop and set status to FILTER FULL 
        - the program is terminated, next time start all over again

    - if AirTemperature drops below 50 degrees, stop and set status to HEATER FAULT
        - the program is terminated, next time start all over again
        - AirTemperature should  not be checked in the first 2 minutes after the start of a program, to allow it to reach the desired temperature

5. If the ProgramSelection input becomes 0 during an ongoing program, then terminate the ongoing program.

5. If the ProgramSelection input changes to a different program during an ongoing program, then terminate the ongoing program, and
then start again with the new program.

5. Use parameters from Matlab whenever for all values you deem necessary (e.g. duration of times etc.).
Our customer may want to adjust the parameters at any time.

6. Test as many behaviors of your state machine as possible (use one/multiple separate test models if necessary)
