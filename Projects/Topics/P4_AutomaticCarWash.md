---
title: Automatic Car Wash controller
#subtitle: Project 4, ESDM
subtitle: ESDM Project
documentclass: scrartcl
fontsize: 12pt
---

![Automatic Car Wash](img/AutomaticCarWash.jpg){.id height=40%}

## General description

1. Create and test Simulink model with a state machine implementing the control logic behind a drive-through automatic Car Wash.

2. Write a report on the project, containing:

   a. An overall description of the design (how it works, states, transitions etc, ).
   b. Some tests of the functionality (2-3 tests, depending on complexity, covering normal usage and some error scenario)

      For each test, indicate:

      - The test scenario: what are the inputs, what are the desired outputs
      - The test results: include screenshots from the tests, to prove the tests work

## Requirements

1. The automatic car wash has 3 programs:
   - quick wash:
       - spray foam for 1 minutes
       - wait another 1 minute
       - optionally brush for 1 minute
       - rinse for 2 minutes
   - normal wash
       - spray foam for 1 minutes
       - wait another 3 minutes
       - optionally brush for 2 minute
       - rinse for 4 minutes
   - hard wash
       - spray foam for 2 minutes
       - wait another 10 minutes
       - optionally brush for 5 minute
       - rinse for 10 minutes

1. The Simulink model has the following inputs and outputs:

    Inputs:
    - ProgramSelection (number, 0 to 3)
        - 0 = no program selected
        - 1/2/3 = the three programs above
    - BrushOption (boolean): if TRUE, brushing is done. If not, the brushing is replaced by waiting for the same amount of time.
    - WaterLevel (real number, 0 to 2000 liters): amount of water in the reservoir
    - FoamLevel (real number, 0 to 50 liters): amount of foam in the reservoir

    Outputs:
    - ActivateWaterPump (boolean): when TRUE, water is poured
    - ActivateFoamPump (boolean): when TRUE, foam is sprayed
    - ActivateBrushMotors (boolean): when TRUE, the brushes are activated

    - Machine Status (integer):
        - 0 = IDLE
        - 1 = FOAMING
        - 2 = WAITING
        - 3 = BRUSHING
        - 4 = RINSING
        - 5 = ERROR

1. No program is allowed to start if there is less then 100 liters of water available, or less then 3 liter of Foam. In this case set the output status to ERROR.

1. If the ProgramSelection input becomes 0 during an ongoing program, then stop the ongoing program and stop

1. If the ProgramSelection input changes to a different program during an ongoing program, then stop the ongoing program and set the output status ERROR.
   Keep this status until ProgramSelection input becomes 0.

1. Error Control:

    - If foam level does not decrease by at least 2 liters after the foaming stage, there is an error. Stop the program and set the output status ERROR.
    - If water level does not decrease by at least 20 liters after the washing phase, there is an error. Stop the program and set the output status ERROR.

1. Use parameters from Matlab whenever for all values you consider necessary (e.g. duration of times etc.).
Our customer may want to adjust the parameters at any time.

1. Test your state machine (use one/multiple separate test models if necessary)
