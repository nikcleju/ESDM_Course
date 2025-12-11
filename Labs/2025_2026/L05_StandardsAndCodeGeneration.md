---
title: Model standards and code generation tools
subtitle: Lab 5, ESDM
documentclass: scrartcl
fontsize: 12pt
---

# Objective

Using the Model Advisor and the Code Generation tools
for model-based development in Simulink.

# Theoretical aspects

## AUTOSAR ARXML files

The interface and internal structure of Simulink models can be described using AUTOSAR XML (`ARXML`) files.
These files specify the data types, interfaces, signals, ports, blocks, etc.

See the lectures.

## Model Advisor and MAAB rules

`MAAB` (sometimes abbreviated `MAB`) and `JMAAB` are sets of guidelines and recommended practices for Simulink and Stateflow models (similar to `MISRA-C` for C code).

Following these guidelines leads to higher-quality models and is often required in practice.

Some of the rules can be checked automatically with the `Model Advisor` tool.

## Generating C code

MATLAB can generate C code automatically from Simulink models, including Stateflow charts.

Steps:

- Specify the data types of all inputs and outputs.
- In the chart Block Parameters -> Code Generation -> Function Packaging, select:
  - Reusable function
  - User-specified function name (choose the name)
  - User-specified file name (choose the name)
- Right-click on the chart -> C/C++ Code -> Build This Subsystem.

It is recommended that delays are specified in `ticks` rather than `sec` or `msec`, so the generated code stays simpler.

# Exercises

1. Design an FSM in Stateflow for a simplified alarm system. The system has two inputs `DoorOpen` and `CodeOK` and one output `AlarmOn`, for the following requirements:

    1. Initially the alarm is off (`AlarmOn = FALSE`) but armed.
    2. The alarm turns on 15 seconds after the door is opened (`DoorOpen = TRUE`) while `CodeOK = FALSE`.
    3. When the correct passcode is entered (`CodeOK = TRUE`), the alarm turns off.
    4. After the door is closed again, the alarm rearms and is ready for the next cycle.

2. Test your design using another model. Inside this test model, use the `Model Reference` to reference the model under test.

3. Run the Model Advisor tool (Analysis -> Model Advisor -> Model Advisor), select and run the "Modeling Standards for MAB" checks. Observe the warnings/failures and fix some of them.

   - You need the toolbox `Simulink Check` (Add-Ons -> Get Add-Ons).

4. Generate C code from the model. Locate the generated files, open them, and identify the implementation of the state machine.

   How is it implemented (with which C instructions)?

   How would you implement it yourself in C?
