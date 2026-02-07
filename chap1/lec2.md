# AI Agents and Environments - Complete Notes

## Table of Contents
1. [Agent and Environment Basics](#agent-and-environment-basics)
2. [Key Terminology](#key-terminology)
3. [Rational Agents](#rational-agents)
4. [Performance Measures](#performance-measures)
5. [PEAS Description](#peas-description)
6. [Properties of Task Environments](#properties-of-task-environments)

---

## Agent and Environment Basics

### Fundamental Concept

**Analogy from Thermodynamics:**
```
Universe = System + Surroundings
AI World = Agent + Environment
```

- **Agent:** The machine, software, or robot we study
- **Environment:** Everything else around it

---

### What is an Agent?

**Definition:**
> "Anything that can be viewed as perceiving its environment through sensors and acting upon that environment through actuators"

**How Agents Work:**
```
Environment
    ↓ (Sensors perceive)
  Agent
    ↓ (Actuators act)
Environment (changed)
```

### Agent Components

**1. Sensors (Input)**
- Perceive information from environment
- Understand what's happening around

**Human Analogy:**
```
Human Sensors:
├── Eyes (vision)
├── Ears (hearing)
├── Nose (smell)
├── Tongue (taste)
└── Skin (touch)

5 senses to perceive environment
```

**Robot Example (Self-Driving Car):**
```
Robot Sensors:
├── Camera
├── Bluetooth
├── Infrared
├── Radar (small-level)
├── GPS
└── Other sensors
```

**2. Actuators (Output)**
- Take actions in environment
- React based on perceived information

**Human Analogy:**
```
Human Actuators:
├── Legs (movement)
├── Hands (manipulation)
├── Voice (communication)
└── Facial expressions (emotion)
```

**Robot Example (Self-Driving Car):**
```
Robot Actuators:
├── Accelerator
├── Brake
├── Steering wheel
├── Turn indicators
├── Horn
└── Lights
```

### Complete Agent Cycle

```
1. Sense Environment (via Sensors)
    ↓
2. Make Decision (based on information)
    ↓
3. Take Action (via Actuators)
    ↓
4. Environment Changes
    ↓
5. Sense Again (repeat cycle)
```

**Example: Self-Driving Car**
```
Sensors detect obstacle
    ↓
Decision: Should brake/turn/accelerate?
    ↓
Actuator: Press brake
    ↓
Environment: Car slows down
    ↓
Sensors: Detect new state
```

---

## Key Terminology

### 1. Percept

**Definition:**
> "What an AI agent (computer program or robot) senses and perceives at a specific moment"

**Explanation:**
- Whatever the agent understands at current time
- Through camera, radar, infrared, or any sensors
- Snapshot of current environment state

**Example:**
```
Time: 10:00 AM
Percept: Temperature = 40°C, Light = Bright, Obstacle = None
```

---

### 2. Percept Sequence

**Definition:**
> "The total history and record that an AI agent has sensed and perceived since it started operating"

**Explanation:**
- Complete history of all percepts
- Not just current state, but all past states
- Used for better decision making

**Example: Air Conditioner**
```
Current: Temperature = 24°C

Percept Sequence (History):
├── 1 hour ago: 45°C
├── 30 min ago: 34°C
├── 15 min ago: 28°C
└── Now: 24°C

Decision: Based on trend, reduce cooling
```

**Importance:**
> "AI agent's decisions and actions at any moment can be influenced by the entire sequence it has experienced so far"

**Key Point:**
- Current decision ≠ Based only on current state
- Current decision = Based on current state + complete history

---

### 3. Agent Function

**Definition:**
> "A rule or set of rules that determine what action an agent takes based on the percept sequence"

**Explanation:**
- Functions/rules that guide decision-making
- Maps percepts to actions
- Tells agent: Given this input, take this action

**Mathematical Representation:**
```
Agent Function: f(Percept Sequence) → Action
```

**Example:**
```
If temperature > 30°C → Turn on compressor
If temperature < 20°C → Turn off compressor
If 20°C ≤ temperature ≤ 30°C → Maintain current state
```

---

### 4. Agent Program

**Definition:**
> "A practical, real-world implementation of the agent function"

**Difference:**
- **Agent Function:** Theoretical concept/rules
- **Agent Program:** Actual code/software

**Analogy:**
```
Agent Function = Mathematical formula
Agent Program = Written code implementing that formula
```

**Example:**
```python
# Agent Program (Implementation)
def temperature_control(percept_sequence):
    current_temp = percept_sequence[-1]
    
    if current_temp > 30:
        return "turn_on_compressor"
    elif current_temp < 20:
        return "turn_off_compressor"
    else:
        return "maintain_state"
```

---

### Important Constraint

**Critical Rule:**
> "Agents can only base decisions on information they have perceived or sensed"

**Why This Matters:**

**Example: Self-Driving Car**
```
Scenario: Camera covered with mud during off-roading

Problem:
├── Camera cannot see
├── Sensors blocked
├── Cannot perceive environment
└── Result: Cannot drive safely

Conclusion: No perception = No intelligent action
```

**Key Insight:**
- Environment may have information
- But if agent cannot sense it → Cannot act on it
- Sensors are critical for agent operation

---

## Rational Agents

### Concept of Rationality

**Analogy to Systems:**

**Operating System:**
- Handles system on our behalf
- Manages resources
- **Always makes correct decisions**

**Government of India:**
- Manages country on behalf of citizens
- Handles resources
- **Should make correct decisions**

**Supreme Court:**
- Custodian of Constitution
- **Always acts lawfully**

**AI System:**
- Works in environment
- Manages tasks
- **Should act rationally, not randomly**

---

### Rational Agent Definition

**Definition:**
> "An AI entity that always chooses the best action based on its percept sequence and built-in knowledge"

**Key Characteristics:**

**1. Best Action Selection**
```
Rational Agent → Chooses Best Action (not random)
```

**2. Based on Complete Information**
```
Decision Based On:
├── Current percept
├── Percept sequence (history)
└── Built-in knowledge
```

**3. Expected Outcome**
```
Action → Maximizes expected performance measure
```

---

### Decision Making Process

**Three-Step Process:**

**Step 1: Rational (रेशनल)**
- Think logically and systematically
- Consider all available information

**Step 2: Correct (करेक्ट)**
- Choose the right action
- Based on rational analysis

**Step 3: Measure Performance**
- Evaluate how good the action was
- Use performance criteria

```
Rational Thinking → Correct Action → Measure Performance
```

---

### Example: Chess-Playing Agent

**Rational Decision Making:**

```
Current State: Board position analyzed

Agent Process:
├── 1. Consider all possible moves
├── 2. Evaluate each move's outcome
├── 3. Predict opponent's responses
└── 4. Select move that maximizes winning chances

Result: Best possible move selected
```

**Not Rational:**
- Random move selection
- Ignoring opponent's position
- Not considering consequences

---

## Performance Measures

### What is Performance Measure?

**Definition:**
> "Criteria or parameters to judge how good an agent's action was"

**Key Points:**
1. **Not fixed** for all tasks and agents
2. **Varies** based on specific task
3. **Essential** to have some evaluation criteria

---

### Designing Performance Measures

**Principle:**
> "Performance measures are designed on desired outcomes in environment, NOT on preconceived ideas about agent behavior"

**Focus On:**
- What we want to achieve in environment
- Actual results and outcomes
- Environmental changes

**Don't Focus On:**
- How agent should behave (our assumptions)
- Specific agent actions
- Predetermined methods

---

### Example: Self-Driving Car Performance Measures

**Performance Criteria:**

```
1. Ride Comfort
   └── Was the ride comfortable or bumpy?

2. Rule Compliance
   └── Were any traffic rules violated?

3. Safety
   └── Did anyone get hurt?
   └── Were pedestrians safe?

4. Fuel Efficiency
   └── What was the average mileage?

5. Time Efficiency
   └── Reached destination on time?
```

**Evaluation:**
```
If all criteria met → Good performance
If criteria not met → Poor performance
```

---

### Example: Air Conditioner Performance

**Scenario:** Room temperature control

**Performance Sequence:**
```
Initial State:
├── Room Temperature: 40°C
├── Target: 24°C
└── Action: Turn on AC full speed

After 15 minutes:
├── Temperature: 34°C
├── Evaluation: Improving, continue
└── Action: Keep compressor running

After 30 minutes:
├── Temperature: 28°C
├── Evaluation: Better, but not target
└── Action: Continue cooling

After 45 minutes:
├── Temperature: 24°C
├── Evaluation: Target achieved
└── Action: Reduce cooling

After 60 minutes:
├── Temperature: 22°C
├── Evaluation: Too cold
└── Action: Switch off compressor

After 70 minutes:
├── Temperature: 24°C
└── Action: Maintain balance
```

**Performance Measure:**
- How quickly reached target temperature?
- How stable is temperature maintenance?
- Energy efficiency

---

## PEAS Description

### What is PEAS?

**Acronym:**
```
P - Performance Measure
E - Environment
A - Actuators
S - Sensors
```

**Purpose:** Complete specification of an AI agent's task

**Importance:** Must write this in exams and documentation

---

### PEAS Components Explained

**1. Performance Measure**
- Criteria for success
- How to evaluate agent

**2. Environment**
- Where agent operates
- Task setting and context

**3. Actuators**
- Agent's action mechanisms
- How agent affects environment

**4. Sensors**
- Agent's perception mechanisms
- How agent observes environment

---

### Example 1: Self-Driving Taxi

**Performance Measure:**
```
✓ Safe journey
✓ Fast travel
✓ Legal driving (follow rules)
✓ Comfortable ride
✓ Maximize profit
✓ Fuel efficiency
```

**Environment:**
```
✓ Roads
✓ Other traffic
✓ Pedestrians
✓ Customers
✓ Weather conditions
```

**Actuators:**
```
✓ Steering wheel
✓ Accelerator
✓ Brake
✓ Signal/indicators
✓ Horn
✓ Display/screen
```

**Sensors:**
```
✓ Camera
✓ Sonar
✓ Speedometer
✓ GPS
✓ Odometer
✓ Accelerometer
✓ Engine sensors
✓ Keyboard/input devices
```

---

### Example 2: Chess-Playing Agent

**Performance Measure:**
```
✓ Win the game
✓ Checkmate opponent
✓ Minimize moves to win
```

**Environment:**
```
✓ Chess board (8x8 grid)
✓ 32 pieces (16 per player)
✓ Game rules
✓ Current board state
✓ Opponent's moves
```

**Actuators:**
```
✓ Move pieces
✓ Capture opponent pieces
✓ Display moves on screen
```

**Sensors:**
```
✓ Board position reader
✓ Opponent move detector
✓ Game state analyzer
```

---

### Example 3: Image Recognition System

**Performance Measure:**
```
✓ Accuracy of recognition
✓ Speed of processing
✓ Correct object identification
```

**Environment:**
```
✓ Digital images
✓ Various object types
✓ Different lighting conditions
✓ Image database
```

**Actuators:**
```
✓ Display results
✓ Label images
✓ Store classifications
```

**Sensors:**
```
✓ Image input device
✓ Camera
✓ Image file reader
```

---

### How to Use PEAS

**Practice Method:**
```
Write all four together:
P-E-A-S
P-E-A-S
P-E-A-S

Helps recall in exams!
```

**For Any Agent:**
1. Identify performance goals
2. Define environment
3. List possible actions
4. List sensing capabilities

---

## Properties of Task Environments

### Overview

Task environments can be classified based on different properties. Understanding these helps design appropriate agents.

---

### 1. Fully Observable vs Partially Observable

**Fully Observable:**
- **Definition:** All aspects of environment are visible to agent
- **Agent can:** See complete state
- **Decision making:** Based on complete information

**Example: Chess Game**
```
✓ Can see entire board
✓ Can see all pieces
✓ Can see opponent's pieces
✓ Complete information available
```

**Partially Observable:**
- **Definition:** Some aspects of environment are not visible
- **Reasons:**
  - Noisy/inaccurate sensors
  - Sensors damaged or blocked
  - Missing sensor data

**Example: Self-Driving Car with Muddy Camera**
```
✗ Camera covered with mud
✗ Cannot see clearly
✗ Partial information only
✗ Some sensors not working
```

**Unobservable:**
- All sensors failed
- Cannot perceive environment at all
- Agent is "blind"

```
Classification:
├── Fully Observable (complete data)
├── Partially Observable (some data missing)
└── Unobservable (no data)
```

---

### 2. Single-Agent vs Multi-Agent

**Single-Agent Environment:**
- Only one agent operating
- Agent's success depends only on own actions
- No interaction with other agents

**Examples:**
```
✓ Solitaire game (Minesweeper)
✓ Snake game on mobile
✓ Crossword puzzle solving
✓ Independent problem solving
```

**Multi-Agent Environment:**
- Multiple agents in same environment
- Agent's success depends on other agents too
- Interaction and competition/cooperation

**Examples:**
```
✓ Chess (two players)
✓ Self-driving cars on road (multiple cars)
✓ Soccer game (multiple players)
✓ Poker (multiple players)
```

**Key Difference:**
```
Single-Agent:
Your performance = Your actions + Environment

Multi-Agent:
Your performance = Your actions + Other agents' actions + Environment
```

**Example: Chess**
```
Your Move: Excellent strategy
↓
Opponent's Move: Better counter-strategy
↓
Result: Your position weakened
↓
Conclusion: Success depends on both agents
```

**Example: Self-Driving Taxi**
```
Your Driving: Perfect
↓
Other Car: Hits you
↓
Result: Collision
↓
Conclusion: Must avoid collision despite other agents
          Must maximize performance of all agents
```

---

### 3. Deterministic vs Stochastic (Non-Deterministic)

**Deterministic Environment:**
- **Definition:** Next state completely determined by current state and action
- **Agent knows:** Exactly what will happen after action

**Example: Chess**
```
Current State: Knight at position A1
Action: Move knight to B3
Result: Knight will be at B3 (100% certain)

You know exactly what will happen
```

**Stochastic/Non-Deterministic Environment:**
- **Definition:** Next state is not fully predictable
- **Agent doesn't know:** Exactly what will happen
- **Involves:** Uncertainty, randomness

**Example: Card Games**
```
Current State: You have cards in hand
Action: Draw next card
Result: Unknown - could be any card

You don't know what card you'll get
```

**Another Example: Playing Cards**
```
Card is face-down (blank)
↓
You must unfold it
↓
You don't know what number/suit it is
↓
Uncertainty in outcome
```

```
Comparison:
Deterministic: Action A → Predictable Result B
Stochastic: Action A → Unpredictable Result (B or C or D...)
```

---

### 4. Episodic vs Sequential

**Episodic Environment:**
- Agent's experience divided into episodes
- Each episode is **independent**
- Past episodes don't affect current episode

**Example: Image Recognition**
```
Episode 1: Recognize image of cat
Episode 2: Recognize image of dog
Episode 3: Recognize image of car

Success in Episode 2 is INDEPENDENT of Episode 1
Each new image is fresh start
```

**Sequential Environment:**
- Current decisions depend on previous actions
- Past affects future
- Sequence matters

**Example: Chess Game**
```
Move 1: Pawn forward
    ↓
Move 2: Options LIMITED by Move 1
    ↓
Move 3: Options LIMITED by Moves 1 & 2
    ↓
...
    ↓
Move 20: Winning/losing chances HEAVILY depend on all previous moves
```

```
Comparison:
Episodic: Each task is fresh, independent
Sequential: Current state depends on history
```

**Real-World Examples:**
```
Episodic:
├── Answering individual questions
├── Recognizing separate images
└── Independent problem solving

Sequential:
├── Chess game
├── Stock trading (today's decision affects tomorrow)
└── Navigation (each turn affects where you can go next)
```

---

### 5. Static vs Dynamic

**Static Environment:**
- Environment **doesn't change** while agent is deciding
- Agent can take time to think
- No time pressure

**Examples:**
```
✓ Chess (your turn)
✓ Tic-Tac-Toe (your turn)
✓ Crossword puzzle

When it's your turn:
├── Board state is frozen
├── You can think for hours
├── Environment waits for you
└── Make decision at your pace
```

**Dynamic Environment:**
- Environment **changes** while agent is deciding
- Time matters
- Can't wait forever

**Example: Stock Trading**
```
Morning 9:00 AM:
├── Market opens
├── You want to buy Tata Motors shares
├── Current price: ₹100
└── You think: "Let me research for 1 hour"

1 Hour Later (10:00 AM):
├── You: "Okay, let's buy now"
├── Current price: ₹105
└── Environment changed while you were deciding!

Result: Lost opportunity, higher price
```

**Detailed Stock Example:**
```
Decision Process:
├── Shortlisted: Tata Motors
├── Plan: Research for 1 hour
├── Reason: Annual report coming, positive sentiment
└── Expected: Will buy after research

Problem:
├── While researching (1 hour)
├── Share price increased 5%
├── Market didn't wait
└── Environment was dynamic
```

```
Comparison:
Static: Environment frozen → Think calmly → Act
Dynamic: Environment changing → Quick decision → Act fast
```

---

### 6. Discrete vs Continuous

**Discrete Environment:**
- **Finite** number of actions
- **Countable** states and actions
- Clear, distinct options

**Example: Chess**
```
Total squares: 64
At any position:
├── Possible moves: Maybe 5-10
├── Not infinite moves
└── Must choose from limited options

Can't make 1 million moves
Can't move piece to infinite positions
```

**Continuous Environment:**
- **Infinite** or very large number of actions
- Actions can vary continuously
- Unlimited possibilities

**Example: Self-Driving Car**
```
Steering:
├── Can turn 1 degree
├── Can turn 1.5 degrees
├── Can turn 1.732 degrees
└── Can turn any angle (infinite possibilities)

Speed:
├── Can go 100 km/h
├── Can go 100.5 km/h
├── Can go 100.001 km/h
└── Can go any speed (infinite possibilities)
```

**Another Example:**
```
Discrete: Moving chess piece
├── 64 squares total
├── Limited valid moves
└── Countable options

Continuous: Self-driving car steering
├── Can turn at any angle
├── Can accelerate to any speed
├── Can brake with any force
└── Infinite variations
```

```
Comparison:
Discrete: Finite, countable actions
Continuous: Infinite, measurable actions
```

---

### 7. Known vs Unknown

**Known Environment:**
- Agent **knows** the rules
- Agent **knows** how environment works
- Agent **knows** what actions lead to what outcomes

**Example: Chess**
```
Agent knows:
✓ All rules of chess
✓ How each piece moves
✓ What is checkmate
✓ Legal vs illegal moves
✓ Winning conditions
```

**Unknown Environment:**
- Agent **doesn't know** all rules
- Must learn through experience
- Uncertainty about outcomes

**Example: Navigating New City**
```
Self-Driving Car enters city for first time:

Unknown factors:
✗ Road layout
✗ Traffic patterns
✗ Local driving rules
✗ Best routes

Must navigate anyway:
├── No preset rules for this city
├── Must explore and learn
├── Trial and error approach
└── Keep traversing and learning
```

**Comparison:**
```
Known: Rules are clear → Apply rules → Optimal decision
Unknown: No clear rules → Explore → Learn → Adapt
```

---

## Properties Summary Table

| Property | Type 1 | Type 2 | Example Type 1 | Example Type 2 |
|----------|--------|--------|----------------|----------------|
| **Observability** | Fully Observable | Partially Observable | Chess (see all) | Muddy camera (see partial) |
| **Agents** | Single-Agent | Multi-Agent | Solitaire game | Chess game |
| **Determinism** | Deterministic | Stochastic | Chess moves | Card drawing |
| **Episodes** | Episodic | Sequential | Image recognition | Chess game |
| **Change** | Static | Dynamic | Chess (your turn) | Stock trading |
| **Actions** | Discrete | Continuous | Chess moves | Car steering |
| **Knowledge** | Known | Unknown | Chess rules | New city navigation |

---

## Complete Examples

### Example 1: Chess Agent (Complete PEAS + Properties)

**PEAS Description:**
```
P - Win game, checkmate opponent
E - Chess board, pieces, rules, opponent
A - Move pieces, capture
S - Board position, opponent moves
```

**Properties:**
```
✓ Fully Observable (can see entire board)
✓ Multi-Agent (two players)
✓ Deterministic (moves have known outcomes)
✓ Sequential (each move affects next)
✓ Static (board doesn't change during your turn)
✓ Discrete (finite number of moves)
✓ Known (rules are clear)
```

---

### Example 2: Self-Driving Taxi (Complete PEAS + Properties)

**PEAS Description:**
```
P - Safe, fast, legal, comfortable, profitable
E - Roads, traffic, pedestrians, customers
A - Steering, accelerator, brake, signals
S - Camera, radar, GPS, speedometer
```

**Properties:**
```
? Partially Observable (sensors can fail, limited view)
✓ Multi-Agent (other cars, pedestrians)
? Stochastic (other drivers' actions unpredictable)
✓ Sequential (each turn affects route)
✓ Dynamic (traffic changes constantly)
✓ Continuous (infinite steering angles, speeds)
? Unknown (new roads, changing conditions)
```

---

### Example 3: Image Recognition System

**PEAS Description:**
```
P - Accurate recognition, fast processing
E - Digital images, various objects
A - Display results, label images
S - Camera, image reader
```

**Properties:**
```
✓ Fully Observable (can see entire image)
✓ Single-Agent (no other agents)
✓ Deterministic (same image → same result)
✓ Episodic (each image independent)
✓ Static (image doesn't change)
✓ Discrete (finite pixel values)
✓ Known (image processing rules known)
```

---

## Key Takeaways

### Essential Concepts

**1. Agent = Sensors + Decision Making + Actuators**
```
Perceive → Think → Act → Environment Changes → Perceive Again
```

**2. Rational Agent**
- Always chooses best action
- Based on percept sequence and knowledge
- Maximizes performance measure

**3. PEAS is Critical**
- Must specify for any agent
- Complete task description
- **Remember:** Performance, Environment, Actuators, Sensors

**4. Environment Properties Matter**
- Determine agent design
- Affect complexity
- Guide decision-making approach

---

### Decision-Making Flow

```
Environment State
    ↓
Sensors perceive (Percept)
    ↓
Build Percept Sequence (History)
    ↓
Agent Function (Rules)
    ↓
Agent Program (Implementation)
    ↓
Choose Action (Rational choice)
    ↓
Actuators execute
    ↓
Environment changes
    ↓
Measure Performance
    ↓
Repeat
```

---

### Exam Tips

**Must Remember:**
1. **PEAS** - Write P-E-A-S multiple times for practice
2. **Seven Properties** - Know all classifications
3. **Examples** - Chess, Self-driving car, Image recognition
4. **Definitions** - Percept, Percept Sequence, Agent Function, Agent Program

**Common Questions:**
- Define rational agent
- Give PEAS description for [scenario]
- Classify environment based on properties
- Explain difference between percept and percept sequence

---

## Quick Reference

### Agent Components
- **Sensors:** Eyes of agent (input)
- **Actuators:** Hands of agent (output)
- **Agent Function:** Brain of agent (decision rules)
- **Agent Program:** Implementation of brain (code)

### Environment Types (7 Properties)
1. Observable: Full / Partial / None
2. Agents: Single / Multi
3. Determinism: Deterministic / Stochastic
4. Episodes: Episodic / Sequential
5. Change: Static / Dynamic
6. Actions: Discrete / Continuous
7. Knowledge: Known / Unknown

### Performance Measures
- Based on **desired outcomes**
- Not on **agent behavior assumptions**
- Varies by task
- Essential for evaluation
