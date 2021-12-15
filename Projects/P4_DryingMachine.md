---
title: Drying Machine
subtitle: Project 6, ESDM
documentclass: scrartcl
fontsize: 12pt
---

# Short description

1. Create and test Simulink model with a state machine implementing the behavior of a drying machine.

2. Write a small report on the project:
   a. briefly describe the overall design you chose (states, transitions etc).
   b. put screenshots from the tests, to prove the tests work
   
![Drying Machine](img/DryingMachine.png){.id width=40%}


# Requirements

1. The drying machine has 3 programs

   1. Wearing:
       - dry for 2 hours
   2. Storage:
       - dry for 1.5 hours
   3. Quick:
       - dry for 1 hour
       
2. The Simulink model has the following inputs and outputs:
    
    Inputs:
    - ProgramSelection (number, 0 to 3)
        - 0 = no program selected
        - 1/2/3 = one of the three programs
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
        - 2 = WATER_FULL
        - 3 = FILTER_FULL 
        - 4 = HEATER_FAULT

3. Each drying program consists of the following steps:

   - rotate the drum by activating the rotating motor (output Rotate = 1 or -1)
   - fan running continuously (output ActivateFan = True)
   - the heater is activated continuously (output HeatFan = True)
   - every 3 minutes, stop rotating for 5 seconds and change rotation direction

4. Fault detection:

    - if Water Level reaches 90 (the water collector is full) stop and set status to WATER FULL
        - do not start until Water Level is below 10
        - afterwards, continue from when the program was paused
        
    - if AirFlow drops below 30, the filter is clogged. Stop and set status to FILTER_FULL 
        - after this the program is fully terminated (next time start all over again)

    - if AirTemperature drops below 50 degrees, stop and set status to HEATER_FAULT
        - in this case the program is fully terminated (next time start all over again)
        - AirTemperature should  not be checked in the first 2 minutes after the start of a program, to allow it to reach the desired temperature

5. If the ProgramSelection input becomes 0 during an ongoing program, then terminate the ongoing program.

5. If the ProgramSelection input changes to a different program during an ongoing program, then terminate the ongoing program, and
then start again with the new program.

5. Use parameters from Matlab whenever for all values you consider necessary (e.g. duration of times etc.).
Our customer may want to adjust the parameters at any time.

6. Test your state machine (use one/multiple separate test models if necessary)

