# State Diagram

 A **state diagram** is a graphical representation of a system that shows its states and the transitions between them. It describes the behavior of a system by illustrating how it changes from one state to another in response to certain events or conditions. Each state represents a specific condition or mode of operation, and the transitions are typically triggered by events, actions, or conditions. State diagrams are commonly used in systems design, software engineering, and control systems to model the dynamic behavior of a system over time.

 
```plantuml
@startuml
title Total System Control Process

[*] --> Idle : System Initialized

Idle --> EStopCheck 
EStopCheck --> Idle : E-Stop Pressed
EStopCheck --> Start : E-Stop Released

Start --> Motor1Running : Motor 1 ON\nWait for Sensor Input

Motor1Running --> CheckSensor 
CheckSensor --> CheckSensor : Sensor Detects Nothing

CheckSensor --> IncreaseCounterA : Sensor Detects A
CheckSensor --> IncreaseCounterB  : Sensor Detects B

IncreaseCounterA --> Motor2Right : Sensor Detects A
IncreaseCounterB --> Motor2Left  : Sensor Detects B

Motor2Right --> Idle : Motor 2 Stops when Conveyor empty
Motor2Left --> Idle : Motor 2 Stops when Conveyor empty

ResetCheck --> CounterReset : Reset Button Pressed
ResetCheck --> Motor1Running : No Reset

CounterReset --> Motor1Running : Counter Reset

Stop --> Idle : System Stopped all motors of   

@enduml
```