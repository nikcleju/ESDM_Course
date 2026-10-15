---
title: Introduction to Simulink and Stateflow
subtitle: Lab 1, ESDM
documentclass: scrartcl
fontsize: 12pt
---

# Objective

Introducing students to the Simulink environment and the Stateflow component.

# Theoretical aspects

TBD
        

# Exercises

1. Create a Parking Counter FSM according to the specifications below.

	Steps:
	  - Create a new Simulink model
	  - Create a Stateflow Chart inside the model
	  - Design the FSM inside the chart
	  - Add some inputs and test the model

	**Model specifications**

	Inputs:

	- up: boolean. Whenever a car is entering the area, `up` is TRUE.
	- down: boolean. Whenever a car is leaving the area, `down` is TRUE.

	Outputs & internal variable:

	- count: integer [0,10]

	Requirements:

	- The output `count` shall indicate always the current number of cars in the parking area.
	- Upon initialization, `count` shall be initialized to 0.


2. Extend the model in the following way:

	- The inputs `up` and `down` shall be considered upon transitioning from FALSE to TRUE (e.g. if `up` stays TRUE for 10 seconds, 
	count it only once).

	- Introduce another input `count_init` which shall be used as the initialization value for `count`.


# Final questions

1. TBD
