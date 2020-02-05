---
title: List of subjects for ESDM 2019-2020 exam
subtitle: Final 2020-02-05
documentclass: scrartcl
fontsize: 12pt
---

The exam will consist of:

1. Implementation of one FSM from the "Finite State Machines design" section, to implement and explain
2. A few (~ 3) questions from the "General" section

# Finite State Machines design

1. Design a Finite State Machine to implement a **parking vehicle counter**, as follows:
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

1. Design a Finite State Machine to implement a **thermostat**, as follows:
	- the thermostat must keep the temperature around 22 degrees, +/- 0.5 degrees (i.e. within the interval 21.5 - 22.5 degrees)
	- there is 1 input `Temp` which is the room temperature (real number).
    - there is 1 boolean output `On`, which controls the heating system: TRUE = turn heating ON, False = turn heating OFF
    - when temperature is below 21.5, heating should be started
    - when temperature is above 22.5, heating should be stopped

    Explain your design briefly.
       
	\smallskip    
    
1. Design a Finite State Machine to implement a **pedestrian traffic light**, as follows:
    - there is 1 boolean input `Button` (False = not pressed, True = pressed)
    - there is 1 output `Color` with two possible values: Color = Red, or Color = Green
    - green always lasts 20 seconds
    - red lasts at least 60 seconds, and then as follows:
        - if no one presses the button, the traffic light remains red indefinitely
        - if button is pressed, the traffic light becomes green after 5 seconds
        - if button is pressed in the first 60 seconds of red, the light stays red until the 60 seconds expire, and then changes to green after 5 seconds.
    This must work even if the button is pressed only briefly (e.g. pressed only for 1 second within the 60 seconds of red)
        
    Explain your design briefly.

	\smallskip
    
1. Design a Finite State Machine to implement a **car traffic light** at a crossing, as follows:
    - there is 1 boolean input `Button` for pedestrians (False = not pressed, True = pressed)
    - there is 1 output `Color` with three possible values: Color = Red, Color = Yellow or Color = Green
    - red lasts 30 seconds
    - after red expires, the light becomes directly green (no yellow)
    - green lasts at least 60 seconds, and then:
        - if no one presses the button, the traffic light remains green indefinitely
        - when someone presses the button, the traffic light becomes yellow for 5 seconds, then it becomes red
        - if button is pressed in the first 60 seconds of green, the light stays green until the 60 seconds expire, and then changes to yellow
    This must work even if the button is pressed only briefly (e.g. pressed only for 1 second within the 60 seconds of green).
    - yellow lasts 5 seconds, then light becomes red
    
    Explain your design briefly.


# General (theory) questions

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

6. Consider a motor controlled with a PID. Initially the motor is not moving. At time 0, the target speed becomes $1000$ rpm, as depicted below.
	Sketch the motor output speed if:
    a. The controller has only the P component
    b. The controller has both the P and I components

	Justify your choices and explain the difference.
	
	![Target speed](figs/TargetSpeed.png){.id width=30%}

7. Consider a motor controlled with a PID. Initially the motor is not moving. At time 0, the target speed becomes $1000$ rpm.
	The motor output speed evolves as depicted in the three images below.
	Indicate which image corresponds to each of the following three types of PID controllers:
	a. PID controller with only the P component
	b. PID controller with only the P and I component
	c. PID controller with P, I and D components
	
	Justify your choices.
	
	![Speed 1](figs/TargetAndMotorSpeed3.png){.id width=30%}
	![Speed 2](figs/TargetAndMotorSpeed1.png){.id width=30%}
	![Speed 3](figs/TargetAndMotorSpeed2.png){.id width=30%}
	

8. Consider the following FSM: (pick one of below). How many different states does the FSM have?
   (Hint: don't count only the "bubbles").

	*(Drawings:*
	 - *parking counter*
	 - *thermostat*
	 - *simple traffic light)*
	
	![Parking Counter](figs/FSM_ParkingCounter.png){.id width=50%} \ 
	
	\ 
	
	![Thermostat](figs/FSM_Thermostat1.png){.id width=70%} \ 
	
	\ 
	
	![Simple Traffic Light](figs/FSM_SimpleTrafficLight.png){.id width=70%} \ 

6. What does it mean that a Finite State Machine is **deterministic**?

6. What are "hybrid systems"?
    - explain what they are
    - indicate a few examples
    
7. Explain the operation of the following timed-automaton FSM (i.e. what happens in each state, what happens to the signal x(t)):

	![Timed-automaton system](figs/FSM_MouseDoubleClick.png){.id width=50%} \ 

7. What is the difference between **temporal** composition and **spatial** composition of two FSM systems A and B?

7. Explain the differences between the following composition types:
    - **side-by-side** and **cascade** composition
    - **sequential** and **parallel** composition
    - **synchronous** and **asynchronous** composition

8. Consider the two systems below.

	![Two Finite State Machines](figs/FSM_Composition.png){.id width=50%} \ 
	
	Draw the equivalent FSM of the composition of the two systems, assuming:
	a. synchronous composition
	a. asynchronous composition, interleaving semantics
	a. asynchronous composition, simultaneous semantics
	
9. What does it mean that a system has **feedback composition**?

8. Explain the following concepts:
    - **super-state** and **sub-state**
    - history transition



