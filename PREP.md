# Study Prep Guide: EndlessRunner-UE5: Next-Gen Procedural Framework

Welcome! This guide is a step-by-step beginner's tutorial designed to help you understand and build **EndlessRunner-UE5**—a highly optimized, procedural infinite runner framework in Unreal Engine 5.7. You will learn about object pooling, StateTree AI/state logic, decoupling systems via interfaces, and modern game development workflows.

---

## 🗺️ System Architecture

EndlessRunner-UE5 uses a modular, decoupled architecture where components communicate via interfaces to avoid circular dependencies:

```
               [Gameplay StateTree (ST_Player)]
                             │
                             ▼
                [BP_ThirdPersonGameMode]
                             │
                [BP_ActorPoolManager]
               /                     \
              ▼                       ▼
      [BP_FloorTile]           [BP_ObstacleSpawner]
      (Recycled/Pooled)        (Niagara VFX & MetaSounds)
```

---

## 📚 Core Learning Prerequisites

Before building a game in UE5, make sure you understand:
1. **Blueprint Basics**: Event graphs, variables, functions, and nodes in Unreal Engine's visual scripting system.
2. **GameMode & GameState**: Understanding which classes control rules, scoring, spawning, and HUD overlays.
3. **Object Pooling**: A design pattern where instances are pre-created (pre-allocated) and deactivated instead of constantly being spawned and destroyed (which causes CPU spikes and lag).
4. **Blueprint Interfaces (BPI)**: Decoupled communication contracts that let different Blueprints talk to each other without knowing anything about each other's internal variables.

---

## 🛠️ Step-by-Step Implementation Guide

Let's understand how a basic Actor Pool works under the hood inside Unreal Engine!

### Step 1: Understanding Actor Pooling (Conceptual)
In an infinite runner, tiles appear in front of the player and disappear behind them.
- **Bad Practice**: Spawning a tile (`Spawn Actor from Class`) and destroying it (`Destroy Actor`) every 2 seconds. This causes garbage collection spikes and micro-stuttering.
- **Good Practice**: Creating an array of 10 Floor tiles when the game boots up. Move them to a hidden location (`Set Actor Hidden in Game` and disable collisions). When a new tile is needed, grab a deactivated one from the pool, place it in front of the player, and activate it.

---

### Step 2: Decoupled Blueprint Interface Communication
To communicate between the Player character and the Tile spawner without hard referencing each other, we create a Blueprint Interface called `BPI_GameManager`.

Inside the Interface:
1. Define a function: `TriggerTileRecycle(Vector SpawnLocation)`.
2. Any Blueprint that implements `BPI_GameManager` (like the GameMode) will automatically listen for this call.

Inside the Floor Tile Blueprint:
1. Place a Box Collision Component at the end of the tile.
2. On `ComponentBeginOverlap` (when the player crosses the finish line), grab the GameMode and call the interface message:
   ```
   Get Game Mode ──► TriggerTileRecycle (Interface Message)
   ```
3. Because we use an Interface, the Floor Tile Blueprint does NOT need to hard-cast to a specific `BP_MyRunnerGameMode`, keeping compiling links perfectly clean and warning-free.

---

### Step 3: Gameplay StateTree Setup
Instead of drawing hundreds of spaghetti lines inside the Animation Blueprint or Player character to handle jumping, sliding, and running, UE 5.7 introduces **Gameplay StateTrees**.
1. Create a `ST_PlayerStateTree` asset.
2. Set up the root states:
   - **Running** (Default state)
   - **Jumping** (Triggered by pressing Spacebar IA)
   - **Sliding** (Triggered by pressing Ctrl IA)
   - **GameOver** (Triggered by hitting an obstacle)
3. Connect task transitions: When `Jumping` completes, transition back to `Running`. StateTree handles this instantly under the hood.

---

## 🔍 Key Deep Dive Topics

### 1. Enhanced Input 2.0
UE 5.7 uses Enhanced Input to support dynamic input mappings (e.g. switching between keyboard and gamepad controls on the fly).
- **Input Action (IA)**: Represents a physical action (like `IA_Jump` or `IA_Slide`).
- **Input Mapping Context (IMC)**: Maps actual keys (e.g. `Spacebar` or `Gamepad Face Button Bottom`) to the Input Actions. The Player Controller registers the IMC at game launch.

### 2. Niagara VFX & MetaSounds
Instead of legacy sound cues and particle systems, EndlessRunner leverages high-performance **Niagara System** emitters for dust kicks during sliding, and **MetaSounds** (Unreal's node-based digital signal processing engine) for procedural sound synthesis that dynamically speeds up as the player runs faster.

---

## 🎯 Verification Tasks

1. **Local Launch**: Clone the repository, run `git lfs pull` to fetch binary assets, and open `EndlessRunner21.uproject` using Unreal Engine 5.7.
2. **Compile Test**: Open the Editor, compile `BP_ThirdPersonGameMode` and `BP_ActorPoolManager`, and verify that the Blueprint Editor reports 0 compile warnings.
3. **Execution Test**: Hit Play, run the character through the course, and notice how floor tiles are recycled dynamically at the back and spawned seamlessly ahead without dropping frames.
