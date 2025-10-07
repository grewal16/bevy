# 🚀 Bevy Engine

<p align="center"><img src="./assets/branding/banner.png" alt="Bevy Engine Logo" width="500"></p>

<p align="center">
  <a href="https://github.com/grewal16/bevy/stargazers"><img src="https://img.shields.io/github/stars/grewal16/bevy?style=for-the-badge" alt="GitHub stars"></a>
  <a href="https://github.com/grewal16/bevy/network/members"><img src="https://img.shields.io/github/forks/grewal16/bevy?style=for-the-badge" alt="GitHub forks"></a>
  <a href="https://github.com/grewal16/bevy/issues"><img src="https://img.shields.io/github/issues/grewal16/bevy?style=for-the-badge" alt="GitHub issues"></a>
  <a href="./LICENSE-MIT"><img src="https://img.shields.io/github/license/grewal16/bevy?style=for-the-badge" alt="GitHub license"></a>
</p>

## Short Description
The Bevy Engine is a refreshingly simple and powerful data-driven game engine built in Rust. Designed for blazing-fast development and unparalleled flexibility, Bevy offers a complete suite of tools for 2D and 3D game creation, leveraging a modern Entity Component System (ECS) architecture. Whether you're a seasoned game developer or new to Rust, Bevy empowers you to build ambitious projects with ease.

## ✨ Key Features
*   **Data-Driven ECS:** A highly performant and flexible Entity Component System for managing game state.
*   **Modular & Extensible:** Built with a plugin-based architecture, allowing you to easily add or swap features.
*   **Stunning 2D & 3D Graphics:** Comprehensive rendering capabilities including Physically Based Rendering (PBR), advanced lighting (ambient, directional, point, spot), real-time shadows, post-processing effects (Bloom, Depth of Field, SSAO, SSR, TAA), and volumetric fog.
*   **Cross-Platform Support:** Deploy your games to desktop, Android, and WebAssembly (WASM).
*   **Rich Input Handling:** Support for keyboard, mouse, touch, and gamepad inputs, including rumble feedback.
*   **Powerful UI System:** Flexible UI layout powered by a flexbox-like system, complete with gradients, interactive widgets, and accessibility features.
*   **Sophisticated Animation:** Advanced animation graphs, skeletal animation, morph targets, and easing functions for dynamic motion.
*   **Robust Asset Pipeline:** Streamlined asset loading, hot-reloading for rapid iteration, and custom asset processors for complex data.
*   **Integrated Dev Tools:** FPS overlay, comprehensive diagnostics, and CI testing utilities to keep development smooth.
*   **Advanced Math Primitives:** Extensive 2D/3D math library including bounding volumes, cubic splines, and raycasting.

## Who is this for?
Bevy is ideal for:
*   **Game Developers:** Seeking a modern, high-performance, and open-source game engine.
*   **Rust Enthusiasts:** Looking to apply their Rust skills to game development and contribute to a rapidly growing ecosystem.
*   **Engine Developers:** Interested in a modular and well-architected codebase for learning or building upon.
*   **Innovators:** Who want full control over their game logic and rendering pipeline without fighting rigid abstractions.

## Technology Stack & Architecture
*   **Language:** Rust
*   **Rendering Backend:** WGPU (WebGPU implementation for cross-platform GPU access)
*   **Core Architecture:** Custom Bevy ECS (Entity Component System)
*   **Input Handling:** Winit (windowing), Gilrs (gamepads)
*   **Asset Management:** Custom asynchronous asset pipeline
*   **Platforms:** Windows, macOS, Linux, Android, Web (WASM)

## 📊 Architecture & Database Schema

The Bevy Engine operates on a powerful, data-driven architecture centered around its custom Entity Component System (ECS). This high-level diagram illustrates the primary flow and interaction between the engine's core components during its lifecycle:

```mermaid
graph TD
    A[Bevy Application] --> B(Plugins: Extensible Modules);
    B --> C{Core Setup: Initialize ECS World & Schedules};
    C --> D[Game Loop Execution];

    subgraph Game Loop Stages
        D --> E(Input Processing & Event Handling);
        E -- Modifies/Reads --> F[ECS World: Entities, Components, Resources];
        F -- Data Synchronization --> G[Render World (GPU-ready Data)];
        G --> H(Rendering Backend: WGPU);
        H -- Presents Frame --> I[Display Output];
    end

    J[Asset Server] -- Loads Assets --> F;
    K[User Input] --> E;
    F -- Systems Operate On --> E;
```

## ⚡ Quick Start Guide
To get started with the Bevy Engine, ensure you have a recent version of Rust installed.

1.  **Clone the Repository:**
    ```bash
    git clone https://github.com/grewal16/bevy.git
    cd bevy
    ```

2.  **Run an Example (e.g., `hello_world`):**
    ```bash
    cargo run --example hello_world
    ```

    To run a specific example with all default features (highly recommended for beginners):
    ```bash
    cargo run --example <example_name> --features bevy_winit
    ```
    Replace `<example_name>` with any example found in the `examples/` directory (e.g., `3d_scene`, `sprite_animation`, `button`).

3.  **Build Your Own Project:**
    Start by creating a new Rust project:
    ```bash
    cargo new my_bevy_game
    cd my_bevy_game
    ```
    Add `bevy` as a dependency in your `Cargo.toml`:
    ```toml
    # Cargo.toml
    [dependencies]
    bevy = "0.14" # Use the latest version available
    ```
    Then, write your Bevy application in `src/main.rs`.

    ```rust
    // src/main.rs
    use bevy::prelude::*;

    fn main() {
        App::new()
            .add_plugins(DefaultPlugins)
            .add_systems(Startup, setup)
            .run();
    }

    fn setup(mut commands: Commands) {
        commands.spawn(Camera2dBundle::default());
        commands.spawn(SpriteBundle {
            sprite: Sprite {
                color: Color::rgb(0.7, 0.7, 0.7),
                custom_size: Some(Vec2::new(100.0, 100.0)),
                ..default()
            },
            ..default()
        });
    }
    ```
    Run your game:
    ```bash
    cargo run
    ```

## 📜 License
This project is dual-licensed under both the Apache 2.0 License and the MIT License. You may choose to use it under either license.

See [LICENSE-APACHE](LICENSE-APACHE) and [LICENSE-MIT](LICENSE-MIT) for more information.