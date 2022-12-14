---
title: Vending Machine - Snacks
#subtitle: Project 1, ESDM
subtitle: ESDM Project
documentclass: scrartcl
fontsize: 12pt
---

![Snacks Vending Machine](img/VendingMachineSnacks.png){.id width=40%}

## General Description

1. Create and test a Simulink model containing a state machine implementing the logic module of a vending machine.

2. Write a report on the project, containing:

   a. An overall description of the design (how it works, states, transitions etc, ).
   b. Some tests of the functionality (2-3 tests, depending on complexity, covering normal usage and some error scenario)

      For each test, indicate:

      - The test scenario: what are the inputs, what are the desired outputs
      - The test results: include screenshots from the tests, to prove the tests work

## Requirements

1. The vending machine has 5 products categories available: chocolate bar, chocolate croissant, sandwich, biscuits, cola.

1. List of inputs and outputs of the model:

   Inputs:
     - ProductSelection: integer (0 to 5)
        - when 0, no product is selected
        - when non-zero, it is the code of product selected by the user
     - MoneyInput: integer
        - when 0, no money is inserted
        - when non-zero, it is the current value of the money inserted by the customer
     - Cancel: boolean
        - when True, cancels an ongoing operation. All money input until this moment shall be returned to the customer.
     - ResetStock
        - when True, the stock for all products is set to 10 (e.g. the machine was refilled).

   Outputs:
     - DispenseProduct: integer (0 to 5), controls the dispensing of products
        - when 0, nothing happens
        - when non-zero, the product with that code is dispensed by a mechanism
     - MoneyReturn: integer, controls the money returned to the customer
        - when 0, nothing happens
        - when non-zero, the specified amount of money will be returned to the customer
     - Status: integer, a status message indicating the current state
        - 0 = Idle, awaiting operation
        - 1 = Operation in progress
        - 2 = Success
        - 3 = Incorrect product code
        - 4 = Product out of stock

1. The vending machine operates in 4 basic steps:
   - first you enter the product code of the product
   - then you enter the money 
   - then the product is dispensed
   - then the rest of the money is returned

1. The vending machine starts with 10 products of each of the 5 categories.

1. The price of every type of product is fixed and known (you pick some value, e.g. 7).

1. The vending machine holds in memory the number of products it has available at any time moment.

1. The machine shall detect if the user requests an invalid product code, and signal this at the Status output 

1. The machine shall detect if the user requests a product which is currently out of stock, and signal at the Status output.

1. The machine shall calculate the rest of the money and provide back the change (Note: assume the machine has an infinite supply of coins/notes).

1. After dispensing a product, the machine will wait 5 seconds before accepting any new operation (to wait until the dispensing mechanism finishes).

1. The number of products available can be reset back to the value of 10 when the input `ResetStock` is activated.

1. The machine shall always provide a status code output.

1. The `Cancel` input button shall be debounced both ways, with a time duration of 0.2 seconds.

1. Use parameters from Matlab for all values you consider necessary (e.g. duration of delays, prices etc.).
Our customer may want to adjust the parameters at any time.

1. Test your state machine (use one/multiple separate test models if necessary)
