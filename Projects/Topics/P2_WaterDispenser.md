---
title: Water Dispenser
#subtitle: Project 5, ESDM
subtitle: ESDM Project
documentclass: scrartcl
fontsize: 12pt
---

![Water Dispenser](img/WaterDispenser.jpg){.id height=40%}

## General description

1. Create and test Simulink model containing a state machine implementing the control logic of a water dispenser ("La fântâna").

2. Write a report on the project, containing:

   a. An overall description of the design (how it works, states, transitions etc, ).
   b. Some tests of the functionality (2-3 tests, depending on complexity, covering normal usage and some error scenario)

      For each test, indicate:

      - The test scenario: what are the inputs, what are the desired outputs
      - The test results: include screenshots from the tests, to prove the tests work

## Requirements

1. The water dispenser can output cold water or hot water. The hot water is heated on the spot (somehow).

1. The Simulink model has the following inputs and outputs:

    Inputs:
    - Water button (boolean)
    - HotWater button (boolean)
    - SelfTest button (boolean)
    - Water level sensor (number, 0 to 1000 ml)
    - Water temperature sensor (number, 0 to 100 degrees Celsius)

    Outputs:
    - Activate Water Heater (boolean)
    - Activate Water Pouring (boolean)
    - Machine Status (integer):
        - 0 = IDLE
        - 1 = WORKING
        - 2 = NO_WATER
        - 3 = HEATER_FAULT
        - 4 = POURING_FAULT

1. The process is as follows:
   - When pouring normal water:
       - Start pouring water when `Water=TRUE` (i.e. user presses button)
       - Stop when `Water=FALSE`
   - When pouring hot water:
       - When `HowWater=TRUE` (i.e. user presses button), activate the water heater and wait for 500 milliseconds. Don't pour any water yet.
       - Only afterwards start pouring water
       - Stop when `HotWater=FALSE`

1. All buttons must be debounced both ways, with a time duration of 0.2 seconds.

1. There is a separate self-test mode, activated via the SelfTest button. The procedure is as follows:
    - Start heating water. If the temperature doesn't reach 99 degrees in 20 seconds, there is a heater error. The error must be signalled by setting Status = HEATER FAULT for at least 10 seconds.
    - Start pouring water. If the water level doesn't drop by 50ml in 2 seconds, the pouring mechanism is blocked (i.e. limestone). The error must be signalled by setting Status = POURING FAULT for at least 10 seconds.

1. Use parameters from Matlab for all values you consider necessary (e.g. duration of times etc.).
Our customer may want to adjust the parameters at any time.

1. Test your state machine (use one/multiple separate test models if necessary)
