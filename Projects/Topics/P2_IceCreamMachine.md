---
title: Ice Cream Machine
#subtitle: Project 2, ESDM
subtitle: ESDM Project
documentclass: scrartcl
fontsize: 12pt
---

![Ice cream Machine](img/StreetIceCreamMachine.jpg){.id height=30%}

## General description

1. Create and test Simulink model containing a state machine implementing the control logic of an street ice cream machine.

2. Write a report on the project, containing:

   a. An overall description of the design (how it works, states, transitions etc, ).
   b. Some tests of the functionality (2-3 tests, depending on complexity, covering normal usage and some error scenario)

      For each test, indicate:

      - The test scenario: what are the inputs, what are the desired outputs
      - The test results: include screenshots from the tests, to prove the tests work

## Requirements

1. The ice cream machine can pour 3 types of ice cream:
   - chocolate ice cream
   - vanilla ice cream
   - mixed chocolate + vanilla ice cream

1. The Simulink model has the following inputs and outputs:

    Inputs:
    - ChocolateLever (boolean): when TRUE, chocolate ice cream must be poured
    - VanillaLever: (boolean): when TRUE, vanilla ice cream must be poured
    - MixedLever (boolean): when ON, mixed ice cream must be poured
    - Chocolate ice cream level sensor (number, 0 to 10000 ml): how much chocolate ice cream is available in the reservoir
    - Vanilla ice cream level sensor (number, 0 to 10000 ml): how much vanilla ice cream is available in the reservoir
    - Ice cream temperature sensor (number, -20 to 20 degrees Celsius)
    - Lid opened (boolean): when TRUE, the reservoir lid is open

    Outputs:
    - PourChocoIceCream:   number 0 to 100, indicating the speed of pouring chocolate ice cream
    - PourVanillaIceCream: number 0 to 100, indicating the speed of pouring vanilla ice cream
    - Machine Status (integer):
        - 0 = IDLE
        - 1 = POURING
        - 2 = FREEZER_FAULT
        - 3 = POUR_FAULT
        - 4 = INPUT_FAULT
        - 5 = LID_OPEN
    - NoChocolateIceCream: boolean error flag. Should be set to TRUE when there is not enough chocolate ice cream in the reservoir
    - NoVanillaIceCream: boolean error flag. Should be set to TRUE when there is not enough vanilla ice cream in the reservoir

1. The normal functioning of the machine is as follows:
   - Chocolate ice cream
       - When ChocolateLever is TRUE, 200 ml of chocolate ice cream must be poured at speed 50
       - Pouring is activated by setting the output PourChocoIceCream to 50
       - Pouring should go on on until the Chocolate level sensor drops by 200
       - If this doesn't happen in 10 seconds, the pouring is blocked. In this case the pouring is cancelled and POUR_FAULT output status should be set.
   - Vanilla ice cream
       - Similar to above
   - Mixed ice cream:
       - Pour both chocolate and vanilla ice cream with speed 25, until both input sensor values decrease with at least 100
       - If any one of them doesn't drop by 100ml in 10 seconds,  the pouring is blocked, and POUR_FAULT should be set.

1. The ChocolateLever input should shall be debounced both ways, with a time duration of 0.5 seconds.

1. When the reservoir lid is open, no pouring is allowed, and the Status output shall be set to LID_OPEN. If lid is opened during a pouring operation, the operation should be terminated immediately.

1. Fault control:
    - Before making anything, check if there is at least 300ml of the necessary ice cream (or 150ml of both, for mixed ice cream). If this is not true, ice cream is not allowed, and NoChocolateIceCream and/or NoVanillaIceCream outputs shall be set to TRUE. If the ice cream is available, they should be set to FALSE.
    - Before making anything, check if ice cream temperature is below 0. If this is not true, ice cream is not allowed, and the Status output
    shall be set to FREEZER_FAULT.
    - The three inputs ChocolateLever, VanillaLever and MixedLever should never be active at the same time. The system shall detect if two or three or them are simultaneously active, and in this case it shall set the Status output to INPUT_FAULT and disallow any operation.

1. Use parameters from Matlab for all values you consider necessary (e.g. duration of times etc.).
Our customer may want to adjust the parameters at any time.

1. Test your state machine (use one/multiple separate test models if necessary)
