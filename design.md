QUESTION 1:

**P (Performative Measure)** - Reach Kisumu safely, minimize travel time and distance, reduce fuel consumption, obey traffic rules, avoid collisions, and deliver cargo without damage.\
**E (Environment)** - Kenya’s highway network\
**A (Actuators)** - Steering system, accelerator, brakes, gear controls, indicators and other vehicle-control mechanisms.
GPS for location, cameras for road signs and lane markings\
**S (Sensors)** - GPS for location, cameras for road signs and lane markings, weather sensors, road-condition sensors, speedometer and wheel sensors\

Agent Environments\
1. Fully observable vs. partially observable\
**Partially observable**\
The trailer cannot obtain complete information about everything happening on the highway at every moment. Therefore, the environment is partially observable because the agent receives incomplete information about the current state of the environment.\
2. Deterministic vs. stochastic\
**Stochastic**\
The outcome of the trailer's actions cannot always be predicted with certainty. i.e. Braking may not stop the trailer immediately, especially on a slippery road and traffic conditions may change unexpectedly.\
3. Episodic vs. sequential\
**Sequential**\
The trailer's current actions affect its future states and decisions. An example being choosing a route through Nakuru affects the remaining journey. Therefore, the environment is sequential because each action influences subsequent actions and the eventual arrival at Kisumu.\
4. Static vs. dynamic\
**Dynamic**\
The highway environment changes while the trailer is making decisions, i.e. other vehicles continue moving, weather and road conditions may change.\
5. Single agent vs. multi-agent\
**Multi-agent**\
The trailer operates alongside other vehicles, pedestrians, cyclists, and traffic enforcement officers.

