## III. Extended FSMs and Timed Automata


### FSM example

- Recall the previous FSM example

![Parking system FSM](fig/Parking_2_FSM.png)

- Can we make it is simpler to draw?

### Extended FSMs

- **Extended FSM** = FSM with **internal variables**

![Extended FSM with variable "count"](fig/Parking_3_Extended.png)

### Extended FSM

- The state of the model = the current "bubble" and the values of **all the internal variables**

- Example: OS hibernation in Windows:
  - state of computer = all the RAM memory values
  - if all memory is written down on HDD, and reloaded tomorrow, the system effectively resumes operation from where it left off

- State is not anymore "the number of bubbles"
  - there is only one "bubble" in our FSM
  - but there are MAX+1 states (all possible values of the count variable)

### Declarations

- Always make explicit declaration of:
  - model inputs
  - model outputs
  - model internal variables
  - and their data types
  
### Measure time

- Extended FSM are useful for modeling **time-based** conditions:
  - measure passage of time: increment a variable every *tick*
  - only works if the FSM is time-triggered

### Example: pedestrian crossing light

- How is time measured in the model below?
- How many states does the model below have?

![Extended FSM with time measuring (image from Seshia' slides)](fig/ExtFSM_PedestrianCrossing.png){width=80%}


### Hybrid systems

![Hybrid systems (image from Seshia' slides)](fig/ExtFSM_HybridSystems.png){width=80%}

### Hybrid systems

- **Hybrid systems** = system with mixes discrete and continuous behavior

- Example: a PID controller with different modes:
  - a set of distinct functioning model (e.g. Startup / Normal / Idle)
  - each state is a sub-system implemented with continuous dynamics
  
- State **refinement** = a lower-level implementation of a state

### Types of hybrid systems

- **Timed automata**  = hybrid system where every state refinement just measures passage of time (differential equation of degree 1)

- **Higher-order systems** = hybrid system where every state refinement uses higher-order differential equation (2 or more)

- **Two-level control systems** = complex controllers with two levels of operation
  - high-level discrete modes of operation (e.g. ECU Power Modes: Normal / Startup / Sleep Mode 1 / Sleep Mode 2)
  - low-level refinements with continuous dynamics
  
### Timed automata  

![Timed automaton example (image from Seshia's slides)](fig/ExtFSM_TimedAutomata.png){width=60%}

### Example

- Mouse Double-click detector model

![(image from Seshia's slides)](fig/ExtFSM_MouseDoubleClickDetector.png){width=60%}

- Here $\dot{x}(t) = 1$ means "x(t) increases linearly with time", so it measures time
- How many states does this model have?

### Example: Another Thermostat

- Another thermostat model as a Timed Automaton

![(image from Seshia's slides)](fig/ExtFSM_TimedAutomata_Thermostat_1.png)

### Example: Another Thermostat

- Another thermostat model as a Timed Automaton

![(image from Seshia's slides)](fig/ExtFSM_TimedAutomata_Thermostat_2.png)


### Example: Another Traffic Light

- Traffic Light controller Timed Automaton

![(image from Seshia's slides)](fig/ExtFSM_TimedAutomata_TrafficLight.png){width=80%}

### Example: Tick generator

- Timed Automaton to generate a *tick* every T seconds

![(image from Seshia's slides)](fig/ExtFSM_TimedAutomata_TickGenerator.png){width=70%}

### Example: Bouncing Ball

- Timed Automaton to simulate a bouncing ball movements

![(image from Seshia's slides)](fig/ExtFSM_TimedAutomata_BouncingBall.png){width=80%}