---
title: List of subjects for ESDM 2018-2019 exam
subtitle: DRAFT 2019-05-11, NOT FINAL YET
documentclass: scrartcl
fontsize: 12pt
---

The exam will consist of:

1. One FSM from the "Finite State Machines" section, to implement and explain
2. 2-3 questions from the "General" section

# Finite State Machines 

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

4. What are the electrical equivalents of the following mechanical elements? Justify your answer.
    - controlled voltage source 
    - the inertial force
    - the friction force

4. Electrical model of a DC motor
    - draw the equivalent schematic
    - what are the input and outputs?
    - what is the transfer function?
    - what is the order of the transfer function?
    
5. Describe in short the PID controller:
    - why is it used
    - what is its input and output
    - what are its three components and what is their purpose

6. What are "hybrid systems"?
    - explain what they are
    - indicate a few examples

7. Explain the differences between the following composition types:
    - **side-by-side** and **cascade** composition
    - **sequential** and **parallel** composition
    - **synchronous** and **asynchronous** composition

8. Explain the following concepts:
    - **super-state** and **sub-state**
    - history transition

9. Explain the Hall effect and how it is used for measuring the rotation speeds of motors

10. Explain briefly the different types of embedded processors

11. Explain how **pipelining** processors operate, and the possible problems of this feature


