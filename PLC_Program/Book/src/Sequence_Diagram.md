# Sequence Diagram

```plantuml
@startuml
title Total System Control Sequence Diagram

actor User
participant EStop
participant StartStopButton
participant Sensor1
participant Sensor2
participant Motor1
participant Motor2
participant CounterA
participant CounterB
participant ResetButton

User -> StartStopButton : Press Start
StartStopButton -> EStop : Check E-Stop
EStop --> StartStopButton : E-Stop Released

StartStopButton -> Motor1 : Turn ON Motor 1
Motor1 -> Sensor1 : Wait for Sensor 1 (Detect A or B)

Sensor1 -> Motor1 : No Object Detected
Motor1 --> Sensor1 : Continue Waiting

Sensor1 -> Motor1 : Object Detected (A or B)
Sensor1 -> CheckSensor : Check if A or B

CheckSensor -> IncreaseCounterA : Sensor Detects A
CheckSensor -> IncreaseCounterB : Sensor Detects B

IncreaseCounterA -> CounterA : Increment Counter A
IncreaseCounterB -> CounterB : Increment Counter B

IncreaseCounterA -> Motor2 : Turn ON Motor 2 Right
IncreaseCounterB -> Motor2 : Turn ON Motor 2 Left
Motor2 -> Motor1 : Turn of Motor 1 after 4 seconds 

Motor2 -> Sensor2 : Wait for Sensor 2 (Detect Conveyor Empty)
Sensor2 -> Motor2 : Conveyor Empty, Turn OFF Motor 2

Motor1 -> Sensor1 : Continue Running, Wait for Next Object

User -> ResetButton : Press Reset
ResetButton -> CounterA : Reset Counter A
ResetButton -> CounterB : Reset Counter B

User -> StartStopButton : Press Stop
StartStopButton -> StartStopButton : Switch to Stop Mode
StartStopButton -> Motor1 : Turn OFF Motor 1
StartStopButton -> Motor2 : Turn OFF Motor 2

EStop -> StartStopButton : E-Stop Pressed
StartStopButton -> StartStopButton : Switch to Stop Mode
StartStopButton -> Motor1 : Turn OFF Motor 1
StartStopButton -> Motor2 : Turn OFF Motor 2

@enduml
```

A sequence diagram is a type of interaction diagram in Unified Modeling Language (UML) that illustrates how processes or objects interact with each other over time in a specific scenario. It shows the sequence of messages exchanged between different elements (such as objects, classes, actors, etc.) in the system and the order in which these interactions occur.

**Key elements of a sequence diagram:**
1. Actors/Participants: Represent the objects, people, or systems involved in the interaction. They are placed horizontally at the top of the diagram.
2. Lifelines: Vertical dashed lines that represent the life span of the participants during the interaction. Each participant has its own lifeline.
3. Messages: Arrows between participants that show the interaction or communication. These messages can represent method calls, signals, or responses.
4. Activations: Rectangles on a lifeline showing the period during which the participant is performing a task (processing time).
5. Time Flow: Time progresses from top to bottom. Interactions closer to the top occur earlier than those lower down.
   
**Purpose:**
- To visualize how different parts of a system collaborate in a particular scenario.
- To capture the chronological order of interactions and processes in a system.
- To model real-time systems or systems where the timing and sequence of events are critical.
  
**Use cases:**
- Describing the flow of logic in use cases or functions.
- Showing how objects and components communicate in distributed systems.
- Demonstrating how external actors (users or other systems) interact with a system.

**Summary**

In summary, a sequence diagram is a useful tool for capturing and understanding dynamic behavior and interactions in a system over time.