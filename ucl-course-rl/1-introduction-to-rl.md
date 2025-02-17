# Outline
1. About Reinforcement Learning
2. The Reinforcement Learning Problem
3. Inside an RL Agent
4. Problems with Reinforcement Learning
# About Reinforcement Learning
### Many Faces of Reinforcement Learning
![Many Faces of RL](01-many-faces-of-rl.png)

1. **Reinforcement Learning as a Cross-Disciplinary Field**
    
    - RL is a central topic that connects various scientific domains.
    - It is fundamentally about **decision-making**, making it applicable across multiple areas.
2. **Connections to Other Fields:**
    
    - **Computer Science:** RL is a subset of **machine learning**, where algorithms learn to make optimal decisions based on rewards.
    - **Engineering:** RL overlaps with **optimal control**, which focuses on determining the best sequence of actions to achieve desired outcomes.
    - **Neuroscience:**
        - The **dopamine system** in the human brain closely mirrors RL algorithms.
        - Research suggests that RL principles underlie human decision-making processes.
    - **Psychology:**
        - Concepts like **classical conditioning** (Pavlov) and **operant conditioning** (Skinner) align with RL, explaining how behaviors emerge through reinforcement.
    - **Mathematics:** RL has strong ties to **operations research** and **optimal control theory**, where mathematical models optimize decisions.
    - **Economics:**
        - RL is linked to **game theory**, **utility theory**, and **bounded rationality**, which explore decision-making strategies under constraints.
3. **The Fundamental Nature of Reinforcement Learning**
    
    - RL is a **universal framework for decision-making** across disciplines.
    - The study of RL helps understand how both artificial systems and biological organisms make decisions to maximize rewards.

### Branches of Machine Learning
![Branches of Machine Learning](02-branches-of-ml.png)
### Characteristics of Reinforcement Learning

1. **No Supervisor in Reinforcement Learning**
    
    - Unlike **Supervised Learning**, where a model is provided with labeled data that explicitly states the correct answer, RL lacks direct supervision.
    - Instead of receiving explicit guidance on what action to take, an RL agent learns through **trial and error**, exploring the environment autonomously.
    - The agent receives only a **reward signal** that indicates whether an action was beneficial or harmful but does not specify the best possible action.
    - Example: Instead of being told “Turn left,” an agent might receive a reward of **+3 points** for a correct move or **-10 points** for a mistake, but it has to figure out why.
2. **Delayed Feedback**
    
    - In **Supervised Learning**, feedback is immediate—errors in prediction are corrected instantly based on labeled data.
    - In **RL**, feedback (i.e., rewards or penalties) may come **many steps later**, making it harder to associate actions with their consequences.
    - Example: A chess-playing RL agent might make a move that seems good at the moment but only realizes much later that it was a mistake when it leads to checkmate.
3. **Sequential Decision-Making**
    
    - Unlike **Supervised Learning**, where each data point is independent (**IID - Independently and Identically Distributed**), RL involves **sequential** decisions where previous actions affect future ones.
    - The agent interacts with the environment **over time**, making decisions that influence subsequent states.
    - Example: A self-driving car must continuously make decisions about steering, acceleration, and braking, where each choice affects its future state.
4. **Non-IID Data and Correlated Observations**
    
    - In **Supervised Learning**, data is typically assumed to be IID (independent of other samples).
    - In RL, however, **each observation is correlated with previous ones**.
    - Example: If a robot is walking, what it sees in one moment is closely related to what it sees in the next second. This makes it difficult to use traditional learning assumptions.
5. **Agent Actively Influences the Data It Receives**
    
    - Unlike a passive machine learning model that learns from a fixed dataset, an RL agent **actively changes its environment** by taking actions.
    - The data it encounters depends on **what it has done previously**.
    - Example: If a robot moves to a different side of a room, it will see different objects, receive different rewards, and gather a **different dataset** from what it would have seen had it stayed in place.
6. **Active Learning and Optimization Over Time**
    
    - RL involves **active learning**, where the agent must explore different strategies before finding the most optimal one.
    - Instead of simply classifying images or predicting values, RL agents must **continuously improve** through experience, refining their strategy based on rewards received over time.
    - Example: A video game AI might initially make random moves but gradually learns the best tactics to maximize its score.
### Examples of Reinforcement Learning

