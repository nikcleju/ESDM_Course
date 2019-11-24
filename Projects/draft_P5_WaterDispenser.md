---
title: Water Dispenser
subtitle: Project 5, ESDM
documentclass: scrartcl
fontsize: 12pt
---

# Short description

1. Create and test Simulink model with a state machine implementing the behavior of a water dispenser ("La fantana").

2. Write a small report on the project:
   a. briefly describe the overall design you chose (states, transitions etc).
   b. put screenshots from the tests, to prove the tests work
   

# Requirements

1. The water dispenser can output cold water or hot water

2. The Simulink model has the following inputs and outputs:
    
    Inputs:
    - Long Coffee button (boolean)
    - Hot water button (boolean)
    - Self-test button (boolean)
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

3. The beverages have the following recipes:
   - Normal coffee: 
       - Heat water until 98 degrees, at the same time start coffee grinder for 2 seconds
       - When both have finished, start pouring water
       - Pour until water level drops by 50 ml
   - Long coffee: 
       - Heat water until 98 degrees, at the same time start coffee grinder for 2 seconds
       - When both have finished, start pouring water
       - Pour until water level drops by 100 ml
   - Hot water for tea: 
       - Heat water until 90 degrees
       - Start pouring water until water level drops by 150 ml

4. The cancel button stops every ongoing operation of the machine

4. Fault control:
    - Before making anything, check if you have enough water. If water is not enough, signal via Status output
    - Coffee can't be done if coffee level is < 10g. In this case, signal via Status output
    - Hot water can be done even if there is no coffee
    
5. There is also a self-test mode, activated via the Self-test button. The procedure is as follows:
    - Start heating water. If the temperature doesn't reach 99 degrees in 20 seconds, there is a heater error
    - Start grinding coffee. If the coffee level doesn't drop by 5 grams in 20 seconds, the grinder motor has a fault
    - Start pouring water. If the coffee level doesn't drop by 20ml in 5 seconds, the pouring mechanism is blocked (i.e. limestone)

5. Use parameters from Matlab for all values you deem necessary (e.g. duration of times etc.).
Our customer may want to adjust the parameters at any time.

6. Test as many behaviors of your state machine as possible (use one/multiple separate test models if necessary)
