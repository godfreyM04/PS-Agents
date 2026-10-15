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
In AI problem formulation, abstraction simplifies the physical world by stripping away non-essential micro-details—such as individual potholes, street lights, speed bumps, local fuel stations, and transient traffic congestion. 

For our trailer transport agent operating across Kenya's highway network (connecting Nairobi, the Central Highlands, the Rift Valley, and the Lake Victoria Basin), the search space is defined strictly by treating:
* **States (Nodes):** Major towns and cities (e.g., Nairobi, Naivasha, Nakuru, Kericho, Kisumu).
* **Actions / Edges:** Major highway segments connecting these urban centers (e.g., Nairobi–Nakuru Highway A104, Mau Summit–Kericho Road B1).

---

### 2.2 Directed Graph of Kenya's Highway Network
The directed graph models the highway segments, directions, and accurate road distances verified via Google Maps.

| From Node (Current Town) | To Node (Next Town) | Highway Segment / Route | Distance (km) |
| :--- | :--- | :--- | :--- |
| **Nairobi** | Naivasha | Nairobi–Nakuru Highway (A104) | ~88 km |
| **Naivasha** | Nakuru | Nairobi–Nakuru Highway (A104) | ~70 km |
| **Nakuru** | Kericho | Mau Summit–Kericho Road (B1) | ~107 km |
| **Kericho** | Kisumu | Kericho–Kisumu Highway (B1) | ~83 km |
| **Nakuru** | Eldoret | Nakuru–Eldoret Highway (A104) | ~128 km |
| **Eldoret** | Kisumu | Eldoret–Kisumu Highway (A104/B1) | ~117 km |

---

### 2.3 Search Tree Expansion (Initial State: Nairobi to Goal State: Kisumu)
The search tree expands outward from the initial state, tracking cumulative path costs (distances in kilometers) along each possible route branch.

```text
Level 0 (Initial State):
└── Nairobi [Cost: 0 km]
    ├── Naivasha [Cumulative Cost: 88 km]
    │   └── Nakuru [Cumulative Cost: 158 km]
    │       ├── Kericho [Cumulative Cost: 265 km]
    │       │   └── Kisumu [GOAL STATE] [Cumulative Cost: 348 km]
    │       └── Eldoret [Cumulative Cost: 286 km]
    │           └── Kisumu [GOAL STATE] [Cumulative Cost: 403 km]