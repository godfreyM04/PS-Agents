QUESTION 1:

P (Performative Measure) - Reach Kisumu safely, minimize travel time and distance, reduce fuel consumption, obey traffic rules, avoid collisions, and deliver cargo without damage.\
E (Environment) - Kenya’s highway network.\
A (Actuators) - Steering system, accelerator, brakes, gear controls, indicators and other vehicle-control mechanisms.
GPS for location, cameras for road signs and lane markings.\
S (Sensors) - GPS for location, cameras for road signs and lane markings, weather sensors, road-condition sensors, speedometer and wheel sensors.

Agent Environments
1. Fully observable vs. partially observable
Partially observable
The trailer cannot obtain complete information about everything happening on the highway at every moment. Therefore, the environment is partially observable because the agent receives incomplete information about the current state of the environment.
2. Deterministic vs. stochastic
Stochastic
The outcome of the trailer's actions cannot always be predicted with certainty. i.e. Braking may not stop the trailer immediately, especially on a slippery road and traffic conditions may change unexpectedly.
3. Episodic vs. sequential
Sequential
The trailer's current actions affect its future states and decisions. An example being choosing a route through Nakuru affects the remaining journey. Therefore, the environment is sequential because each action influences subsequent actions and the eventual arrival at Kisumu.
4. Static vs. dynamic
Dynamic
The highway environment changes while the trailer is making decisions, i.e. other vehicles continue moving, weather and road conditions may change.
5. Single agent vs. multi-agent
Classification: Multi-agent
The trailer operates alongside other vehicles, pedestrians, cyclists, and traffic enforcement officers.

## Question 2: Directed Graph, Search Tree & Abstraction
### 2.1 Concept of Abstraction
In AI problem formulation, **abstraction** simplifies the real world by stripping away non-essential micro-details (such as individual potholes, street lights, speed bumps, or fuel stops) \[1, 4\]. The search space is defined strictly by treating **towns/cities as states (nodes)** and **highway segments as actions/edges** \[1, 5\].
### 2.2 Directed Graph of Kenya's Highway Network
| From Node (Town) | To Node (Town) | Highway Segment | Distance (km) |
| :---- | :---- | :---- | :---- |
| Nairobi | Naivasha | Nairobi–Nakuru Highway (A104) | \~90 km |
| Naivasha | Nakuru | Rift Valley Highway (A104) | \~70 km |
| Nakuru | Kericho | Mau Summit–Kericho Road (B1) | \~80 km |
| Kericho | Kisumu | Kericho–Kisumu Highway (B1) | \~85 km |
| Nakuru | Eldoret | Nakuru–Eldoret Highway (A104) | \~130 km |
| Eldoret | Kisumu | Eldoret–Kisumu Highway (A104/B1) | \~120 km |
### 2.3 Search Tree Expansion (Initial State: Nairobi → Goal State: Kisumu)
Level 0 (Initial State):

└── Nairobi \[Cost: 0 km\]

    ├── Naivasha \[Cumulative Cost: 90 km\]

    │   └── Nakuru \[Cumulative Cost: 160 km\]

    │       ├── Kericho \[Cumulative Cost: 240 km\]

    │       │   └── Kisumu \[GOAL STATE\] \[Cumulative Cost: 325 km\]

    │       └── Eldoret \[Cumulative Cost: 290 km\]

    │           └── Kisumu \[GOAL STATE\] \[Cumulative Cost: 410 km\]