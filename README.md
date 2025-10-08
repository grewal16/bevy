# 🚀 Bevy Engine

<p align="center"><img src="./assets/branding/banner.png" alt="Bevy Engine Logo" width="500"></p>

<p align="center">
  <a href="https://github.com/grewal16/bevy/stargazers"><img src="https://img.shields.io/github/stars/grewal16/bevy?style=for-the-badge" alt="GitHub stars"></a>
  <a href="https://github.com/grewal16/bevy/network/members"><img src="https://img.shields.io/github/forks/grewal16/bevy?style=for-the-badge" alt="GitHub forks"></a>
  <a href="https://github.com/grewal16/bevy/issues"><img src="https://img.shields.io/github/issues/grewal16/bevy?style=for-the-badge" alt="GitHub issues"></a>
  <a href="./LICENSE-MIT"><img src="https://img.shields.io/github/license/grewal16/bevy?style=for-the-badge" alt="GitHub license"></a>
</p>

## Short Description
Bevy is a refreshingly simple, yet powerfully extensible data-driven game engine built in Rust. Designed for maximum productivity and performance, Bevy empowers developers to create ambitious 2D and 3D games and applications with ease, embracing a modular architecture that puts you in control.

## ✨ Key Features
*   **Entity Component System (ECS)**: At its core, Bevy leverages a highly optimized, parallel ECS to manage game state and logic, enabling efficient and scalable game development.
*   **Comprehensive 2D & 3D Rendering**: From intricate PBR materials and dynamic lighting to advanced post-processing effects like Bloom, SSAO, SSR, volumetric fog, and various anti-aliasing techniques (FXAA, TAA, SMAA, DLSS), Bevy delivers stunning visuals out-of-the-box.
*   **Flexible Asset Pipeline**: Manage diverse asset types including 3D models (GLTF, GLB), textures (PNG, KTX2), shaders (WGSL, GLSL), sounds (OGG), and fonts. Enjoy hot reloading for rapid iteration.
*   **Powerful Animation System**: Bring your worlds to life with support for complex animations, including skinned meshes, morph targets, and advanced animation graphs for sophisticated character movements.
*   **Responsive User Interface (UI)**: Build engaging user interfaces with a flexible UI system supporting declarative layouts, dynamic interactions, visual gradients, scrollbars, text input, and custom widgets.
*   **Intuitive Input Handling**: Capture and respond to a wide range of user inputs, including keyboard, mouse, gamepad, and touch, ensuring broad compatibility and accessibility for your applications.
*   **Spatial Audio Capabilities**: Immerse players in rich soundscapes with integrated audio playback and spatial audio features for realistic sound positioning.
*   **Cross-Platform Development**: Deploy your creations across multiple platforms, including desktop (Linux, Windows, macOS), Android, and WebAssembly (WASM), thanks to its platform-agnostic design.
*   **Debug & Development Tools**: Utilize built-in gizmos for visual debugging, performance diagnostics, and other developer-centric utilities to streamline your workflow.
*   **Modular & Extensible**: Bevy's "plugin-first" approach means you only include what you need, making it incredibly flexible and easy to extend with custom features.

## Who is this for?
Bevy is ideal for:
*   **Game Developers**: Looking for a modern, high-performance engine to build 2D and 3D games.
*   **Rustaceans**: Eager to leverage their Rust skills in the exciting domain of game development.
*   **Graphics & Engine Enthusiasts**: Interested in a transparent, extensible engine architecture for experimentation and deep customization.
*   **Educators & Learners**: Providing a clean, well-documented codebase for understanding game engine principles.

## Technology Stack & Architecture
Bevy is primarily written in **Rust**, a language renowned for its performance, memory safety, and concurrency. The rendering backend leverages **WGPU** for cross-platform GPU abstraction, utilizing **WGSL** (WebGPU Shading Language) for shader development. It supports industry-standard asset formats like **GLTF/GLB** for 3D models and **KTX2** for compressed textures. Its architecture is deeply rooted in an **Entity Component System (ECS)** paradigm, allowing for highly parallel and organized game logic.

## 📊 Architecture & Database Schema
The Bevy Engine's architecture is a prime example of a modern, data-driven design. The core `App` orchestrates a series of `Schedules`, each comprising `Systems` that operate on the `World`'s `Resources` and `Components`. Data flows through well-defined phases, enabling highly parallel execution and clear separation of concerns.

```mermaid
graph TD
    A[App (main)] --> B{Plugins};
    B --> C(Schedules);
    C -- FixedUpdate --> D(Systems);
    C -- Update --> D;
    C -- PostUpdate --> D;
    D --> E(World State - Components & Resources);
    E --> F[Render World (Extract)];
    F --> G(Render Phases);
    G --> H[GPU Commands (WGPU)];
    H --> I(Display Output);
    I --> J[Input Events];
    J --> C;
```

## ⚡ Quick Start Guide
To get started with Bevy, ensure you have Rust installed (via `rustup`).

1.  **Clone the Repository**:
    ```bash
    git clone https://github.com/grewal16/bevy.git
    cd bevy
    ```
2.  **Run an Example**:
    Bevy comes with a rich set of examples to showcase its capabilities. You can run any example using Cargo:
    ```bash
    cargo run --example 3d_scene
    ```
    For a 2D example:
    ```bash
    cargo run --example sprite
    ```
    Explore the `examples/` directory for many more.

3.  **Build Your Own Project**:
    Create a new Rust project and add `bevy` as a dependency in your `Cargo.toml`:
    ```toml
    [dependencies]
    bevy = "0.13" # Or the latest version
    ```
    Then, create your `main.rs` file and start building your game!

## 📜 License
This project is dual-licensed under both the **Apache 2.0 License** and the **MIT License**. You may choose which license to use.

*   [Apache 2.0 License](./LICENSE-APACHE)
*   [MIT License](./LICENSE-MIT)