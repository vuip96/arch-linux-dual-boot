# Generative AI Unity Game Project

A **Unity 3D game developed in C#** as one of the two practical case-study projects in the thesis **Using Generative AI in Unity Game Development: A Comparative Case Study of Two AI-Assisted Game Projects**.

The project explores how generative AI and AI-assisted tools can support programming, debugging, UI development, 3D asset creation, animation, audio, and iterative game development while keeping testing and final technical decisions in the developer's hands.

![Final gameplay and boss arena](screenshots/final-gameplay.png)

**▶ [Watch the gameplay demonstration on YouTube](https://youtu.be/BVXpZhep5CU)**

---

## Project Overview

The game is a 3D platforming project set in a lava-themed environment. The player progresses through the level, collects crystals, uses checkpoints, encounters enemies, and ultimately reaches a boss battle.

The repository contains the Unity project itself, including the game assets, C# scripts, package configuration, and project settings.

### My Role

This repository contains the Unity game project developed by **Pete Vuorela** as part of the comparative thesis study. I worked on the gameplay systems, C# implementation, UI and settings, boss mechanics, asset integration, AI-assisted development workflow, debugging, and testing.

### Key Features

- player movement and combat
- lava-based platforming environment
- collectible crystal system and counter
- checkpoints and progression logic
- main menu, pause/death states and settings
- audio and music controls
- language selection and key-binding settings
- enemy and boss systems
- boss HP, melee attacks and shockwave mechanics
- save/progression functionality
- character animation and 3D asset integration

---

## UI and Visual Design

The project evolved from simple Unity prototype interfaces into a more consistent lava/fantasy visual style.

### Main Menu

![Main menu](screenshots/main-menu.png)

### Settings

The settings system includes separate sound controls, mouse sensitivity, language selection and access to key bindings.

![Settings menu](screenshots/settings-menu.png)

---

## Technologies and Tools

### Development

- **Unity**
- **C#**
- **Visual Studio**
- **Git**
- **GitHub**

### 3D and Animation

- **Blender 5.1** - model inspection, editing and asset preparation
- **Mixamo** - character rigging and animation

### Generative AI and AI-Assisted Tools

| Tool | Use in the project |
|---|---|
| **ChatGPT** | Planning, problem solving, debugging support and development guidance |
| **Codex** | Project analysis, C# code changes, technical implementation and debugging |
| **Rodin** | AI-assisted 3D character and asset generation |
| **Adobe Firefly** | Visual asset and background generation |
| **ElevenLabs Studio** | AI-assisted voice and audio production |
| **Suno** | AI-generated music |

---

## AI-Assisted 3D Workflow

Rodin was used to generate early 3D character assets. The generated models still required practical integration, inspection, animation work and adjustment before they were suitable for the Unity project.

Player character and enemy character used in the project:

![Rodin-generated characters](screenshots/rodin-characters.png)

The workflow combined AI-generated content with **Blender**, **Mixamo** and **Unity** rather than treating AI output as a finished asset.

---

## How AI Was Used

### Programming and Debugging

ChatGPT and Codex supported development by helping with:

- C# implementation
- debugging and error analysis
- planning game systems
- modifying existing project files
- iterating on UI and settings
- solving Unity-specific implementation problems

AI-generated suggestions were tested in Unity and adjusted when they did not fit the existing project structure or gameplay goals.

### UI and Settings

A substantial part of the AI-assisted work involved menus, UI, settings and related logic. These systems combined visual elements with code for audio settings, mouse sensitivity, language selection, key bindings and different game states.

### Assets, Animation and Audio

AI and supporting tools were also used outside programming:

- **Rodin** for 3D asset generation
- **Adobe Firefly** for visual content
- **Blender 5.1** for 3D model work
- **Mixamo** for animation and rigging
- **Suno** for music
- **ElevenLabs Studio** for voice/audio work

This made the project a broader experiment in AI-assisted game development rather than only an AI coding exercise.

---

## Development Process

The project was developed iteratively. Early versions were tested directly in Unity, and systems were revised when visual results, colliders, controls, animations or gameplay behavior did not work as intended.

<details>
<summary><strong>View technical development screenshots</strong></summary>

### Level Overview

The Unity editor view shows the overall lava environment, platforming route and boss arena.

![Unity level overview](screenshots/development/level-overview.png)

### Collectible and UI Integration

This development view shows a crystal collectible being integrated into the game together with the HUD crystal counter.

![Collectible and UI integration](screenshots/development/collectible-ui-integration.png)

### Collectible Behaviour and Collider

The collectible uses a custom hover-and-rotate component together with a trigger collider.

![Hover and rotate component](screenshots/development/hover-rotate-component.png)

</details>

---

## What the Project Demonstrates

This project demonstrates practical experience with:

- Unity and C# development
- gameplay and boss mechanics
- UI and settings systems
- debugging and iterative development
- game-state and progression logic
- 3D asset integration
- character animation
- audio integration
- Git and GitHub
- AI-assisted programming
- AI-assisted asset and content workflows
- evaluating where AI output still requires manual testing and judgement

The most important result of the project was not simply that AI could generate code or assets, but that it could accelerate clearly scoped tasks while the developer remained responsible for integration, testing, quality and final decisions.

---

## Running the Project

1. Clone the repository.
2. Make sure **Git LFS** is installed and available.
3. Open the project through **Unity Hub**.
4. Use **Unity 6000.4.2f1** or a compatible version.
5. Allow Unity to restore the required packages before opening the project scenes.

---

## Thesis

This project was created as part of the thesis:

### Using Generative AI in Unity Game Development: A Comparative Case Study of Two AI-Assisted Game Projects

**Finnish title:** *Generatiivisen tekoälyn hyödyntäminen Unity-pelinkehityksessä*  
**Authors:** Hilla Ukonsaari and Pete Vuorela  
**Institution:** Oulu University of Applied Sciences  
**Degree Programme:** Information and Communication Technology  
**Publication year:** 2026  
**Language:** Finnish

📖 **[Read the thesis in Theseus](https://www.theseus.fi/handle/10024/926898)**

---

## Asset Notice

This project contains a combination of original, AI-assisted and third-party assets. Third-party assets remain subject to their respective original licenses and terms.

---

## Repository Structure

```text
Generative-AI-Unity-Game-Project/
├── Assets/                     # Game assets, C# scripts, scenes and audio
├── Packages/                   # Unity package configuration
├── ProjectSettings/            # Unity project settings
├── screenshots/
│   ├── final-gameplay.png
│   ├── main-menu.png
│   ├── settings-menu.png
│   ├── rodin-characters.png
│   └── development/
│       ├── level-overview.png
│       ├── collectible-ui-integration.png
│       └── hover-rotate-component.png
├── .gitignore
├── .gitattributes
└── README.md
```

---

## Author

**Pete Vuorela**  
ICT Engineering  
Oulu University of Applied Sciences
