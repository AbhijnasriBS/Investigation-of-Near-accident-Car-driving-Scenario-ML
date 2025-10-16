# Near-Accident Car Driving with Deep Imitation Learning and Reinforcement Learning

## 🚘 Project Overview

This project presents a **hierarchical driving control system** designed to handle near-accident scenarios. The system integrates:
1. **Conditional Imitation Learning (CoIL)** — for low-level driving control.  
2. **Proximal Policy Optimization (PPO)** — for high-level decision-making and mode selection.

---

## 🧠 Problem Statement

In near-accident scenarios, autonomous vehicles must **react quickly and adaptively** to the behavior of surrounding vehicles. Traditional control systems struggle to handle high-risk conditions effectively.  
This project tackles this challenge by:
- Learning multiple driving modes (**timid**, **normal**, **aggressive**).  
- Using reinforcement learning to switch intelligently between these modes.  

---

## ⚙️ Methodology

### 1. Conditional Imitation Learning (CoIL)
- Trains a neural network to imitate expert driving in different behavioral modes.  
- **Architecture:** Shared feature extraction layers + mode-specific output heads.  
- **Input:** Vehicle observations (positions, velocities).  
- **Output:** Low-level control actions (e.g., throttle).

### 2. Reinforcement Learning (PPO)
- Trains a high-level agent to select the most appropriate driving mode.  
- **Objective:** Minimize collisions while maintaining efficiency.  
- **Controller:** Uses the trained CoIL model as a low-level policy.

---

## 🛠️ Implementation Details

### Technologies Used
- 🧰 **PyTorch** — Deep learning for CoIL  
- 🧭 **Stable-Baselines3** — RL framework for PPO  
- 🏎️ **Gymnasium** — RL environment interface  
- 🐍 **Python 3.x** — Core programming language

### CoIL Network Architecture
- **Input:** 8D observation (ego + ado vehicle positions and velocities)  
- **Shared Layers:** 2 hidden layers (256 units each)  
- **Branch Heads:** 3 mode-specific heads (128 → 64 → 1 units)  
- **Total Parameters:** ≈ 200K

### PPO Agent
- **Policy:** Multi-Layer Perceptron (MLP)  
- **Action Space:** Discrete(3) → Mode selection  
- **Observation Space:** 8D continuous

---

## 🚦 Scenarios Evaluated
1. **Cross Traffic:** Ego car approaches intersection while another vehicle crosses.  
2. **Wrong Direction:** Head-on collision scenario with an oncoming vehicle.

---

## 📊 Results

| Method            | Collision Rate | Completion Time (s) |
|--------------------|----------------|-----------------------|
| CoIL - Timid       | 0.37           | 9.52 s               |
| CoIL - Normal      | 0.18           | 4.39 s               |
| CoIL - Aggressive  | 0.14           | 4.01 s               |
| Random             | 0.28           | 6.10 s               |
| RL - 3 Modes       | **0.15**       | **4.28 s**           |

- **RL-3modes** achieves the **best balance** between **safety** and **efficiency**.  
- Outperforms random mode selection significantly.  
- Adding more modes improves completion time with minimal safety trade-off.

---

## 🧪 Performance Metrics
- Collision rate comparison  
- Average completion time comparison  
- Mode-switching efficiency  
- (See `evaluation_results.csv` for detailed metrics)

---

## 🧰 Setup & Installation

```bash
# Clone the repository
git clone https://github.com/AbhijnasriBS/Investigation-of-Near-accident-Car-driving-Scenario-ML
cd NearAccident-Driving

# Create and activate virtual environment (optional but recommended)
python -m venv venv
source venv/bin/activate  # On Windows: venv\Scripts\activate

# Install dependencies
pip install -r requirements.txt
```

---

## 🚀 Run the Project

```bash
# Train CoIL model
python train_coil.py

# Train PPO high-level agent
python train_ppo.py

# Evaluate model
python evaluate.py
```

---

## 📌 Future Work
- Adding more behavioral modes for complex scenarios.  
- Extending to multi-agent traffic environments.  
- Real-world deployment with sensor integration.

---

## 📝 Citation
If you use this work, please consider citing the project or giving credit in your research.

---

## 👨‍💻 Authors
Developed as part of a mini-project on **autonomous driving in near-accident scenarios**.

