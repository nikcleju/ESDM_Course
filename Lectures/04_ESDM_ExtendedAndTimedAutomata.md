## III. Extended FSMs and Timed Automata


### FSM example

- Recall the previous FSM example

![Parking system FSM](fig/Parking_2_FSM.png)

- Can we make it simpler to draw?

### Extended FSMs

- **Extended FSM** = FSM with **internal variables**

![Extended FSM with variable "count"](fig/Parking_3_Extended.png)

### Extended FSM

- The state of the model = the current "bubble" and the values of **all the internal variables**

- Example: OS hibernation in Windows:
  - state of computer = all the RAM memory values
  - if all memory is written down on HDD, and reloaded tomorrow, the system effectively resumes operation from where it left off

- Number of states is not anymore "the number of bubbles"
  - there is only one "bubble" in our FSM
  - but there are MAX+1 states (all possible values of the count variable)

### Declarations

- Always make explicit declaration of:
  - model inputs
  - model outputs
  - model internal variables
  - and their data types

### Measure time

- Extended FSMs are useful for modeling **time-based** conditions:
  - measure passage of time: increment a variable every *tick*
  - only works if the FSM is time-triggered

### Example: pedestrian crossing light

- How is time measured in the model below?
- How many states does the model below have?

![Extended FSM with time measuring [^ExtFSMtime]](fig/ExtFSM_PedestrianCrossing.png){width=80%}

[^ExtFSMtime]: image from Seshia's slides

### Hybrid systems

![Hybrid systems [^HybridSystems]](fig/ExtFSM_HybridSystems.png){width=80%}

[^HybridSystems]: image from Seshia's slides

### Hybrid systems

- **Hybrid systems** = system with mixed discrete and continuous behavior

- Example: a PID controller with different modes:
  - a set of distinct functioning models (e.g. Startup / Normal / Idle)
  - each state is a sub-system implemented with continuous dynamics

- State **refinement** = a lower-level implementation of a state

### Types of hybrid systems

- **Timed automata**  = hybrid system where every state refinement just measures passage of time (differential equation of degree 1)

- **Higher-order systems** = hybrid system where every state refinement uses higher-order differential equation (2 or more)

- **Two-level control systems** = complex controllers with two levels of operation
  - high-level discrete modes of operation (e.g. ECU Power Modes: Normal / Startup / Sleep Mode 1 / Sleep Mode 2)
  - low-level refinements with continuous dynamics

### Timed automata

![Timed automaton example [^TimedAutomaton]](fig/ExtFSM_TimedAutomata.png){width=60%}

[^TimedAutomaton]: image from Seshia's slides

### Example

![Mouse Double-click detector model [^ExtDblClick]](fig/ExtFSM_MouseDoubleClickDetector.png){width=40%}

[^ExtDblClick]: image from Seshia's slides

- Here $\dot{x}(t) = 1$ means "x(t) increases linearly with time", so it measures time
- How many states does this model have?

### Example: Another Thermostat

![- Another thermostat model as a Timed Automaton [^AnothTherm]](fig/ExtFSM_TimedAutomata_Thermostat_1.png)

[^AnothTherm]: image from Seshia's slides

### Example: Another Thermostat

![ Input and output signals [^AnothTherm2]](fig/ExtFSM_TimedAutomata_Thermostat_2.png)

[^AnothTherm2]: image from Seshia's slides

### Example: Another Traffic Light

![Traffic Light controller Timed Automaton [^AnothTrafL]](fig/ExtFSM_TimedAutomata_TrafficLight.png){width=80%}

[^AnothTrafL]: image from Seshia's slides

### Example: Tick generator

![Timed Automaton to generate a *tick* event every T seconds [^TickGen]](fig/ExtFSM_TimedAutomata_TickGenerator.png){width=70%}

[^TickGen]: image from Seshia's slides

### Example: Bouncing Ball

![Hybrid system to simulate a bouncing ball movements [^BouncingBall]](fig/ExtFSM_TimedAutomata_BouncingBall.png){width=80%}

[^BouncingBall]: image from Seshia's slides

### FSM simulation software

- FSM simulation software

- Used in this class: Stateflow (Simulink / MATLAB)

- Features:

  - State Actions
  - Temporal Logic
  - Other events
  - ... other ...

### State actions

- Actions can exist not only on transitions, but also **inside states**

- Three main types of **State Actions**:

  - **entry (en)**:  executed only when a **state is entered**
  - **exit (ex)**:   executed only when a **state is exited**
  - **during (du)**: executed when a state is active, and is neither entered, nor exited

### State actions

![State Actions example [^StateAct]](fig/Stateflow_StateActions.png)

[^StateAct]: image from MATLAB docs

### State actions

- State actions can be avoided (use only transition actions),
but sometimes one or the other are more convenient

### Temporal logic

- For time-based conditions, we can use certain predefined variables/events,
which can be used to **measure time spent in a state**

  - ***tick***: measures time steps
    - is incremented at **every chart execution**
    - is reset to 0 every time a state is exited or entered
    - actual duration **depends** on model step size


  - ***sec / msec***: measures seconds or milliseconds
    - is incremented every second / millisecond
    - is reset to 0 every time a state is exited or entered
    - actual duration is **independent** of model step size

### Temporal logic

- Temporal operators **after()**, **on()**, **every()**
can generate events which can be used in conditions

- Examples:
  - ***after(10, tick)***:
    - evaluates to TRUE after 10 time steps spent in a state
    - evaluates to FALSE for the first 9 steps, is TRUE every time after that

  - ***at(x, tick)***:
    - evaluates to TRUE only **once**, exactly after $x$ time steps spent in a state
    - evaluates to FALSE for the first $x-1$ time moments, is TRUE only once at the $x$-th moment, is FALSE after that

  - ***every(x, tick)***:
    - evaluates to TRUE periodically after $x$ time steps
    - evaluates to FALSE for the first $x-1$ time moments, is TRUE once at the $x$-th moment,
    then FALSE for the next $x-1$ time moments, then TRUE again, and so on

### Temporal logic

![Temporal Logic example [^TempLogic]](fig/Stateflow_TemporalLogic.png){width=70%}

[^TempLogic]: image from MATLAB docs
