# 🏃‍♂️ EndlessRunner-UE5
[![Unreal Engine](https://img.shields.io/badge/Unreal_Engine-5.2%2B-white?logo=unrealengine&logoColor=white&color=0E1128)](https://www.unrealengine.com/)
[![Status](https://img.shields.io/badge/Status-Work_In_Progress-orange?style=flat-square)](https://github.com/Ares19v/EndlessRunner-UE5)
[![License](https://img.shields.io/badge/License-MIT-green?style=flat-square)](LICENSE)
[![Platform](https://img.shields.io/badge/Platform-Windows-blue?style=flat-square)](https://www.microsoft.com/windows)

A high-performance, modular, and visually stunning Endless Runner built from the ground up in **Unreal Engine 5**. This project serves as a showcase for procedural environment generation, advanced character movement, and modern rendering techniques like Lumen and Substrate.

---

## 🌟 Project Overview
**EndlessRunner-UE5** is more than just a game; it's a technical framework for building scalable procedural experiences. Developed over several months of iterative design, it focuses on high-fidelity urban environments, fluid controls, and a decoupled architecture that allows for infinite scalability.

### 🎯 Key Features
- **✨ Procedural Tile System**: A modular floor spawning logic that ensures infinite gameplay with zero performance degradation.
- **🏃‍♂️ Advanced Movement**: Built on the Enhanced Input System, featuring smooth lane switching, jumping, and momentum-based physics.
- **🧱 Dynamic Obstacle Generation**: A robust obstacle spawning engine that intelligently places hazards to challenge the player.
- **🎨 High-Fidelity Rendering**: Fully integrated with **Lumen Global Illumination**, **Nanite Virtualized Geometry**, and **Substrate Materials**.
- **🔌 Interface-Driven Architecture**: Uses Blueprint Interfaces for decoupled communication between the Game Mode, Character, and Spawner.

---

## 🛠 Tech Stack & Tools
| Technology | Description |
| :--- | :--- |
| **Unreal Engine 5.2+** | Core game engine and development environment. |
| **Blueprints (Visual Scripting)** | High-level logic and game systems implementation. |
| **Enhanced Input System** | Modern input handling for complex control schemes. |
| **Lumen & Nanite** | Real-time global illumination and high-poly geometry support. |
| **Substrate** | New modular material framework for realistic surfaces. |
| **Git LFS** | Optimized handling of large binary assets (.uasset, .umap). |

---

## 📁 Repository Structure
```text
EndlessRunner/
├── Config/             # Project-wide settings (Input, Engine, Editor)
├── Content/
│   ├── BluePrints/     # Core game logic (Floors, Obstacles, Spawners)
│   ├── BPInterface/    # Communication contracts between systems
│   ├── Characters/     # Player models and animation blueprints
│   ├── Input/          # Enhanced Input Actions and Mapping Contexts
│   ├── ThirdPerson/    # Customized core game mode and templates
│   ├── UserWidget/     # UI/HUD layouts and logic
│   └── Assets/         # High-quality environment and prop assets
├── .gitattributes      # LFS configuration for binary assets
├── .gitignore          # Exclusion rules for generated files
└── EndlessRunner21.uproject
```

---

## 🚀 Getting Started

### Prerequisites
1.  **Unreal Engine 5.2+** installed via the Epic Games Launcher.
2.  **Git LFS** installed on your system. Run `git lfs install` in your terminal.

### Installation
1.  **Clone the repository**:
    ```bash
    git clone https://github.com/Ares19v/EndlessRunner-UE5.git
    ```
2.  **Initialize LFS**:
    ```bash
    git lfs pull
    ```
3.  **Open the Project**:
    - Right-click `EndlessRunner21.uproject` and select **Generate Visual Studio project files** (if C++ extensions are added).
    - Open `EndlessRunner21.uproject` in the Unreal Editor.

---

## 🛣 Roadmap & WIP
This project is currently under active development. Upcoming milestones include:
- [ ] **Power-up System**: Magnets, Shields, and Speed Boosters.
- [ ] **Global Leaderboard**: Integration with a backend for high-score tracking.
- [ ] **Multiple Biomes**: Seamless transitions between city, industrial, and forest zones.
- [ ] **Advanced AI**: Dynamic NPCs that interact with the environment.

---

## 🤝 Contributing
Contributions are what make the open-source community such an amazing place to learn, inspire, and create. Any contributions you make are **greatly appreciated**.

1. Fork the Project
2. Create your Feature Branch (`git checkout -b feature/AmazingFeature`)
3. Commit your Changes (`git commit -m 'Add some AmazingFeature'`)
4. Push to the Branch (`git push origin feature/AmazingFeature`)
5. Open a Pull Request

---

## 📜 License
Distributed under the MIT License. See `LICENSE` for more information.

---

## 📫 Contact
**Devansh Tyagi** - [GitHub](https://github.com/Ares19v)  
Project Link: [https://github.com/Ares19v/EndlessRunner-UE5](https://github.com/Ares19v/EndlessRunner-UE5)

---
*Created with ❤️ for the Unreal Engine Community.*
