# 🎓 FACIEE Gamified Challenge

> A desktop-based interactive experience designed to introduce students to the different study paths within FACIEE through camera interaction, mini-games, scoring and a persistent leaderboard.

![Python](https://img.shields.io/badge/Python-3.x-3776AB?style=for-the-badge\&logo=python\&logoColor=white)
![PyQt6](https://img.shields.io/badge/PyQt6-GUI-41CD52?style=for-the-badge\&logo=qt\&logoColor=white)
![OpenCV](https://img.shields.io/badge/OpenCV-Computer%20Vision-5C3EE8?style=for-the-badge\&logo=opencv\&logoColor=white)
![Pygame](https://img.shields.io/badge/Pygame-Game%20Engine-00A86B?style=for-the-badge\&logo=python\&logoColor=white)

A hackathon project built around a simple idea:

**turn the presentation of a university faculty into an interactive experience rather than a static screen.**

The application combines a modular PyQt6 interface, webcam-based interaction, computer vision, several PyGame mini-games, dynamic scoring and a shared leaderboard.

---

# ✨ What It Does

The application guides a user through an interactive faculty experience.

The main flow is:

```text
                 ┌──────────────────┐
                 │   Launch App     │
                 └────────┬─────────┘
                          │
                          ▼
                 ┌──────────────────┐
                 │ Webcam / Start   │
                 │      Screen      │
                 └────────┬─────────┘
                          │
                    Smile detected
                          │
                          ▼
                 ┌──────────────────┐
                 │ Game Selection   │
                 └────────┬─────────┘
                          │
             ┌────────────┼────────────┐
             ▼            ▼            ▼
          AIA Game      IEC Game     IETTI Game
             │            │            │
             └────────────┼────────────┘
                          ▼
                 ┌──────────────────┐
                 │ Score + Results  │
                 └────────┬─────────┘
                          ▼
                 ┌──────────────────┐
                 │   Leaderboard    │
                 └──────────────────┘
```

The user can start the experience by interacting with the webcam or use the manual start option provided by the interface.

---

# 🧠 Key Features

### 📷 Webcam Interaction

The project uses **OpenCV** to capture frames from the webcam and perform face and smile detection.

The camera module:

* captures live webcam frames;
* mirrors the image for a more natural interaction;
* detects faces using Haar cascades;
* detects smiles inside the detected face region;
* draws visual feedback around detected faces and smiles;
* exposes the detection result to the PyQt interface.

The smile detection is used as an interaction mechanism for starting the game flow. The application also provides a manual fallback button.

---

# 🖥️ Modular PyQt6 Interface

The application is built around a **PyQt6** main window with independently managed panels.

The main window combines:

* a camera panel;
* a welcome/start panel;
* a game selection panel;
* dynamically replaced content;
* timer-driven frame updates;
* transitions between application states.

The interface uses Qt signals to communicate between panels instead of hard-coding all interactions into a single window.

For example:

```text
Camera Panel
     │
     │ smile_detected
     ▼
Main Window
     │
     ▼
Game Panel
```

This keeps the UI logic separated into smaller components.

---

# 🎮 Interactive Mini-Games

The project includes multiple mini-games implemented with **PyGame**.

Each game follows the same general pattern:

```text
Input
  ↓
Game Logic
  ↓
Real-time State Update
  ↓
Score Calculation
  ↓
Game Over
  ↓
Persistent Score
  ↓
Leaderboard
```

## ⚡ AIA — Logic Circuit Challenge

The AIA game simulates a small digital logic circuit.

The player interacts with switches and must configure the circuit so that the final output is activated.

The game contains:

* configurable input switches;
* AND, OR, XOR and NAND gates;
* randomized circuit configurations;
* real-time circuit evaluation;
* a 60-second time limit;
* score penalties for additional clicks;
* a final score saved to the leaderboard.

The underlying circuit logic is represented directly in Python:

```text
Inputs → Logic Gates → Output
```

The level is randomized before the game begins, ensuring that each run can produce a different configuration.

---

## 📡 IETTI — Signal Master

The IETTI game is built around controlling a signal amplitude and matching it to dynamically generated targets.

The player can interact using:

* keyboard controls;
* mouse controls;
* real-time movement;
* dynamically generated targets.

The game includes:

* a 60-second time limit;
* dynamic scoring;
* particle effects;
* animated grid rendering;
* signal matching logic;
* reset functionality;
* leaderboard integration.

The game rewards the player for repeatedly aligning the controllable signal with the target range.

---

## 🔧 IEC — Hardware Hero

The IEC game focuses on identifying and collecting useful hardware components while avoiding hazards.

The game contains:

* falling components;
* player movement;
* collision detection;
* lives;
* score bonuses;
* penalties for incorrect collisions;
* particle/explosion effects;
* animated neon-style graphics;
* keyboard and mouse controls.

Components are classified as either beneficial or harmful, creating a fast reaction-based challenge.

---

# 🏆 Leaderboard

Scores are persisted locally in a CSV file.

Each recorded result contains:

```text
Name
Avatar
Specialization
Score
```

The leaderboard application loads the CSV data, parses player information, sorts players by score and displays the resulting ranking through a PyQt6 interface.

This creates a shared scoring system between the different games.

```text
              ┌───────────────┐
              │   Mini-Game   │
              └───────┬───────┘
                      │
                      ▼
                Final Score
                      │
                      ▼
               database.csv
                      │
                      ▼
              ┌───────────────┐
              │  Leaderboard  │
              └───────────────┘
```

---

# 🏗️ Project Architecture

The application is split into several logical layers.

```text
Hackaton2025/
│
├── main.py
│
├── Camera
│   └── camera.py
│
├── UI Panels
│   ├── panelCamera.py
│   ├── panelDreapta.py
│   └── panelJocuri.py
│
├── Games
│   ├── AiaGame.py
│   ├── Joc-IETTI.py
│   ├── joc_iec.py
│   └── ctiGame.py
│
├── Leaderboard
│   ├── leaderboard.py
│   ├── LeaderBoard.ui
│   └── database.csv
│
├── UI / Styling
│   └── style.qss
│
└── Assets
    └── asset/
```

The main entry point constructs the application window, initializes the camera and controls transitions between the different panels.

---

# 🔌 Communication Between Components

A notable part of the project is the interaction between multiple independently implemented components.

The main application uses **Qt signals** to communicate between panels.

Examples include:

```text
smile_detected
start_clicked
close_main_window
```

These events allow the application to transition between states without tightly coupling every component together.

The PyGame games also return control to the main application after completion and launch the leaderboard flow using Python subprocesses.

---

# 🎨 UI & Visual Design

The project combines multiple UI technologies:

### PyQt6

Used for:

* main application window;
* panels;
* buttons;
* labels;
* leaderboard;
* `.ui` layouts.

### QSS

Custom styling is used for the Qt interface through:

```text
style.qss
```

### PyGame

Used for:

* real-time game rendering;
* animations;
* particles;
* custom HUDs;
* collision handling;
* interactive gameplay.

This allows the project to combine a conventional desktop interface with dedicated real-time game environments.

---

# 🛠️ Technology Stack

| Technology | Purpose                            |
| ---------- | ---------------------------------- |
| Python     | Main programming language          |
| PyQt6      | Desktop GUI                        |
| OpenCV     | Webcam capture and computer vision |
| PyGame     | Interactive mini-games             |
| CSV        | Local score persistence            |
| Qt Signals | Component communication            |
| QSS        | GUI styling                        |
| Subprocess | Application/game transitions       |

---

# 🚀 Running the Project

## 1. Clone the repository

```bash
git clone https://github.com/TG-Jorj-2005/Hackaton2025.git
cd Hackaton2025
```

## 2. Install dependencies

The repository does not currently include a dedicated `requirements.txt`, so the main Python dependencies can be installed manually:

```bash
pip install PyQt6 opencv-python pygame
```

## 3. Start the application

```bash
python main.py
```

A webcam should be available if you want to use the camera-based interaction.

---

# 📁 Important Files

| File              | Responsibility                     |
| ----------------- | ---------------------------------- |
| `main.py`         | Main application entry point       |
| `camera.py`       | Webcam capture and smile detection |
| `panelCamera.py`  | Camera UI panel                    |
| `panelDreapta.py` | Welcome/start panel                |
| `panelJocuri.py`  | Game selection interface           |
| `AiaGame.py`      | AIA logic circuit game             |
| `Joc-IETTI.py`    | IETTI signal-based game            |
| `joc_iec.py`      | IEC hardware-themed game           |
| `leaderboard.py`  | Leaderboard management             |
| `database.csv`    | Persistent score storage           |
| `LeaderBoard.ui`  | Qt Designer UI                     |
| `style.qss`       | Qt stylesheet                      |
| `asset/`          | Visual assets                      |

---

# 🧩 Design Goals

The project was designed around several ideas:

**Interactive instead of static**

Students interact with the application instead of simply reading information.

**Technical instead of purely visual**

Each specialization is represented through a small technical challenge.

**Immediate feedback**

The games provide real-time visual feedback, scoring and game states.

**Modular implementation**

The UI, camera system, games and leaderboard are separated into distinct components.

**Competitive element**

The leaderboard adds replayability by allowing players to compare scores.

---

# 🧠 What This Project Demonstrates

This project combines several areas of software development in a single application:

* desktop GUI development;
* event-driven programming;
* modular application design;
* computer vision;
* real-time rendering;
* game development;
* collision detection;
* state management;
* scoring systems;
* local data persistence;
* inter-component communication;
* process management;
* UI styling.

Rather than being a collection of isolated scripts, the project connects these components into a single interactive user flow.

---

# 📸 Screenshots

Screenshots can be added here to show the main parts of the application:

```text
Main Screen
Game Selection
AIA Game
IETTI Game
IEC Game
Leaderboard
```

Example:

```markdown
![Main Interface](asset/main.png)
![Game Interface](asset/game.png)
![Leaderboard](asset/leaderboard.png)
```

---

# 🚧 Current Status

**Hackathon prototype / educational project**

The application was developed as a hackathon project and focuses on experimentation, rapid prototyping and combining multiple technologies into one interactive experience.

The codebase can be extended with additional games, richer persistence, improved packaging and a more scalable application architecture.

---

# 🔮 Possible Improvements

Future iterations could include:

* a proper SQLite database instead of CSV storage;
* a `requirements.txt` or `pyproject.toml`;
* improved error handling;
* separation of game logic from rendering;
* reusable game abstractions;
* packaged executables;
* richer user profiles;
* online leaderboards;
* additional computer-vision interactions;
* automated testing;
* CI/CD;
* improved documentation and screenshots.

---

## 🎓 Project Context

**Hackathon 2025 — FACIEE**

Built as an interactive software project combining education, gamification and technology.

---

## 🔗 Related Projects

My other Linux and development configurations:

* **Arch Linux Dotfiles:** https://github.com/TG-Jorj-2005/Dotfiles.Arch
* **NixOS Configuration:** https://github.com/TG-Jorj-2005/Nixos

---

> Built with Python, Qt, OpenCV and PyGame — with the goal of turning a faculty introduction into something you can actually interact with.
