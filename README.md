# Reinforcement-Learning
# Sepsis ICU Management with Reinforcement Learning

Reinforcement Learning project, MSc Data Science & Advanced Analytics, NOVA IMS (2025/2026).

Trains RL agents to choose vasopressor and IV-fluid doses for sepsis patients on the ICU-Sepsis-v2 benchmark,
built from the real MIMIC-III database. The reward is +1 for survival and 0 otherwise.

## Configuration A: tabular (716 states, 25 actions)
- **Policy Iteration** as the performance ceiling
- **Q-Learning** in three versions: baseline, improved (optimistic initialisation, visit-based learning rate,
  tie-breaking) and tuned (400k episodes)

| Method | Survival |
|---|---|
| Random | 69.3% |
| Q-Learning baseline | 76.1% |
| Q-Learning tuned | 82.5% |
| Policy Iteration | 84.1% |

## Configuration B: deep RL (47 continuous features)
Adds observation noise, missing lab values and random acute events. Compares **DQN, PPO and A2C**.

| Method | Survival |
|---|---|
| Random | 64.6% |
| DQN | 65.0% |
| PPO | 66.2% |
| **A2C** | **71.0%** |

DQN collapsed to a near-constant action, while A2C learned a conservative, more robust treatment policy.

## Extension: SOFA-based reward shaping
A per-step penalty based on the SOFA organ-failure score improved PPO's return under missing
observations (0.49 to 0.61), mainly by adding robustness rather than raising survival.
