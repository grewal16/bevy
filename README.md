```markdown
# 🚀 Bevy Engine

<p align="center"><img src="./assets/branding/banner.png" alt="Bevy Engine Banner" width="500"></p>

<p align="center">
  <a href="https://github.com/grewal16/bevy/stargazers"><img src="https://img.shields.io/github/stars/grewal16/bevy?style=for-the-badge" alt="GitHub stars"></a>
  <a href="https://github.com/grewal16/bevy/network/members"><img src="https://img.shields.io/github/forks/grewal16/bevy?style=for-the-badge" alt="GitHub forks"></a>
  <a href="https://github.com/grewal16/bevy/issues"><img src="https://img.shields.io/github/issues/grewal16/bevy?style=for-the-badge" alt="GitHub issues"></a>
  <a href="./LICENSE-MIT"><img src="https://img.shields.io/github/license/grewal16/bevy?style=for-the-badge" alt="GitHub license"></a>
</p>

## Short Description
Bevy is a refreshingly simple, yet powerful, data-driven game engine written in Rust. Designed for performance, modularity, and rapid iteration, Bevy empowers developers to create incredible games and interactive applications across all major platforms with ease and elegance.

## 🛡️ Project Health & Status
Bevy is under **active, continuous development** by a vibrant community. Robust CI/CD pipelines (`.github/workflows/`) ensure high code quality, stability, and broad platform compatibility, while extensive benchmarking (`benches/`) drives relentless performance optimization. Bevy is battle-tested and production-ready for your next project.

## ✨ Key Features
*   **Data-Driven ECS:** At its core, Bevy leverages a custom, highly performant Entity Component System (ECS) for unmatched flexibility and scalability.
*   **Powerful 2D & 3D Renderer:** A modern, PBR-based graphics pipeline built on WGPU, featuring advanced lighting, shadows, bloom, anti-aliasing (FXAA, TAA, DLSS), deferred rendering, screen-space reflections (SSR), and experimental real-time ray tracing (Solari RTGI/ReSTIR DI).
*   **Flexible UI System:** Declarative UI with CSS-like styling, supporting gradients, box shadows, dynamic layouts, and interactive widgets.
*   **Comprehensive Asset Management:** Robust asynchronous loading and hot-reloading for diverse assets, including GLTF models, images (KTX2, DDS, HDR), fonts, scenes, shaders (WGSL, GLSL), and audio (OGG).
*   **Cross-Platform Support:** Seamlessly target Windows, macOS, Linux, Web (WebAssembly), and Android from a single codebase.
*   **Animation & Input:** Integrated animation graphs for dynamic 2D/3D content and extensive input handling for keyboard, mouse, gamepad (Gilrs), and touch.
*   **Developer-Friendly Tools:** Built-in diagnostics, FPS overlay, a powerful gizmo system, and custom asset processing for streamlined development and debugging.
*   **Mathematical Foundations:** A comprehensive and optimized math library (`glam`) covering geometry, transformations, curves, and bounding volumes.

## Who is this for?
*   **Game Developers:** Seeking a high-performance, flexible, and rapidly iterating engine written in Rust.
*   **Graphics Programmers:** Interested in a modern, low-level rendering framework for custom graphics applications and research.
*   **Rust Enthusiasts:** Looking for a large, active, and well-maintained Rust project to contribute to or learn from.
*   **Engine Hackers:** Desiring a modular engine that allows deep customization and extension at all levels.

## Technology Stack & Architecture
*   **Core Language:** Rust
*   **Entity Component System (ECS):** Bevy's custom-built ECS for high performance and parallelism.
*   **Rendering Backend:** WGPU (a Rust-native implementation of WebGPU) provides cross-platform GPU abstraction.
*   **Shader Language:** WGSL (WebGPU Shading Language) and GLSL.
*   **Build System:** Cargo (Rust's package manager and build tool).
*   **Platform Integration:** Winit (native windowing), WebAssembly (for web targets), Android NDK (for Android targets).
*   **Key Libraries:** `glam` for efficient graphics math, `rodio` for audio playback, and `gilrs` for gamepad support.

## 📊 Architecture & Database Schema
The Bevy Engine is designed around a data-driven, modular architecture. The core loop, powered by its ECS, orchestrates systems that operate on components and resources.

```mermaid
graph TD
    A["User Input / External Event"] --> B{Bevy App};
    subgraph Bevy Engine Core
        B --> C[Scheduler: FixedUpdate, Update, PostUpdate...];
        C --> D{Plugins & Systems};
        subgraph ECS (Entity Component System)
            D -- Reads/Writes --> E[Resources];
            D -- Queries --> F[Components];
            F -- Attached to --> G[Entities];
            D -- Triggers --> H[Events];
        end
        H --> C;
    end
    B --> I[Render World Synchronization];
    I --> J[Rendering Backend (WGPU)];
    J --> K[Display Output];
```

## ⚙️ Configuration & Deployment
Bevy offers flexible configuration and deployment options:
*   **Rust Toolchain:** Requires a stable or nightly Rust toolchain, managed via `rustup`.
*   **Custom Cargo Configuration:** Optimized `.cargo/config_fast_builds.toml` is provided for faster compilation in development.
*   **CI/CD:** Automated builds, tests, and deployment checks are managed through GitHub Actions, including specific workflows for mobile and WebAssembly examples.
*   **Platform-Specific Builds:**
    *   **Android:** Use `cargo-apk` alongside the Android NDK. Refer to `examples/mobile` for setup and build instructions.
    *   **WebAssembly:** Compile with `wasm-bindgen` and serve with a basic web server. Detailed setup can be found in `examples/wasm`.

## ⚡ Quick Start Guide
1.  **Install Rust:** Ensure you have Rust installed by following the instructions at [rustup.rs](https://rustup.rs/).
2.  **Clone the Repository:**
    ```bash
    git clone https://github.com/grewal16/bevy.git
    cd bevy
    ```
3.  **Run a Bevy Example:** Explore the diverse capabilities of Bevy by running any of the examples:
    ```bash
    cargo run --example 3d_scene
    # Or, for 2D:
    cargo run --example sprite_animation
    # And for UI:
    cargo run --example button
    ```
    (Many more examples are available in the `examples/` directory!)
4.  **Start Your Own Project:** Create a new Rust project and add `bevy` as a dependency:
    ```bash
    cargo new my_bevy_game
    cd my_bevy_game
    # Add bevy dependency to Cargo.toml
    ```
    In `src/main.rs`, get started with a minimal app:
    ```rust
    use bevy::prelude::*;

    fn main() {
        App::new()
            .add_plugins(DefaultPlugins)
            .add_systems(Startup, setup_camera)
            .run();
    }

    fn setup_camera(mut commands: Commands) {
        commands.spawn(Camera2dBundle::default());
    }
    ```
5.  **For Web/Mobile Deployment:** Consult the comprehensive guides within the `examples/mobile` and `examples/wasm` directories for platform-specific setup and deployment instructions.

## 📜 License
This project is dual-licensed under both the **MIT License** and **Apache License (Version 2.0)**. You may choose either license to use this project.
*   [LICENSE-MIT](./LICENSE-MIT)
*   [LICENSE-APACHE](./LICENSE-APACHE)
```