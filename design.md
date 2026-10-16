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

```
Question 3:

## 3. Optimal Path Using Distance as Path Cost

The path cost function is given by:
$$g(n) = \sum_{i=1}^{k} c(s_{i-1}, a_i, s_i)$$
where $c(s_{i-1}, a_i, s_i)$ denotes the distance between adjacent nodes/towns as given by Google Maps

### 3.1 Possible routes from Nairobi to Kisumu
|Route|Route Sequence|Cumulative Distance Calculation in $km$|Path Cost($g(n)$) 
| :--- | :--- | :--- | :--- |
|**ROUTE1: (via Kericho)**|Nairobi -> Naivasha -> Nakuru -> Kericho -> Kisumu|$88 + 70 + 107 + 83$|**$348 km$**|
|**ROUTE 2: (via Eldoret)**|Nairobi -> Naivasha -> Nakuru -> Eldoret -> Kisumu|$88 + 70 + 128 + 117$|**$403 km$**|

### 3.2 Uniform Cost Search (Dijkstra's algorithm)
Guided by **Djikstra's algorithm** to find the optimal path:

#### Initialisation:
* Current node: **None** 
* Univisited nodes: {Nairobi, Naivasha, Nakuru, Kericho, Eldoret, Kisumu}
* Visited nodes: {}

| Node | Shortest Distance | Previous Node |
| :--- | :--- | :--- |
| Nairobi | 0 km | - |
| Naivasha | $\infty$ | - |
| Nakuru | $\infty$ | - |
| Kericho | $\infty$ | - |
| Eldoret | $\infty$ | - |
| Kisumu | $\infty$ | - |

#### **Iteration 1**
* Current node: **Nairobi**(Initial state)
* Unvisited nodes: {Naivasha, Nakuru, Kericho, Eldoret, Kisumu}
* Visited nodes: {Nairobi}

**We find the distance between Nairobi and unvisited neighbour nodes. Therefore, distance between Nairobi and Naivasha is given by $(0+88)$. Given that $88<\infty$, update shortest distance as $88km$**

| Node | Shortest Distance | Previous Node |
| :--- | :--- | :--- |
| Nairobi | 0 km | - |
| Naivasha | 88 km | Nairobi |
| Nakuru | $\infty$ | - |
| Kericho | $\infty$ | - |
| Eldoret | $\infty$ | - |
| Kisumu | $\infty$ | - |

#### **Iteration 2**
* Current node: **Naivasha**
* Unvisited nodes: {Nakuru, Kericho, Eldoret, Kisumu}
* Visited nodes: {Nairobi, Naivasha}

**For the second iteration, we calculated the distance between Nairobi and Nakuru given as $(88+70= 158 km)$. Since $158<\infty$ we update the shortest distance between Nairobi and Nakuru as $158 km$**

| Node | Shortest Distance | Previous Node |
| :--- | :--- | :--- |
| Nairobi | 0 km | - |
| Naivasha | 88 km | Nairobi |
| Nakuru | 158 km | Naivasha |
| Kericho | $\infty$ | - |
| Eldoret | $\infty$ | - |
| Kisumu | $\infty$ | - |

#### **Iteration 3**
* Current node: **Nakuru**
* Unvisited nodes: {Kericho, Eldoret, Kisumu}
* Visited nodes: {Nairobi, Naivasha, Nakuru}

* **Nakuru has 2 unvisited neighbours ie. Kericho and Eldoret**
* **For Kericho $158+107= 265km$. Since $265 km <\infty$, we update the shortest distance between Nairobi and Kericho as $265 km$**
* **For Eldoret $158+128= 286km$. Since $286 km <\infty$, we update the shortest distance between Nairobi and Eldoret as $286 km$**

| Node | Shortest Distance | Previous Node |
| :--- | :--- | :--- |
| Nairobi | 0 km | - |
| Naivasha | 88 km | Nairobi |
| Nakuru | 158 km | Naivasha |
| Kericho | 265 km | Nakuru |
| Eldoret | 286 km | Nakuru |
| Kisumu | $\infty$ | - |

#### **Iteration 4**
* Current Node: **Kericho** (Because the minimum cost distance between unvisited nodes was lower for Kericho)
* Unvisited nodes: {Eldoret, Kisumu}
* Visited nodes: {Nairobi, Naivasha, Nakuru, Kericho}

**Distance between unvisited neighbour Kisumu and Kericho is given by ($265+83 = 348km$). Since $348 km<\infty$, we update the shortest distance between Nairobi and Kisumu as 348km**

| Node | Shortest Distance | Previous Node |
| :--- | :--- | :--- |
| Nairobi | 0 km | - |
| Naivasha | 88 km | Nairobi |
| Nakuru | 158 km | Naivasha |
| Kericho | 265 km | Nakuru |
| Eldoret | 286 km | Nakuru |
| Kisumu | 348 km | Kericho |

#### **Iteration 5**
* Current Node: **Eldoret** (Minimum distance among unvisited nodes was lower for Eld 286km vs 348km)
* Unvisited nodes: {Kisumu}
* Visited nodes {Nairobi, Naivasha, Nakuru, Kericho, Eldoret}

**Kisumu is Eldoret's unvisited neighbour, thus ($286+117=403 km$) since $403>348$ we do not update the shortest distance between Nairobi and Kisumu; the table remains as is**

| Node | Shortest Distance | Previous Node |
| :--- | :--- | :--- |
| Nairobi | 0 km | - |
| Naivasha | 88 km | Nairobi |
| Nakuru | 158 km | Naivasha |
| Kericho | 265 km | Nakuru |
| Eldoret | 286 km | Nakuru |
| Kisumu | 348 km | Kericho |

#### **Iteration 6**
* Current node: **Kisumu** 
* Unvisited nodes: {}
* Visited nodes: {Nairobi, Naivasha, Nakuru, Kericho, Eldoret, Kisumu}

**Kisumu has no unvisited nodes and is our goal state we therefore mark it as visited and find the optimal path**

| Node | Shortest Distance | Previous Node |
| :--- | :--- | :--- |
| Nairobi | 0 km | - |
| Naivasha | 88 km | Nairobi |
| Nakuru | 158 km | Naivasha |
| Kericho | 265 km | Nakuru |
| Eldoret | 286 km | Nakuru |
| Kisumu | 348 km | Kericho |

#### **Constructing the optimal path**
We first start at **Kisumu** and find the previous node which provides the shortest distance as $348 km$ that is Kericho. Next, we look up Kericho and find its previous node as Nakuru. Next, we look up Nakuru and find its previous node as Naivasha. Then look up Naivasha and find its previous node as Nairobi.

Therefore the optimal path is given by: **Nairobi -> Naivasha -> Nakuru -> Kericho -> Kisumu** with a path cost of **$348km$**




