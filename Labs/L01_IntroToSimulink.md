---
title: Basic control blocks in Simulink
subtitle: Lab 1, DSP
documentclass: scrartcl
fontsize: 12pt
---

# Objective

Introducing students to the Simulink environment

# Theoretical aspects

Blocks often used:

  - In and Out ports
  - Switch
  - Constant / values from Workspace
  - Logical operators
  - Relational operators
  - Sum / Product
  - Enabled subsystems
  - If / Action / Merge blocks
  - Model configuration parameters: solver step size
        

# Exercises

1. Create a Vehicle Speed Adapter system that satisfies the following requirements.

    Implement the conditions in the requirements in two ways:
     - with Switch blocks
     - with If / Action / Merge blocks
  
    Implement the Suggested Gear functionality with a lookup table block.

---------------

**Requirements**


  1. Inputs:
  
     - `UserRequest`: enum (USERREQ_NONE=0, USERREQ_ACC=1, USERREQ_DECC=2)
     - `CurrentSpeed`: double (0 - 200 km/h)

  2. Outputs:
  
     - `TargetSpeed`: double (0 - 200 km/h)
     - `SuggestedGear`: int (0 - 6)

  3. Functional requirements

      1. When input `UserRequest` is USERREQ_ACC, the output `TargetSpeed` shall be computed
      from the input `CurrentSpeed`, increased according to acceleration value `PARAM_MaxAccel`.
      2. When input `UserRequest` is USERREQ_DECC, the output `TargetSpeed` shall be computed
      from the input `CurrentSpeed`, decreased according to decceleration value `PARAM_MaxDeccel`.
      2. When input `UserRequest` is USERREQ_NONE, the output `TargetSpeed` shall computed  
      from the input `CurrentSpeed`, with no acceleration nor decceleration.
      3. The output `TargetSpeed` shall be below maximum value `PARAM_MaxSpeed` at all times.
      4. The output `SuggestedGear` shall be computed based on the `TargetSpeed` as follows:
          
           Speed Range       Suggested Gear
          -------------     ----------------- 
          0  - 20 km/h         1  
          20 - 40 km/h         2
          40 - 60 km/h         3
          60 - 90 km/h         4
          90 - 120 km/h        5
          over 120 km/h        6

---------------  


2. Create a testbench model and test the Speed Adapter module in some simple scenarios:
   - test that all user requests work
   - test that all suggested gear values are output
   - test that PARAM_MaxSpeed is not exceeded
   
3. Implement the following new requirement as well, and then update the test module to test them:
      
      1. The speed adaption module can be enabled or disabled with parameter `PARAM_EnableSpeedAdapt`.
      2. When `PARAM_EnableSpeedAdapt` is FALSE, the output `TargetSpeed` shall have the 
      value of the input `CurrentSpeed`, without any modification
      2. When `PARAM_EnableSpeedAdapt` is TRUE, the output `TargetSpeed` shall be computed
      according to the previous requirements.


# Final questions

1. TBD
