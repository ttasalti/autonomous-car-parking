# Autonomous car parking with reinforcement learning

Undergraduate project (Ankara University, 2021) by Tarık Tuna Taşaltı and Alparslan İdris Arslan. A 2D car learns to park in a randomly chosen slot between other cars, trained with PPO through Unity ML-Agents. We developed the project on one machine, so the commit history carries one name.

## How it works

- **Environment.** A top-down Unity scene. At the start of each episode one of ten parking slots is picked at random, the other nine are filled with obstacle cars, and the agent starts from a fixed spawn point (`Assets/Scripts/CarAgent.cs`, `spawnOthers.cs`).
- **Agent.** Continuous actions for steering and throttle, applied through a simple car controller. Observations are the agent's position, the target slot's position and direction in the car's own frame, its velocity, and its orientation vectors.
- **Rewards.** A small shaping reward for moving towards the slot, a penalty and episode end on collision with a car or a wall, and a reward when the car comes to rest inside the slot (`Parking.cs`).
- **Training.** PPO with the settings in `config/ourConfig.yaml` (two hidden layers of 128 units, batch 1024, buffer 10240, up to 5M steps). Recorded human demonstrations are in `Assets/Demonstration/` and the trained policies in `Assets/nn-models/`.

## Running

Open the project in Unity with the ML-Agents package, then train from the repository root:

```bash
mlagents-learn config/ourConfig.yaml --run-id=parking
```

Press Play in the editor when prompted. To watch a trained policy, assign one of the `.onnx` files under `Assets/nn-models/` to the agent's Behavior Parameters.
