---
title: Juice Machine
#subtitle: Project 2, ESDM
subtitle: ESDM Project
documentclass: scrartcl
fontsize: 12pt
---

![Juice Machine](img/JuiceMachine.jpg){.id width=40%}

## General description

1. Create and test Simulink model containing a state machine implementing the control logic of a milkshake machine.

2. Write a report on the project, containing:

   a. An overall description of the design (how it works, states, transitions etc, ).
   b. Some tests of the functionality (2-3 tests, depending on complexity, covering normal usage and some error scenario)

      For each test, indicate:

      - The test scenario: what are the inputs, what are the desired outputs
      - The test results: include screenshots from the tests, to prove the tests work

## Requirements

1. The juice machine can produce 3 beverages:
   - orange juice
   - strawberry juice
   - orange + strawberry juice

    The beverages can add ice cubes to the beverages.

1. The Simulink model has the following inputs and outputs:

    Inputs:
    - OrangeJuice button (boolean)
    - StrawBerryJuice button (boolean)
    - OrangeStrawberryJuice button (boolean)
    - AddIce (boolean)
    - Cancel button
    - OrangeJuice level sensor (number, 0 to 1000 ml)
    - StrawberryJuice level sensor (number, 0 to 1000 ml)
    - Ice Temperature sensor (number, -20 to 20 degrees Celsius)

    Outputs:
    - PourOrangeJuice (boolean): start/stop pouring orange juice
    - PourStrawberryJuice (boolean): start/stop pouring strawberry juice
    - DropIce (boolean): when transitioning from False to True, an ice cube is dropped
    - Machine Status (integer):
        - 0 = IDLE
        - 1 = WORKING
        - 2 = NO_ORANGE_JUICE
        - 3 = NO_STRAWBERRY_JUICE
        - 4 = FREEZER_FAULT
        - 5 = POURING_FAULT

1. The beverages have the following recipes:
   - Orange Juice:
       - Once activated, pour orange juice until level drops by 250 ml
   - Strawberry Juice:
       - Once activated, pour strawberry juice until drops by 250 ml
   - OrangeStrawberry Juice:
       - Once activated, pour both orange and strawberry juice at the same time, until each juice level drops by 125 ml

1. After the juice is poured, the user has the option to select Ice or not. The machine waits 5 seconds for the user to press
   the Ice button. If the user presses the button during this time, ice is added to the beverage. If not, the machine goes on after 5 seconds
   and no ice is added.

1. The AddIce input button shall be debounced both ways, with a time duration of 0.25 seconds.

1. The cancel button stops every ongoing operation of the machine

1. Fault control:
    - Before making anything, check if you have juice for the selected beverage. If any juice is not enough for the selected beverage, signal via Status  output.
    - If any juice pouring is activated but the juice level takes more than 10 seconds to finish, that pouring is blocked. Signal this error via Status output
    - An error status remains set until the cancel button is pressed. Until then, no other operation is permitted.
    - If at any time the Ice Temperature is above 0 degrees, the freezer is broken. Signal this error via Status output. In this case the machine is not allowed to pour any juice.

1. Use parameters from Matlab for all values you consider necessary (e.g. duration of times etc.).
Our customer may want to adjust the parameters at any time.

1. Test your state machine (use one/multiple separate test models if necessary)
