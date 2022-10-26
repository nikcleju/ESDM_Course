## IX. Scheduling basics

### Scheduling

- Scheduling = the process of arranging the execution of a set of **tasks** which need
to be run on the same processing device, 

  - i.e. decide which task is run when, for how long, etc.

- Encountered in multi-tasking systems


### Task

- A **task** is a set of operations which have:

  - release time: earliest time when it can be run
  - **start time**: actual starting time
  - **finish time**: actual ending time
  - execution time: actual running time, excluding any interruptions
  - **deadline**: latest time by which a task must be completed
  
- Tasks may be interrupted by higher priority tasks, when priorities are defined

- Tasks may be periodic (e.g. every 10ms) or aperiodic

- Figure  

### Types of scheduling

Tasks can be:

- periodic / aperiodic

- independent / dependent

Scheduling can be:

- preemtive / non-preemptive

- static / dynamic



### Rate Monotonic Scheduling

### Earliest Deadline First