1. **Helicopter Stunt Maneuvers:**
    
    - A helicopter performs complex stunts based on reinforcement learning.
    - There is no immediate feedback after every move, but success is determined at the end of the maneuver.
    - Crashing is considered a failure, reinforcing the need for precise learning.
2. **Backgammon AI Success:**
    
    - Jerry Taro’s RL model defeated the human world champion in Backgammon.
    - The AI learned to play by repeated trial and error, gradually improving its strategy.
3. **Investment Portfolio Management:**
    
    - An RL model makes real-time investment decisions based on incoming data.
    - The reward function is based on maximizing financial returns over time.
    - The model learns optimal investment strategies through experience.
4. **Power Station Control:**
    
    - RL optimizes control over a power station’s operation.
    - Adjustments include torque control, battery ratios, and blade pitch in wind turbines.
    - The objective is to maximize energy efficiency and output over time.
5. **Humanoid Robot Walking:**
    
    - A robot learns to walk using RL, receiving feedback on whether it falls or moves forward.
    - It refines its movement strategy step by step to reach a goal (e.g., crossing a room).
6. **DeepMind’s Atari Game Agent:**
    
    - A single RL-based agent learns to play multiple Atari games at a superhuman level.
    - The program adapts to different game environments by learning optimal strategies.

**Audience Questions and Lecturer's Response**
1. Question about **simulation in Reinforcement Learning**
	- Audience: Whether the helicopter reinforcement learning system was trained in a simulated environment
	- Lecturer: Approach involved first building a model of the helicopter's behavior using real-world data. The learning was then done offline using this model before being applied to the actual helicopter.
2. Question about **Atari Game Learning**
	- Audience: Inquires the reinforcement learning agent playing Atari games
	- Lecturer: The agent learns purely through trial and error. It has no prior knowledge of the game rules and only receives video input and score feedback. Through reinforcement learning, it figures out how to maximize the score without human guidance.
- Question about **Knowledge transfer between Atari games**
	- Audience: Whether knowledge transfer strategies is applied between Atari games
	- Lecturer: Each game starts fresh, with no knowledge transfer.

Reinforcement learning (RL) is not just about games, though many applications involve games. RL concepts are broadly applicable beyond gaming.
# The Reinforcement Learning Problem
In reinforcement learning (RL), one of the core concepts is the **reward**, which is a numerical feedback signal (R<sub>t</sub>​) given at each time step 't' to indicate how well the agent is performing. The **agent's goal** is to maximize the total sum of rewards over time.

A fundamental hypothesis in RL is that **all goals can be framed as the maximization of expected cumulative reward**. This assumption underlies the entire RL framework, though it can be debated.

Key points:

- **Rewards define objectives**: If there are no intermediate rewards, the agent only receives a reward at the end of an episode.
- **Handling time-based goals**: If the goal is to achieve something in the shortest time, a common approach is to set a reward of -1 per time step, encouraging the agent to complete the task as quickly as possible.
### Examples of Rewards
![Examples of Rewards](03-rewards-example.png)

- **Helicopter Stunts:** Positive rewards are given for following the desired trajectory or staying within a small radius of the target position. A large negative reward is assigned for crashing.
    
- **Backgammon:** No intermediate rewards are provided during the game. Only at the end is a reward given: positive for winning, negative for losing. The agent must learn to maximize these end-game rewards by making good decisions throughout the game.
    
- **Investment Portfolio:** The reward signal is straightforward: profit (dollars or pounds). The goal is to maximize the total accumulated profit.
    
- **Power Station Control:** Positive rewards are given for each unit of power produced. Negative rewards are assigned for exceeding safety thresholds or violating regulations.
    
- **Robot Walking:** Positive rewards are given for forward motion (distance traveled). A large negative reward is assigned for falling over.
    
