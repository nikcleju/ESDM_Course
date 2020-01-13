---
title: List of subjects for ESDM 2019-2020 exam
subtitle: DRAFT 2020-01-13, NOT FINAL YET
documentclass: scrartcl
fontsize: 12pt
---

The exam will consist of:

1. Implementation of one FSM from the "Finite State Machines" section, to implement and explain
2. A few (~ 3) questions from the "General" section

# Finite State Machines 

1. Realize a Finite State Machine to implement a **parking vehicle counter**, as follows:
	- the system must always indicate how many cars are in the parking space
    - there is 1 boolean input `In`, defined as: False = no car entering, True = one car is entering
    - there is 1 boolean input `Out`, defined as: False = no car exiting, True = one car is exiting
    - there is 1 output `Count`, an integer number
    - the parking space has only 60 parking spots available.
    - the following scenarios are possible:
        - a car may enter the parking
        - a car may exit the parking
        - a car may enter the parking and another one may exit the parking simultaneously
    - the output number is not allowed to exceed 60 or go below 0.
    
    Explain your design briefly.

\smallskip    

1. Realize a Finite State Machine to implement a **thermostat**, as follows:
	- the thermostat must keep the temperature around 22 degrees, +/- 0.5 degrees (i.e. within the interval 21.5 - 22.5 degrees)
	- there is 1 input `Temp` which is the room temperature (real number).
    - there is 1 output `On`, which controls the heating system: TRUE = turn heating ON, False = turn heating OFF
    - when temperature is below 21.5, heating should be started
    - when temperature is above 22.5, heating should be stopped

    Explain your design briefly.
    
\smallskip    
    
1. Realize a Finite State Machine to implement a **pedestrian traffic light**, as follows:
    - there is 1 boolean input `Button` (False = not pressed, True = pressed)
    - there is 1 output `Color` with two possible values: Color = Red, or Color = Green
    - red lasts 60 seconds, green lasts 20 seconds
    - if no one presses the button, the green is skipped and the traffic light remains red
    - if someone presses the button, the traffic light becomes green after the current 60s of red expire 
    ("când îi vine rîndul", like the common pedestrian traffic signs in Iasi)
    
    Explain your design briefly.
    
\smallskip    
    
1. Realize a Finite State Machine to implement a **pedestrian traffic light**, as follows:
    - there is 1 boolean input `Button` (False = not pressed, True = pressed)
    - there is 1 output `Color` with two possible values: Color = Red, or Color = Green
    - if no one presses the button, the traffic light remains red
    - when someone presses the button, the traffic light becomes green after 5 seconds
    - green lasts 20 seconds
    - after a green, there should be at least 60 seconds of red, before the next green.
    
    Explain your design briefly.

\smallskip
    
1. Realize a Finite State Machine to implement a **car traffic light** at a crossing, as follows:
    - there is 1 boolean input `Button` for pedestrians (False = not pressed, True = pressed)
    - there is 1 output `Color` with three possible values: Color = Red, Color = Yellow or Color = Green
    - if no one presses the button, the traffic light remains green
    - when someone presses the button, the traffic light becomes yellow for 5 seconds, then it becomes red
    - red lasts 20 seconds
    - after red expires, the light goes directly to green (no yellow)
    - any green must last for at least 60 seconds
    
    Explain your design briefly.

\smallskip
  
1. Realize a Finite State Machine to implement a **debouncing** of a boolean input signal `in`, as follows:
    - there is a boolean input signal `in` and a boolean output `out`
    - initially, `out` takes the initial value of `in`
    - `out` is set to TRUE only after `in` stays TRUE for at least 5 seconds
    - `out` is set to FALSE only after `in` stays FALSE for at least 8 seconds

    Explain your design briefly.

\smallskip
        
1. Realize a Finite State Machine to implement the following requirements:
    - there are two boolean inputs `A` and `B` and a boolean output `out`
    - initially, `out` takes the value FALSE
    - `out` becomes TRUE only in the following case: when A is TRUE before B, and B becomes TRUE no latter than 3 seconds after A
    - afterwards, `out` is set to FALSE whenever A or B becomes FALSE


# General

1. Discuss a few common characteristics of embedded systems

2. Discuss a few characteristics which make embedded systems different than PC-like systems

3. Indicate briefly the main structural components of embedded systems

4. What are the mechanical equivalents of the electrical current and voltage? (in the analogy used in the lectures)

4. What are the electrical equivalents of the following mechanical elements? Justify your answer.
    - controlled voltage source 
    - the inertial force
    - the friction force

4. Electrical model of a DC motor
    - draw the equivalent schematic
    - what are the input and outputs?
    - what is the transfer function?
    - what is the order of the transfer function?
    
4. Fill in: "The DC motor model is a model of order ______. If the inductance of the armatures is negligible, it can be approximated with a model of order ______."

4. Explain how is the load modeled in the electrical equivalent of a DC motor.
  
5. Describe in short the PID controller:
    - why is it used
    - what is its input and output
    - what are its three components and what is their purpose

6. Consider a motor controlled with a PID. If the target speed is depicted below, sketch the motor output speed if:
    a. The controller has only the P component
    b. The controller has both the P and I components

	Justify your choices.
	
	TBD: make drawing of target speed = unit step

7. Match the the following three images with the three types of PID controllers:
	a. PID controller with only the P component
	b. PID controller with only the P and I component
	c. PID controller with P, I and D components
	
	Justify your choices.
	
	TBD: make drawings

8. Consider the following FSM: ... How many different states does the FSM have?
   (Hint: don't count only the "bubbles", but the number if different internal configurations possible).
	
	TBD: make drawings:
	 - parking counter
	 - thermostat
	 - simple traffic light

6. What does it mean that a Finite State Machine is **deterministic**?

6. What are "hybrid systems"?
    - explain what they are
    - indicate a few examples
    
7. Explain (in detail) the operation of the following timed-automaton FSM:

	TBD: draw the "Mouse Double Click Detector" system from 04_ESDM_ExtendedAndTimedAutomata.pdf

7. Consider the following timed-automaton FSM for detecting single-clicks and double-clicks (Mouse Double Click Detector).

	Draw the signal $x(t)$ if the input event `click` is as follows: 

	TBD: Draw the click event: (pause - click - very short pause - click - pause) or similar

	TBD: draw the "Mouse Double Click Detector" system from 04_ESDM_ExtendedAndTimedAutomata.pdf

7. What is the difference between **temporal** composition and **spatial** composition of two FSM systems A and B?

7. Explain the differences between the following composition types:
    - **side-by-side** and **cascade** composition
    - **sequential** and **parallel** composition
    - **synchronous** and **asynchronous** composition

8. Consider the two systems A and B below.

	TBD: draw two simple systems A, B with 2-3 states, like in slides
	
	Draw the equivalent FSM of the composition of A and B, assuming:
	a. synchronous composition
	a. asynchronous composition, interleaving semantics
	a. asynchronous composition, simultaneous semantics
	
9. What does it mean that a system has **feedback composition**?

8. Explain the following concepts:
    - **super-state** and **sub-state**
    - history transition



