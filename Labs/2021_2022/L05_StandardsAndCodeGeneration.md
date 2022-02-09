---
title: Model standards and code generation tools
subtitle: Lab 5, ESDM
documentclass: scrartcl
fontsize: 12pt
---

# Objective

Using the Model Advisor and the Code Generation tools 
for model-based development in Simulink.


# Exercises

1. Design a FSM in Stateflow for a simplified alarm system. The system has two inputs `DoorOpen` and `CodeOK` and one output `AlarmOn`, for the following requirements:

    1. The alarm is turned off (`AlarmOn = FALSE`) always when `DoorOpen = FALSE`.
    2. The alarm is turned on when the door is open (`DoorOpen = TRUE`), while `CodeOK = FALSE`. 
    3. The alarm is turned off when either the door is closed (`DoorOpen = FALSE`) or the correct passcode is entered (`CodeOK = TRUE`).

2. Test your design using another model. Inside this test model, use the `Model Reference` to reference the model under test.

3. Run the Model advisor tool (Analysis -> Model Advisor -> Model Advisor), select and run the "Modeling Standards for MAB" checks. Observe the warnings/failures and fix some of them.

   - You need to install the toolbox `Simulink Check` in Add-Ons -> Get Add-ons

4. Generate C code from the model. Locate the code files, open them and identify the implementation of the state machine. How is it implemented (with which C instructions)?
   
   Steps:
     - specify the data types of all inputs and outputs
	 - Right-click on chart -> Block Parameters -> Code Generation -> Function Packaging and select:
	 
	   - Reusable function
	   - User specified function name (you choose name)
	   - User specified file name (you choose name)
	 
     - Right-click on chart -> C/C++ Code -> Build This Subsystem

