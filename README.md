# 🎓 FACIEE Gamified Challenge

> An interactive Raspberry Pi-powered desktop experience designed to introduce students to the different study paths within FACIEE through computer vision, hardware interaction, mini-games, scoring and a persistent leaderboard.

[![Python](https://img.shields.io/badge/Python-3.x-3776AB?style=for-the-badge\&logo=python\&logoColor=white)](https://www.python.org/)
[![PyQt6](https://img.shields.io/badge/PyQt6-GUI-41CD52?style=for-the-badge\&logo=qt\&logoColor=white)](https://www.riverbankcomputing.com/software/pyqt/)
[![OpenCV](https://img.shields.io/badge/OpenCV-Computer%20Vision-5C3EE8?style=for-the-badge\&logo=opencv\&logoColor=white)](https://opencv.org/)
[![Pygame](https://img.shields.io/badge/Pygame-Game%20Engine-00A86B?style=for-the-badge\&logo=python\&logoColor=white)](https://www.pygame.org/)
[![Raspberry Pi](https://img.shields.io/badge/Raspberry%20Pi-Hardware-C51A4A?style=for-the-badge\&logo=raspberry-pi\&logoColor=white)](https://www.raspberrypi.com/)

A hackathon project built around a simple idea:

**turn the presentation of a university faculty into an interactive physical experience rather than a static screen.**

The application combines a **Raspberry Pi**, webcam-based computer vision, a modular **PyQt6** interface, several **PyGame** mini-games, dynamic scoring and a shared leaderboard.

---

# ✨ What It Does

The application guides a user through an interactive faculty experience running on a Raspberry Pi.

The main flow is:

```text
                 ┌────────────────────┐
                 │    Raspberry Pi    │
                 └─────────┬──────────┘
                           │
                           ▼
                 ┌────────────────────┐
                 │  Camera / Start    │
                 │      Screen        │
                 └─────────┬──────────┘
                           │
                     Smile detected
                           │
                           ▼
                 ┌────────────────────┐
                 │   Game Selection   │
                 └─────────┬──────────┘
                           │
              ┌────────────┼────────────┐
              ▼            ▼            ▼
           AIA Game      IEC Game     IETTI Game
              │            │            │
              └────────────┼────────────┘
                           ▼
                 ┌────────────────────┐
                 │  Score + Results   │
                 └─────────┬──────────┘
                           ▼
                 ┌────────────────────┐
                 │    Leaderboard     │
                 └────────────────────┘
```

The physical setup combines the Raspberry Pi with a display and camera, turning the software into an interactive kiosk-like experience.

---

# 🍓 Raspberry Pi Integration

A core part of the project is its deployment on a **Raspberry Pi**.

Instead of running only as a conventional desktop application, the project was designed to work as a self-contained interactive system using Raspberry Pi hardware.

The Raspberry Pi acts as the computing platform for:

* running the Python application;
* connecting to the webcam;
* processing camera frames;
* rendering the graphical interface;
* running the PyGame mini-games;
* handling user input;
* providing the physical deployment environment.

This makes the project a combination of **software development and hardware-oriented deployment**.

```text
             ┌──────────────────────┐
             │     Raspberry Pi     │
             │                      │
             │  Python Application  │
             └──────────┬───────────┘
                        │
          ┌─────────────┼─────────────┐
          │             │             │
          ▼             ▼             ▼
       Webcam        Display       Input
          │             │             │
          ▼             ▼             ▼
      OpenCV         PyQt6         PyGame
```

The project was therefore developed with the constraints of a small embedded computing platform in mind rather than a conventional high-performance desktop.

---

# 🧠 Key Features

### 📷 Computer Vision

The project uses **OpenCV** to capture frames from the webcam and perform face and smile detection.

The camera module:

* captures live webcam frames;
* mirrors the image for a more natural interaction;
* detects faces using Haar cascades;
* detects smiles inside detected face regions;
* draws visual feedback around detected faces and smiles;
* exposes the detection result to the PyQt interface.

The smile detection is used as an interaction mechanism for starting the experience, while a manual fallback is also available.

---

### 🖥️ Modular Desktop Interface

The application is built around a **PyQt6** main window with independently managed panels.

The main window combines:

* camera panel;
* welcome/start panel;
* game selection panel;
* dynamically replaced content;
* timer-driven frame updates;
* transitions between application states.

Qt signals are used to communicate between panels rather than keeping all application logic inside a single monolithic window.

Example:

```text
Camera Panel
     │
     │ smile_detected
     ▼
Main Window
     │
     ▼
Game Selection
```

This keeps the interface modular and easier to extend.

---

# 🎮 Interactive Mini-Games

The project includes multiple mini-games implemented with **PyGame**.

Each game follows a similar pipeline:

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

The games are designed around different technical themes associated with FACIEE specializations.

---

## Demonstrație video

O rundă a minijocului CTI în PyQt6, de la prima întrebare până la scorul final.

https://github.com/user-attachments/assets/b35d8da3-b28f-4aea-8bed-536462475d1e

## ⚡ AIA — Logic Circuit Challenge

The AIA game simulates a digital logic circuit.

The player interacts with switches and must configure the circuit so that the desired output is activated.

The game contains:

* configurable input switches;
* AND, OR, XOR and NAND gates;
* randomized circuit configurations;
* real-time circuit evaluation;
* a 60-second time limit;
* score penalties for additional clicks;
* final score persistence.

The logic can be represented as:

```text
Inputs → Logic Gates → Output
```

The circuit configuration is randomized before each run, making repeated sessions less predictable.

---

## 📡 IETTI — Signal Master

The IETTI game focuses on controlling a signal amplitude and matching it against dynamically generated targets.

The player interacts through:

* keyboard controls;
* mouse input;
* real-time movement;
* dynamic target generation.

The game includes:

* time-based gameplay;
* dynamic scoring;
* particle effects;
* animated grid rendering;
* signal matching;
* reset functionality;
* leaderboard integration.

The objective is to repeatedly align the controllable signal with the generated target.

---

## 🔧 IEC — Hardware Hero

The IEC game introduces a hardware-themed challenge where the player collects useful components while avoiding hazards.

The game includes:

* falling components;
* player movement;
* collision detection;
* lives;
* score bonuses;
* penalties;
* particle/explosion effects;
* animated rendering;
* keyboard and mouse controls.

The game was designed to reinforce the connection between software and physical hardware concepts.

---

# 🏆 Leaderboard

Scores are persisted locally using a CSV-based storage system.

Each result contains information such as:

```text
Name
Avatar
Specialization
Score
```

The leaderboard loads the stored results, sorts players according to their scores and displays the ranking through a PyQt6 interface.

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

This creates a shared progression and competitive element across the different games.

---

# 🏗️ Project Architecture

The application is split into several logical components:

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

The architecture separates:

```text
Hardware / Camera
        ↓
Computer Vision
        ↓
GUI / Application State
        ↓
Game Modules
        ↓
Scoring
        ↓
Leaderboard
```

---

# 🔌 Communication Between Components

The application uses **Qt signals** to coordinate transitions between different UI components.

Examples include:

```text
smile_detected
start_clicked
close_main_window
```

This allows individual panels to emit events while the main application decides how to transition to the next state.

The PyGame modules are launched as dedicated game environments and return control to the main application once gameplay is finished.

The project also uses Python process management where appropriate to handle transitions between components.

---

# 🎨 UI & Visual Design

The application combines several graphical technologies.

### PyQt6

Used for:

* application window;
* interface panels;
* buttons;
* labels;
* leaderboard;
* Qt Designer layouts.

### QSS

Custom Qt styling is provided through:

```text
style.qss
```

### PyGame

Used for:

* game rendering;
* animations;
* particles;
* HUDs;
* real-time interaction;
* collision handling.

This combination allows the application to maintain a polished desktop interface while embedding dedicated real-time gameplay.

---

# 🧰 Technology Stack

| Technology       | Purpose                               |
| ---------------- | ------------------------------------- |
| **Python**       | Main programming language             |
| **Raspberry Pi** | Computing / hardware platform         |
| **PyQt6**        | Desktop GUI                           |
| **OpenCV**       | Computer vision and webcam processing |
| **PyGame**       | Interactive mini-games                |
| **CSV**          | Local score persistence               |
| **Qt Signals**   | Component communication               |
| **QSS**          | GUI styling                           |
| **Subprocess**   | Application / game transitions        |

---

# 🚀 Running the Project

## 1. Clone the repository

```bash
git clone https://github.com/TG-Jorj-2005/Hackaton2025.git
cd Hackaton2025
```

## 2. Install dependencies

The main Python dependencies are:

```bash
pip install PyQt6 opencv-python pygame
```

On a Raspberry Pi, the installation method may need to be adapted to the OS image, Python version and available system packages.

## 3. Start the application

```bash
python main.py
```

A working webcam is required for the camera-based interaction.

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

The project was designed around several principles.

### Interactive instead of static

Users interact with the application instead of simply reading information.

### Software + Hardware

The experience runs on a Raspberry Pi, connecting the software application to a physical computing platform.

### Technical instead of purely visual

Each specialization is represented through a small technical challenge.

### Immediate feedback

The games provide real-time visual feedback, scoring and state changes.

### Modular implementation

The camera, UI panels, games and leaderboard are separated into distinct components.

### Competitive element

The leaderboard encourages replayability and comparison between players.

---

# 🧠 What This Project Demonstrates

This project combines multiple areas of software and hardware development:

* Python application development;
* desktop GUI development;
* event-driven programming;
* modular application architecture;
* Raspberry Pi deployment;
* webcam integration;
* computer vision;
* real-time rendering;
* game development;
* collision detection;
* state management;
* scoring systems;
* local data persistence;
* process management;
* inter-component communication;
* UI styling.

More importantly, the project demonstrates how multiple independent technologies can be combined into a single physical interactive system.

---

# 🔄 End-to-End System

The complete experience can be viewed as:

```text
                    USER
                      │
                      ▼
              ┌───────────────┐
              │   Raspberry   │
              │      Pi       │
              └───────┬───────┘
                      │
              ┌───────▼───────┐
              │    Webcam     │
              └───────┬───────┘
                      │
                      ▼
               ┌─────────────┐
               │   OpenCV    │
               │ Face/Smile  │
               │  Detection  │
               └──────┬──────┘
                      │
                      ▼
               ┌─────────────┐
               │   PyQt6     │
               │ Application │
               └──────┬──────┘
                      │
              ┌───────┼────────┐
              ▼       ▼        ▼
             AIA     IEC      IETTI
              │       │        │
              └───────┼────────┘
                      │
                      ▼
               ┌─────────────┐
               │    Score    │
               └──────┬──────┘
                      │
                      ▼
               ┌─────────────┐
               │ Leaderboard │
               └─────────────┘
```

---

# 📸 Screenshots

Screenshots can be added here to showcase the physical and software experience:

```text
Main Screen
Camera Interaction
Game Selection
AIA Game
IETTI Game
IEC Game
Leaderboard
Raspberry Pi Setup
```

Example:

```markdown
![Main Interface](asset/main.png)
![Game Interface](asset/game.png)
![Leaderboard](asset/leaderboard.png)
```

A photograph of the Raspberry Pi setup would also be particularly useful here because it demonstrates that this is not only a desktop software project.

---

# 🚧 Current Status

**Hackathon prototype / educational project**

The application was developed as a hackathon project and focuses on rapid prototyping, hardware/software integration and combining multiple technologies into one interactive experience.

The current implementation can be extended with additional games, more robust persistence, better packaging and a more scalable application architecture.

---

# 🔮 Possible Improvements

Potential future improvements include:

* SQLite or another structured database instead of CSV;
* `requirements.txt` or `pyproject.toml`;
* improved input validation and error handling;
* reusable game abstractions;
* cleaner separation between game logic and rendering;
* packaged deployment for Raspberry Pi;
* richer player profiles;
* online leaderboards;
* additional camera interactions;
* automated testing;
* CI/CD;
* hardware peripherals such as physical buttons, LEDs or sensors;
* better performance optimization for Raspberry Pi.

---

## 🎓 Project Context

**Hackathon 2025 — FACIEE**

An interactive project built to combine:

**education + gamification + computer vision + software + Raspberry Pi**

> Built with Python, Qt, OpenCV, PyGame and Raspberry Pi — turning a faculty presentation into an interactive experience.
