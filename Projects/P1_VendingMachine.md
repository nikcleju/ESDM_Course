---
title: Vending Machine
subtitle: Project 1, ESDM
documentclass: scrartcl
fontsize: 12pt
---

# Short description

1. Create and test Simulink model with a state machine implementing the behavior of a vending machine.

2. Write a small report on the project:
   a. briefly describe the overall design you chose (states, transitions etc).
   b. put screenshots from the tests, to prove the tests work

# Requirements

1. The vending machine has 5 products available (e.g. chocolate bar, chocolate croissant, sandwich, biscuits, cola)

2. List of inputs and outputs of the model:

   Inputs:
     - ProductSelection: integer (0 to 5)
        - when 0, no product is selected
        - when non-zero, it is the code of product selected by the user
     - MoneyInput: integer
        - when 0, no money is inserted
        - when non-zero, it is the current value of the coin/note given by the customer
     - Cancel: boolean
        - when True, cancels an ongoing operation. All money input until this moment shall be returned to the customer.
     - ResetStock
        - when True, the stock for all products is set to 10 (e.g. the machine was refilled).
     
   Outputs:
     - DispenseProduct: integer (0 to 5)
        - when 0, nothing happens
        - when non-zero, the product with that code is dispensed by a mechanism
     - MoneyReturn:
        - when 0, nothing happens
        - when non-zero, the specified amount of money will be returned to the customer
     - Status: integer
        - 0 = Idle, awaiting operation
        - 1 = Operation in progress
        - 2 = Success
        - 3 = Incorrect product code
        - 4 = Product out of stock

3. The vending machine operates in 4 basic steps:
   - first you enter the product code of the product
   - then you enter the money 
   - then the product is dispensed
   - then the rest of the money is returned

2. The vending machine holds in memory the number of products it has available at any time moment, and the price of each product.

5. The machine shall detect if the user requests an invalid product code, and signal this at the Status output 

3. The machine shall detect if the user requests a product which is currently out of stock, and signal at the Status output.

4. The machine shall calculate the rest of the money and provide back the change (Note: assume the machine has an infinite supply of coins/notes).

5. After dispensing a product, the machine will wait 5 seconds before accepting any new operation (to wait until the dispensing mechanism finishes).

5. The number of products available can be reset back to the value of 10 when the input `ResetStock` is activated.

6. The machine shall always provide a status code output.

5. Use parameters from Matlab for all values you deem necessary (e.g. duration of delays, prices etc.).
Our customer may want to adjust the parameters at any time.

6. Test as many behaviors of your state machine as possible (use one/multiple separate test models if necessary)

