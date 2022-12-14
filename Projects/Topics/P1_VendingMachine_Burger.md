---
title: Vending Machine - Burger
#subtitle: Project 1, ESDM
subtitle: ESDM Project
documentclass: scrartcl
fontsize: 12pt
---

![Burger Vending Machine](img/VendingMachineBurger.jpg){.id width=40%}

## General Description

1. Create and test a Simulink model containing a state machine implementing the logic module of a vending machine.

2. Write a report on the project, containing:

   a. An overall description of the design (how it works, states, transitions etc, ).
   b. Some tests of the functionality (2-3 tests, depending on complexity, covering normal usage and some error scenario)

      For each test, indicate:

      - The test scenario: what are the inputs, what are the desired outputs
      - The test results: include screenshots from the tests, to prove the tests work

## Requirements

1. The vending machine has 3 products categories available: Normal Burger, Cheeseburger, Double Burger.

1. List of inputs and outputs of the model:

   Inputs:
     - ProductSelection: integer (0 to 3)
        - 0, no product is selected
        - 1: Normal Burger: bun + salad + meat
        - 2: Cheeseburger: bun + salad + meat + cheese
        - 3: Double Burger: bun + salad + meat + cheese + meat + cheese
     - MoneyInput: integer
        - when 0, no money is inserted
        - when non-zero, it is the current value of the coin/note given by the customer
     - Cancel: boolean
        - when True, cancels an ongoing operation. All money input until this moment shall be returned to the customer.
     - ResetStock
        - when True, the stock for all buns, sausages and veggie sausages to 10 (e.g. the machine was refilled).

   Outputs:
     - DispenseBunAndSalad: boolean
        - the transition from False to True activates the dispensing of one bread bun with salad on top of it
     - DispenseMeat: boolean
        - the transition from False to True activates the dispensing of one meat slice
     - DispenseCheese: boolean
        - the transition from False to True activates the dispensing of one cheese slice
     - MoneyReturn: integer, controls the money returned to the customer
        - when 0, nothing happens
        - when non-zero, the specified amount of money will be returned to the customer
     - Status: integer, a status message indicating the current state
        - 0 = Idle, awaiting operation
        - 1 = Operation in progress
        - 2 = Success
        - 3 = Incorrect product code
        - 4 = Product out of stock

2. The vending machine operates in 4 basic steps:
   - first you enter the product code of the product
   - then you enter the money
   - then the product is created and dispensed, according to the recipe
   - then the rest of the money is returned

3. The vending machine starts with 10 buns and salads, 10 meat slices, 10 cheese slices

4. The price of every type of product is fixed and known (you pick some value, e.g. 5).

5. The vending machine holds in memory the number of products it has available at any time moment: buns, salads, meat slices, cheese slices. Every time one is used, the number of available products decreases.

6. The machine shall detect if the user requests an invalid product code, and signal this at the Status output

7. The machine shall detect if the user requests a product which is currently out of stock, and signal at the Status output (e.g. when the machine is out of cheese, it cannot produce ca Cheeseburger or Double burger, but it can produce a normal burger).

8. The machine shall calculate the rest of the money and provide back the change (Note: assume the machine has an infinite supply of coins/notes).

9. After dispensing a product, the machine will wait 5 seconds before accepting any new operation (to wait until the dispensing mechanism finishes).

10. The number of products available can be reset back to the value of 10 when the input `ResetStock` is activated.

11. The machine shall always provide a status code output.

12. The `Cancel` input button shall be debounced both ways, with a time duration of 0.2 seconds.

13. Use parameters from Matlab for all values you consider necessary (e.g. duration of delays, prices etc.).
Our customer may want to adjust the parameters at any time.

1. Test your state machine (use one/multiple separate test models if necessary)
