## II. Modeling continuous systems

### Continuous systems

- Physical processes are usually in continuous domain
    - e.g. electrical, mechanical

- Processes in continuous domain are described by **differential equations**
    - i.e. with unknown functions + their derivatives + their second derivatives + ...

- Simple (ideal) case: differential equations are linear:
    - only operations allowed: sum, multiplication by a constant

- Every electrical/mechanical part defines a certain
relation between the unknowns

### Electrical systems

Electrical systems:

- Unknown functions = voltage + current in all branches
- Electrical (ideal) elements:
    - resistance: $u(i) = R \cdot i(t)$
	- capacity: $i(t) = C \cdot \frac{d}{dt} u(t)$
	- etc.
- One big system of linear differential equations (SCS course, basically)
    - Kirchhoff equations <=> equations between currents and voltages <=> linear differential equation system
	
- Example: an RC system (solve at blackboard)

### Mechanical systems

Mechanical systems:

- Unknown functions = coordinates x(t), y(t), z(t)
    - speeds = derivatives of the positions
	- acceleration = derivative of speed = second derivative of positions
	- (forces: $F = m \cdot a = m \cdot \frac{d^2}{dt^2}x(t)$)
	
- Mechanical (ideal) elements:
    - (Consider just a single dimension $x(t)$, is easier)
    - inertial force: $F = m \cdot a = m \cdot \frac{d^2}{dt^2}x(t)$
	- friction force:
	   - sliding friction: $\vec{F_f} = - \mu \vec{N} = - \mu \cdot m \cdot \frac{d^2}{dt^2}x(t)$
	   - viscous friction: $\vec{F_v} = - C_v \cdot \vec{v} = - C_v \cdot \frac{d}{dt}x(t)$
	- etc...

### Mechanical systems

- Mechanical elements are described by linear differential equations,
just like electrical ones
    - they are just idealizations, physical processes can be highly nonlinear (more complex)
	- but wait, so are electrical devices actually, and this hasn't stopped us...

- Example: oscillations after releasing of a loaded spring 
     - (solve at blackboard)


### Electrical - mechanical analogies

- Multiple ways to define analogies between electrical and mechanical characteristics

- Here is the one we will use:

|    Electr. |   Mech. (linear)  |  Mech. (rotational) |
|  ----------|  --------------- | ------------------ |
|   Current [A] |   Force [N]   |  Torque ("cuplu") [N.m] |
|   Voltage [V] |   Speed [m/s] | Angular speed [rad/s]|


### Simple model of a DC motor

- Motor: gateway between the two electrical and mechanical domains
    - converts electric energy to mechanical energy, and vice-versa

- (Simple) model of a DC motor:
    
	![Simple model of a DC motor](fig/II_DCMotorModel.png){width=50%}
    
Image from Mathworks Simulink (`ssc_dcmotor` example model)


### DC motor model: electrical side

Electrical circuit of the DC motor model:

- Resistance: models the resistance of the windings
    - $u(t) = R \cdot i(t)$
- Inductance: models the inductive behavior of the windings
    - $u(t) = L \cdot \frac{d}{dt}i(t)$
- Controlled voltage source:
    - Voltage ("back electro-magnetic force voltage") is proportional to motor angular speed $S(t)$ on the mechanical side (think of a dynamo)
	- $u(t) = K_e \cdot S(t)$

### DC motor model: mechanical side

Mechanical circuit of the DC motor model (no load):

- Controlled force/torque source
    - Generates force/torque proportional to the current $i(t)$ on the electrical side
	- $T = K_t \cdot i(t)$
	
- Inertia: models the inertial force of the moving part of the motor
    - $T_i = - m \cdot acceleration = - m \cdot \frac{d}{dt} S(t)$ 

- Friction: models the (viscous) friction force of the moving part of the motor, proportional to speed
    - $T_f = - C_v \cdot S(t)$

- Inertia and Friction forces (torques) oppose the force(torque) of the motor, hence they have minus sign.

### Laplace transform

- Both electrical and mechanical sides are described by linear differential equations

- The Laplace transform is a useful tool (remember SCS)
    - derivation = multiplication by $s$
	- integration = multiplication by $1/s$
	- transform function H(s) = output(s)/input(s)

- Exercise: write the equations of all electrical and mechanical elements in Laplace transform

### Full electrical model

- All the mechanical elements can be modeled in the electrical domain
    - since they are all just differential equations, basically
    - obtain a full model in the electrical domain only

### The controlled voltage source

- How to model the controlled voltage source?

- Like this:
    - voltage is proportional to speed: $U(s) = K_e \cdot S(s)$
    - speed = integral of acceleration: $S(s) = S_0 + 1/s \cdot A$
    - acceleration is proportional to force (force(torque) / mass) = $C_{const} \cdot T(s)$
	- force/torque = proportional to current: $T(s) = K_t \cdot I(s)$

- Result: $U(s) = K_e \cdot (S_0 + 1/s \cdot C_{const} \cdot K_t I(s))$

- $U(s) = Constant_1 + Constant_2 \cdot 1/s \cdot I(s)$
	- voltage depends on integral of current (plus a constant)
	- what kind of electrical element acts like this?
	
### The controlled voltage source

- The controlled voltage source can be modeled as a **capacity**
    - on the electrical side

- The constant term added in front = the initial voltage on the capacity

- The capacitance value depends on all the motor parameters


### The inertial force

- Inertia = a force which opposes (i.e. reduces) the motor force, and is proportional to acceleration

- Use the analogy:
    - force = current
	- speed = voltage
	- acceleration  = derivative of speed = derivative of voltage
	
- Inertia = a current which opposes (i.e. reduces) the motor current, and is proportional to derivative of voltage
    - current proportional to derivative voltage <=> a capacity
	- reduces motor current <=> in parallel with the controlled voltage source (steals some current)
	
- Inertia model = a **capacity in parallel** with the controlled voltage source
    - it steals current from the motor (i.e. reduces motor force)
	- amount of current stolen = proportional to derivative of voltage

### The friction force

- (Viscous) friction = a force which opposes (i.e. reduces) the motor force, and is proportional to speed

- Use the analogy:
    - force = current
	- speed = voltage
	
- (Viscous) friction = a current which opposes (i.e. reduces) the motor current, and is proportional to voltage
	
- (Viscous) friction model = a **resistance in parallel** with the controlled voltage source
    - it steals current from the motor (i.e. reduces motor force)
	- amount of current stolen = proportional to voltage (speed)

### The sliding friction force

- There can also exist a sliding friction force = friction force which does not 
depend on speed, but is a constant \
    - that's the friction force you encountered in high-school physics, likely

- Exercise: how is this force modeled in electrical domain?

### The full electrical model

- Draw picture at blackboard
- This is a second order model (1L, 1C)
    - the two capacities are in parallel, so they can be added into a single one

- Derive a transfer function (input = voltage on motor input, output = motor speed)

- Take home message: simple DC motor no-load model = a second order RLC model
    - this is a no-load model (motor doesn't move anything heavy)

### Motor under load

- Exercise: suppose our motor drags/lifts a constant weight
    - i.e. like a crane lifting a big weight from the ground

- How to model the load?
    - think ... 

### Motor under load

- Exercise: suppose our motor drags/lifts a constant weight
    - i.e. like a crane lifting a big weight from the ground

- How to model the load?
    - like a constant force/torque opposing the motor force/torque
	
### Simulink model

- Simulink has a DC motor model already integrated
- You will use it in the lab

