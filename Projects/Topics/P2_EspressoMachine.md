---
title: Espresso Machine
#subtitle: Project 2, ESDM
subtitle: ESDM Project
documentclass: scrartcl
fontsize: 12pt
---

![Espresso Machine](img/EspressoMachine.jpg){.id width=40%}

## General description

1. Create and test Simulink model containing a state machine implementing the control logic of an espresso coffee machine.

2. Write a report on the project, containing:

   a. An overall description of the design (how it works, states, transitions etc, ).
   b. Some tests of the functionality (2-3 tests, depending on complexity, covering normal usage and some error scenario)

      For each test, indicate:

      - The test scenario: what are the inputs, what are the desired outputs
      - The test results: include screenshots from the tests, to prove the tests work

## Requirements

1. The coffee machine can produce 3 beverages:
   - normal coffee
   - long coffee
   - hot water (for tea)

1. The Simulink model has the following inputs and outputs:

    Inputs:
    - Normal Coffee button (boolean)
    - Long Coffee button (boolean)
    - Hot water button (boolean)
    - Cancel button
    - Water level sensor (number, 0 to 1000 ml)
    - Coffee level sensor (number, 0 to 1000 g)
    - Water temperature sensor (number, 0 to 100 degrees Celsius)

    Outputs:
    - Activate Coffee Grinder (boolean)
    - Activate Water Heater (boolean)
    - Activate Water Pouring (boolean)
    - Machine Status (integer):
        - 0 = IDLE
        - 1 = WORKING
        - 2 = NO WATER
        - 3 = NO COFFEE
        - 4 = HEATER FAULT
        - 5 = GRINDER FAULT
        - 6 = POURING FAULT

1. The beverages have the following recipes:
   - Normal coffee:
       - Start coffee grinder for 2 seconds
       - Heat water until 98 degrees is reached
       - Start pouring water
       - Pour until water level drops by 50 ml
   - Long coffee:
       - Start coffee grinder for 2 seconds
       - Heat water until 98 degrees is reached
       - Start pouring water
       - Pour until water level drops by 100 ml
   - Hot water for tea:
       - Heat water until 90 degrees is reached
       - Start pouring water until water level drops by 150 ml

1. The `Cancel` button stops every ongoing operation of the machine

1. The `Cancel` input button shall be debounced both ways, with a time duration of 0.3 seconds.

1. Fault control:
    - Before making anything, check if you have enough water. If water is not enough, signal via Status output
    - Coffee can't be done if coffee level is < 10g. In this case, signal via Status output
    - Hot water can be done even if there is no coffee

1. Use parameters from Matlab for all values you consider necessary (e.g. duration of times etc.).
Our customer may want to adjust the parameters at any time.

1. Test your state machine (use one/multiple separate test models if necessary)
