---
title: Automatic Ice Cream Machine
#subtitle: Project 2, ESDM
subtitle: ESDM Project
documentclass: scrartcl
fontsize: 12pt
---

![Automatic ice cream Machine](img/StreetIceCreamMachine_Coins.jpg){.id height=30%}

## General description

1. Create and test Simulink model containing a state machine implementing the control logic of an automatic street ice cream machine, accepting payment with coins.

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

   The client pays at the machine, and the ice cream is poured automatically.

1. The Simulink model has the following inputs and outputs:

    Inputs:
    - Chocolate button (boolean): when TRUE, chocolate ice cream must be poured
    - Vanilla button (boolean): when TRUE, vanilla ice cream must be poured
    - Mixed button (boolean): when ON, mixed ice cream must be poured
    - Chocolate ice cream level sensor (number, 0 to 20000 ml): how much chocolate ice cream is available in the reservoir
    - Vanilla ice cream level sensor (number, 0 to 20000 ml): how much vanilla ice cream is available in the reservoir
    - MoneyInput (number, 0 to 100): amount of money inserted by the user
    - Cancel button (boolean): when TRUE, the current operation is cancelled

    Outputs:
    - PourChocoIceCream:   (boolean). When set to TRUE, chocolate ice cream is poured
    - PourVanillaIceCream: (boolean). When set to TRUE, vanilla ice cream is poured
    - ReturnMoney: number 0 to 100, indicates the amount of money to return (assume the machine has infinite amount of coins available)
    - DropCone: boolean. A transition from FALSE to TRUE activates the dropping of one cone, in which the ice cream will be then poured
    - Machine Status (integer):
        - 0 = IDLE
        - 1 = POURING
        - 2 = NO_ICE_CREAM
        - 3 = NO_CONES
        - 4 = NOT_ENOUGH_MONEY
        - 5 = ERROR

1. The normal functioning of the machine is as follows:
   - The user chooses an ice cream type and presses the right button
   - The user inserts the money. All ice cream types cost 5 lei.
   - The machine checks if the money is enough and returns the rest of the money
   - The machine checks if it has cones, and if true it drops one ice cream cone
   - The machine pours 150ml of the desired ice cream:

     - Chocolate ice cream:

       - The output PourChocoIceCream is activated and remains active until the chocolate input sensor drops by 150ml
       - If this doesn't happen in 7 seconds, the pouring is blocked. In this case the pouring is cancelled and ERROR output status should be set.

     - Vanilla ice cream:

       - The output PourVanillaIceCream is activated and remains active until the vanilla input sensor drops by 150ml
       - If this doesn't happen in 7 seconds, the pouring is blocked. In this case the pouring is cancelled and ERROR output status should be set.

     - Mixed ice cream:

       - Both outputs PourChocoIceCream and PourVanillaIceCream are activated, until both input sensor levels decrease with at least 75ml each.
       - If any one of them doesn't drop by 75ml in 7 seconds,  the pouring is blocked, and ERROR output status should be set.

     - While pouring, the output status shall be set to POURING.

1. If the money is not enough, the machine shall set the output status to NOT_ENOUGH_MONEY and return all the sum to the client, by setting the output ReturnMoney to the total amount.

1. The machine keeps track of the number of cones it has available. It starts with 20 cones, and at every new ice-cream it decrements the value. If at one time it has no cones, it refuses to produce an ice cream.

1. When Cancel button is activated, any operation is immediately terminated. Any new operation shall not start while the Cancel button remains active.

1. The Cancel input button should shall be debounced both ways, with a time duration of 0.3 seconds.

1. Fault control:

    - Before making anything, check if there is at least 300ml of the necessary ice cream (or 150ml of both, for mixed ice cream). If this is not true, ice cream is not allowed, and the output status shall be set to NO_ICE_CREAM.
    - Before making anything, check if the number of available cones is not 0. If there are no cones, the output status shall be set to NO_CONES.

1. Use parameters from Matlab for all values you consider necessary (e.g. duration of times etc.).
Our customer may want to adjust the parameters at any time.

1. Test your state machine (use one/multiple separate test models if necessary)
