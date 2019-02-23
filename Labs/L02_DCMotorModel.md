---
title: Modeling a DC Motor in Simulink
subtitle: Lab 2, ESDM
documentclass: scrartcl
fontsize: 12pt
---

# Objective

Using the Simulink/Simscape DC Motor model in simple simulations.


# Theoretical aspects

        

# Exercises

1. Create a DC Motor model according to the following schematic.

	Explain the role of each block, and check its parameters.

	Set the DC Motor parameters to the actual values from the attached datasheet.
	
	Comment out the "Rotational Hard Stop" block for now.
	
	Put everything inside a subsystem block named "Physical Plant".

	![](fig/L02_PhysPlant.png)

2. Apply a 12V voltage source to the motor (with no load), and observe the output.

    a. What is the maximum motor speed (known as "no-load speed")? 
	a. How long does it take the to motor reach 90% of the no-load speed?
    b. What happens with the current in the beginning of the simulation? Why?
	
3. Now apply a load (torque) to the motor, using non-zero value for the load input. 
    
	a. What is the maximum motor speed in this case?
	b. Increase the load torque 2 times, 3, times, 4 times and 5 times, and observe the 
	maximum motor speed. How does it vary?

5. Simulate a hard mechanical stop by un-commenting the "Rotational Hard Block" block from inside the physical plant.
Set the upper limit to a convenient value.
    
	a. What happens with the current value? Why?

6. Hard stops can damage a motor. Implement a detection rule for a hard stop, such that
whenever it happens, the motor is stopped (the supply is cut off).

4. Simulate a variable load: 
add to the constant load input a 10% slow sinusoidal variation (amplitude = 10% of the constant value).
Observe the outputs. What happens to the speed?


5. Stabilize the speed with a PID block in a feedback connection, replacing the constant voltage input, 
as in the figure below. The desired target speed is 350 rad/s.

	![](fig/L02_Bench.png)

	In the PID block parameters, use a 0 value for the I and D constant (only the P constant is non-zero). Choose an appropriate
P value so that the motor works reasonably well.
   
   a. What happens to the motor speed?
   b. What happens at the beginning of the simulation?
   c. Is the target speed actually reached?
   c. What is the influence of the P value? Modify it and observe the differences.
   d. Set a small non-zero value for the I value as well. What happens now?
   

