---
title: Paid Drying Machine
#subtitle: Project 6, ESDM
subtitle: ESDM Project
documentclass: scrartcl
fontsize: 12pt
---

![Public Drying Machine](img/DryingMachineCoins.jpg){.id width=40%}

## General description

1. Create and test Simulink model with a state machine implementing the control logic of a public drying machine, payed for with coins.

2. Write a report on the project, containing:

   a. An overall description of the design (how it works, states, transitions etc, ).
   b. Some tests of the functionality (2-3 tests, depending on complexity, covering normal usage and some error scenario)

      For each test, indicate:

      - The test scenario: what are the inputs, what are the desired outputs
      - The test results: include screenshots from the tests, to prove the tests work

## Requirements

1. The drying machine has 3 programs

   - wearing:
       - dry for 2 hours
   - storage:
       - dry for 1.5 hours
   - quick:
       - dry for 1 hours

1. Each program costs some money:
    - wearing: 8 lei
    - storage: 6 lei
    - quick: 4 lei

1. The Simulink model has the following inputs and outputs:

    Inputs:
    - ProgramSelection (number, 0 to 3)
        - 0 = no program selected
        - 1/2/3 = one of the three programs above
    - MoneyInput (number, 0 to any)
    - Cancel button
    - WaterLevel (real number, 0 to 100=MAX)
    - AirFlow (number, 0 to 100=MAX)
    - AirTemperature (number, 0 to 100 degrees)

    Outputs:
    - ReturnMoney (number, 0 to any): returns to the user a certain amount of money
    - ActivateFan (boolean): when TRUE, fan is started
    - Rotate(number, -1 / 0 /1): control the rotating motor:
        - 0 = stop
        - 1 = rotate clockwise
        - $-1$ = rotate counterclockwise
    - HeatAir (boolean): when TRUE, the air heater is activated

    - Machine Status (integer):
        - 0 = IDLE
        - 1 = WORKING
        - 2 = NOT_ENOUGH_MONEY
        - 3 = WATER FULL
        - 4 = FILTER FULL 

1. The machine is used as follows:
    - The user selects a program with the ProgramSelection input
    - The user enters some money with the MoneyInput input
    - The machine checks if the money is enough. If not enough, it sets the Status output to NOT_ENOUGH_MONEY
    - If money is sufficient, the machine returns the rest, by setting ReturnMoney to the correct values
    - Then the machine proceeds with the program

1. Each drying consists of the following steps:

   - rotate the drum by activating the rotating motor (output Rotate = 1 or -1)
   - fan running continuously (output ActivateFan = True)
   - the heater is activated continuously (output HeatFan = True)
   - every 4 minutes, stop for 5 seconds and change rotation direction

1. Error detection

    - if Water Level reaches 90, stop and set status to WATER FULL
        - the program is terminated, next time start all over again

    - if AirFlow drops below 30, stop and set status to FILTER FULL 
        - the program is terminated, next time start all over again

1. If the ProgramSelection input becomes 0 during an ongoing program, then terminate the ongoing program.

1. The ProgramSelection input is not allowed to change to a different program during an ongoing program (i.e. you don't need to consider the case when ProgramSelection changes from 1 directly to 2 or 3)

1. Use parameters from Matlab whenever for all values you consider necessary (e.g. duration of times etc.).
Our customer may want to adjust the parameters at any time.

1. Test your state machine (use one/multiple separate test models if necessary)