- **Atari Games:** Rewards are based on score changes at each step. A positive reward is given for an increase in score, and presumably a negative reward for a decrease (though this isn't explicitly stated).

While these problems appear different, **the goal is to create a unified machine learning framework to handle them all with the same agents and concepts**. The first step is understanding the reward signal, which is received at each time step.
### Sequential Decision Making
- **Unified Framework** → Even though problems (e.g., financial investment, helicopter control, chess) seem different, they share a common structure: **making a sequence of decisions to maximize future rewards**.
- **Maximizing Total Future Reward** → The core idea is to choose actions that result in the highest long-term benefit, not just immediate gain.
- **Planning Ahead & Long-Term Consequences** →
    - **Non-Greedy Strategy**: Short-term sacrifices (e.g., spending money, refueling, defensive chess moves) may lead to better outcomes in the future.
    - **Delayed Reward**: The effect of an action may not be immediate but could influence rewards later.

- **Examples in RL:**

	- **Financial Investment**: Spend money now → Gain profits later.
	- **Helicopter Control**: Take a detour to refuel → Avoid crashing later.
	- **Chess**: Sacrificing a piece now → Achieve a stronger position later.

- **Reinforcement Learning Concepts Covered:**

	- **Agent**: The decision-maker (e.g., investor, pilot, chess player).
	- **Environment**: The world in which the agent operates (e.g., stock market, helicopter physics, chessboard).
	- **Actions**: Choices available to the agent.
	- **Reward**: Feedback received for taking an action.
	- **Policy**: The strategy for choosing actions to maximize future rewards.
### Environments
![Agent and Environments](04-agent-environments.png)

**1. The Agent**

- The **agent** is represented as a **"big brain"** that we are designing.
- It is the entity that **makes decisions and takes actions** in an environment.
- The goal of RL is to **build an algorithm** that acts as the brain of the agent.
- The agent could be:
    - A **robot** that controls motors.
    - A **trading algorithm** deciding investments.
    - A **game-playing AI** making strategic moves.

**2. The Agent’s Inputs and Outputs**

At each step, the agent:

1. **Receives an observation** – This is a snapshot of the world (e.g., a camera feed for a robot, a game screen for an AI playing Atari).
2. **Receives a reward** – A signal indicating how well the agent is performing.
3. **Takes an action** – Decides the next step based on observations and past experiences.

The agent must **learn** to take the best possible actions to maximize future rewards.

**3. The Environment**

- The **environment** is everything **outside** the agent that it interacts with.
- It could be:
    - The **real world** for a self-driving car.
    - A **stock market simulation** for a trading AI.
    - A **game environment** for an Atari-playing AI.
- The environment **responds** to the agent's actions by:
    - Generating a new **observation**.
    - Providing a **reward** based on how good/bad the action was.

**4. The Feedback Loop in Reinforcement Learning**

The interaction between agent and environment happens in a continuous **feedback loop**:

4. The agent **observes** the environment.
5. It **decides** an action.
6. The action **affects** the environment.
7. The environment **responds** with a new observation and a reward.
8. The agent **learns** from this experience and updates its decision-making process.

This process is similar to **trial and error**, where the agent learns over time **which actions lead to higher rewards**.

**5. Example: Atari Game**

- If the agent is playing an Atari game:
    - It **observes** the screen (pixel data).
    - It **chooses an action** (e.g., move left, right, jump).
    - The game **updates** the screen and score.
    - The agent **receives** a reward based on performance.

The same loop applies to robotics, finance, and many AI applications.

**6. The Machine Learning Challenge in RL**

- RL is fundamentally about **learning from experience**.
- The **time series of observations, actions, and rewards** forms the dataset.
- The **learning algorithm** must extract patterns from this experience to improve future decisions.

This is the core problem of **reinforcement learning (RL)**—finding the best **policy** (strategy) to maximize rewards over time.



***Should rewards always be scalar values?***

The Debate: Scalar Rewards vs. Multiple Objectives

- In RL, the **reward hypothesis** states that a **single scalar reward** is sufficient to represent any goal the agent is optimizing for.
- However, in **real-world decision-making**, we often have **conflicting goals** (e.g., impressing your boss vs. keeping your partner happy).
- The question arises: **Do we always have to use a single scalar reward, or can we work with multiple, possibly conflicting objectives?**

RL Perspective: Everything Can Be Converted to a Scalar Reward

- Ultimately, an agent must **choose one action** at each step.
- To compare different choices, there must be a **common scale** to weigh them.
- This means that, even if multiple objectives exist, they must be **combined** into a single scalar value for decision-making.
- This process involves assigning **weights or trade-offs** to different objectives.

Example: Work vs. Personal Life Decision

- Suppose an agent (you) must choose between:
    1. **Working late** → Increases boss’s approval (career growth).
    2. **Spending time with a partner** → Strengthens relationship.
- You have to **assign a value to each outcome** and decide.
- If you prioritize work more at that moment, you might assign a **higher reward** to working late.
- This conversion of multiple factors into **one final decision metric** aligns with RL’s approach to scalar rewards.

**Key Takeaways**

- RL assumes that **all goals must ultimately be mapped to a single reward function**.
- Even if multiple competing goals exist, they must be **reduced** to a single scalar value to make decisions.
- This does not mean **multiple objectives don’t exist**, but rather that they need to be **aggregated** into one measure.
### State
![History and State](05-history-state.png)


- **History (H<sub>t</sub>)**
    
    - The history consists of all past observations, actions, and rewards.
    - The agent only has access to this history and must make decisions based on it.
- **Agent’s Decision Process**
    
    - The goal of RL is to develop an algorithm that maps history (H<sub>t</sub>) to an action (A<sub>t</sub>).
    - This mapping is crucial for determining the agent’s next move.
- **Environment’s Role**
    
    - The environment receives the agent’s action and updates itself based on history.
    - It emits a new observation and reward for the agent.
- **State Representation**
    
    - While history is essential, it becomes impractically large over time.
    - Instead of using raw history, we define a **state (S<sub>t</sub>)**, a compressed representation that captures all necessary information to decide what happens next.
    - This allows for more efficient learning and decision-making.

**Understanding Different Definitions of State**

![Environment State](06-environment-state.png)

**Environment State:**

The **environment state** refers to the underlying information within a system that determines what happens next. It represents the **true, complete description of the environment** at any given moment. However, this information is often **not fully observable** to the agent (e.g., a robot, AI system, or reinforcement learning agent).

**Key Characteristics of Environment State:**

1. **Defines What Happens Next:**
    
    - The environment has an internal state that dictates what will happen in the next step.
    - Example: In an Atari game emulator, the emulator has an **internal representation** of the game state, which determines how the game will progress based on inputs.
2. **Different Scenarios:**
    
    - If it's a **robot interacting with the real world**, the environment state consists of all physical variables determining what happens next.
    - In a **factory**, the environment state includes all process-related variables.
    - In a **game emulator**, the environment state includes internal variables controlling how the game plays out.
3. **Hidden from the Agent:**
    
    - The agent **does not have direct access** to the environment state.
    - Instead, the agent **only gets observations** from the environment (e.g., images, sensor data, rewards).
    - The agent must **infer** or **estimate** the true environment state from these observations.
4. **Not Always Useful for Decision-Making:**
    
    - Even if the agent could access the full environment state, not all of that information would be useful for making good decisions.
    - Example: If a robot is navigating a room, the atomic configuration of a rock in Australia is **not relevant** to its decision-making.
    - Instead, the agent should **focus on local observations** to determine the best action.

**Implications for Reinforcement Learning and AI**

- **Why is this distinction important?**
    
    - In reinforcement learning, an **agent** does not get to see the full environment state but instead **receives observations** and must learn to act based on them.
    - The **Markov Decision Process (MDP)** framework assumes that decisions are based on **states**, but in practice, we often work with **observations** instead.
- **Example in a Game (Atari Emulator):**
    
    - The **environment state** includes all variables inside the emulator that govern how the game runs.
    - The agent **only sees** pixel observations and score updates.
    - The challenge is to infer **the most relevant aspects of the environment state** based on limited observations.

The question asks:

_"**If you put a lot of agents together in the same environment, do you see any kind of self-organized behavior or patterns?**"_

In simpler terms:

- If you have **many independent "brains" (agents)** acting in the same world, will they start to organize themselves into patterns naturally, even without being explicitly told to do so?

For example:

- If you release **many birds into the sky**, will they start flying in synchronized patterns (like a flock)?
- If many people are walking in a busy street, do they start **unconsciously forming lanes** to avoid bumping into each other?

The answer:

- **Each agent sees the other agents as part of the "environment."**
    
    - Imagine you are one of the birds in a flock.
    - From **your** perspective, the other birds are just part of your surroundings.
    - You don’t think, "I am in a multi-agent system"; you just react to what’s around you.
- **This means that, formally, nothing needs to change in the way we describe the environment.**
    
    - If we define an environment for **one** agent, we don’t need to redefine everything just because multiple agents exist.
    - Each agent simply **interacts with whatever is around it**, including other agents.
- **But does self-organized behavior emerge?**
    
    - The answer is **yes, it can happen**.
    - There’s a lot of research on how multiple agents interacting in a shared environment can lead to **emergent behaviors**.
    - However, this particular discussion isn’t diving into those details.

**What Does This Mean for "Environment State"?**

> **"The environment state doesn't tell us anything useful for actually building algorithms because we don't see it."**

This means:

- In real-world AI, **we don’t have direct access to the full environment state**—just like how a person can’t see everything in the world at once.
- We **only see part of the environment** (this is called an **observation**).
- This is why AI agents have to make decisions based on **limited information**, not the full environment state.

![Agent State](07-agent-state.png)



1. **Definition of Agent State**:
    
    - It consists of numerical values stored within the algorithm.
    - It represents a summary of everything the agent has observed so far.
    - It is used to **determine the next action**.
2. **Role in Reinforcement Learning**:
    
    - The agent state is **not just a direct representation** of the environment.
    - Instead, it is **constructed** from past actions, observations, and rewards.
    - This constructed state is then used to inform decision-making.
3. **Decision-making Process**:
    
    - The **agent must decide** what information to keep and what to discard.
    - Different algorithms make different choices on how to process observations.
    - The agent's state is designed to **capture history in a meaningful way**.
4. **Function of History**:
    
    - The agent state is a function of history, meaning it is derived from all past interactions.
    - This function can be any transformation of historical data, determined by the **RL algorithm's design**.
    - The goal is to convert past interactions into a useful **vector representation** that guides future behavior.
5. **Final Objective**:
    
    - The agent state serves as a compact, informative summary.
    - It allows the RL algorithm to **make optimal action selections** based on past experiences.
    - Designing an effective state representation is critical to the **performance of RL models**.

![Information State](08-information-state.png)

- **Definition of Markov State:**
    
    - It is a representation of a state that contains all useful information from the history.
    - It follows an **information-theoretic** approach to ensure no past information is needed beyond the current state.
- **Markov Property:**
    
    - The probability of transitioning to the next state depends only on the current state, not on the entire history.
    - This means the **future is independent of the past, given the present**.
- **Implication of the Markov Property:**
    
    - One can **discard past states** and retain only the current state without losing any predictive power.
    - The **state acts as a sufficient statistic** for predicting future actions, observations, and rewards.
- **Compact Representation:**
    
    - Since the state fully characterizes future distributions, it provides a **concise** and **efficient** way to model a system without storing unnecessary historical data.


***Question:***

- The speaker acknowledges a point made earlier about rewards arriving many time steps after the action and observation.
- How this aligns with the approach of only retaining the previous time step while discarding the rest.

***Answer:***

- Even though rewards (good or bad outcomes) come later, we don’t need to remember everything that happened in the past.
- Instead, if we know the current state (S), it already contains all the important information we need to predict the future.
- Why Not Remember Everything?
	- It might seem like we are "throwing away" past information, but we aren’t.
    - The current state (S) acts as a summary of everything that has happened so far.
    - So, making decisions based on (S) can still lead to the best possible results.
- What’s Still Left to Figure Out?
	- Even though we now understand that using (S) is enough, we still have to learn how to make good decisions based on it.
	- The real challenge is figuring out what actions to take in each state to maximize rewards in the future.

***Question:***
- The speaker is explaining how the idea of "Markov state" fits with the example of a helicopter.
- A Markov state means that everything you need to predict the future is contained in the present moment—you don’t need to remember past events.

***Answer:***
- To control a helicopter, you need to know certain things about it at the current moment:
	- **Position** (where it is)
	- **Velocity** (how fast and in what direction it’s moving)
    - **Angular velocity** (how fast it’s rotating)
    - **Angular position** (its orientation)
    - **Wind direction** (external factors affecting movement)
- If you have all this information **right now**, you don’t need to remember where the helicopter was 10 minutes ago.
    - That past position is irrelevant because the future movement is fully determined by the current state and the forces acting on it (like wind).
- **Why You Don’t Need to Remember the Past (Markov Property)**
    - The present state contains **all the relevant information**.
    - Given the **current** position, velocity, and wind, you can accurately predict what happens next without needing old data.
- **What Happens If You Use an Imperfect State Representation?**
    - Suppose instead of knowing **position + velocity**, you only knew the **position**.
    - Now, you **can’t** predict the next movement correctly because you don’t know how fast the helicopter is already moving.
    - In this case, you would **need to look at past data** to estimate speed and momentum.
- **Key Takeaway:**
    
    - A **Markov state** is one where **the present state gives you all the necessary information to predict the future**.
    - If the state is incomplete, you would need to look at past events, making it **non-Markov**.
    - In the helicopter example, having both **position and velocity** makes it a Markov state because it tells you everything needed to determine the next step.

**Clarifying the Concept of a Markov State**
    
- The speaker is responding to a question about whether knowing the current state is enough to predict the future.
- They confirm that **if we know the state, we can determine future states**—this follows the Markov property.
- However, **knowing the state does not necessarily tell us everything about rewards**.

- **Why is This Important?**
    
    - In reinforcement learning (RL) or decision-making problems, we often care not just about future states, but also **future rewards**.
    - Even if the current state determines the future, that doesn’t mean it automatically tells us whether the outcome will be good (high reward) or bad (low reward).
- **The Role of History in Rewards**
    
    - The speaker reminds us that **history includes all past rewards**.
    - So, when we say a Markov state is a "sufficient statistic for the future," we mean it must contain enough information to **predict all future rewards**, not just future states.



**Example 1: The Environment State is Markovian**

- If we had access to the **true environment state**, it would be **ideal** because:
    - By definition, the environment state **fully determines the future**.
    - The environment itself **relies on this state** to decide what happens next (e.g., next observation and reward).
    - This means that the **true environment state is always Markovian**—it has all the necessary information to predict future states and rewards.

**Example 2: The Entire History is Also Markovian (But Not Useful)**

- If we keep track of **all past observations, actions, and rewards**, this would also form a **Markov state**, because:
    - The **full history** contains all information needed to predict the future.
    - However, this is **impractical** because storing and processing an entire history is computationally inefficient.
    - It is **tautological** (obvious) that history contains all the information about itself, but that doesn’t mean it’s a useful way to represent a state.

**Key Takeaways**

1. **Markov states always exist**, but finding a useful representation is the challenge.
2. The **true environment state** is the best Markov state, but it’s often **not accessible** in real-world problems.
3. **Keeping the entire history is technically Markovian**, but it’s **impractical**.
4. The real challenge in reinforcement learning is **finding a compact and effective representation** of state that captures all relevant information **without storing everything**.

![Rat Example](09-rat-example.png)

- An example to illustrate how learning by trial and error works in an environment where actions lead to either rewards (cheese) or punishments (electrocution). 
- The example involves a rat (the audience) interacting with an "evil experimenter" who provides different sequences of actions (light, bell, lever) and outcomes.
- The predictions depend on the agent's **state representation**:
    - If the state is the last three actions, electrocution seems likely.
    - If the state is the count of actions, it might suggest cheese.
    - If the state is the full sequence, the outcome remains uncertain.
- The example emphasizes how different ways of encoding **state information** influence decision-making and learning.

![Fully Observable Environments](./images/10-fully-observable-environments.png)

- **Fully observable environments**.
    - In such environments, the **agent has complete visibility** into the environment's state.
    - The agent directly **observes and interacts with numerical states** within the environment.
- **Characteristics of a Fully Observable Environment**
    
    - The **observation**, **agent state**, and **environment state** all **collapse into the same quantity**.
    - The agent can **use the environment state directly** to make decisions.
    - This represents the **best-case scenario** for learning and decision-making.
- **Markov Decision Processes (MDPs)**
    
    - When dealing with fully observable environments, we use the **Markov Decision Process (MDP) framework**.
    - MDPs serve as the **main formalism in reinforcement learning**.
    - The next lecture will **explore MDPs in detail** as a powerful tool for modeling decision-making.
- **State Representation & Realistic Challenges**
    
    - While fully observable environments are ideal, **many real-world problems involve partial observability**.
    - Understanding **state representation** is crucial for handling such **realistic challenges**.
    - The MDP formalism also helps in **addressing partially observable cases**.

![Partially Observable Environments](./images/11-partially-observable-environments.png)
