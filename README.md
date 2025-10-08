# 🚀 Bevy: A Data-Driven Game Engine and App Framework

<p align="center"><img src="./assets/branding/banner.png" alt="Bevy Engine Banner" width="500"></p>

<p align="center">
  <a href="https://github.com/grewal16/bevy/stargazers"><img src="https://img.shields.io/github/stars/grewal16/bevy?style=for-the-badge" alt="GitHub stars"></a>
  <a href="https://github.com/grewal16/bevy/network/members"><img src="https://img.shields.io/github/forks/grewal16/bevy?style=for-the-badge" alt="GitHub forks"></a>
  <a href="https://github.com/grewal16/bevy/issues"><img src="https://img.shields.io/github/issues/grewal16/bevy?style=for-the-badge" alt="GitHub issues"></a>
  <a href="./LICENSE-MIT"><img src="https://img.shields.io/github/license/grewal16/bevy?style=for-the-badge" alt="GitHub license"></a>
</p>

## Short Description
Bevy is a refreshingly modular and high-performance data-driven game engine and app framework built in Rust. It empowers developers to create stunning 2D and 3D experiences with unparalleled flexibility and speed. Designed for maximum developer ergonomics and scalability, Bevy handles everything from rendering to asset management, input, and physics, allowing you to focus on bringing your creative visions to life.

## 🛡️ Project Health & Status
Bevy is under active, high-velocity development, driven by a vibrant open-source community. Project health is robust, featuring comprehensive continuous integration pipelines via GitHub Actions (including `ci.yml`, `codeql.yml`, and `example-run.yml`). Extensive unit tests, benchmarks, and compile-fail tests ensure code quality, stability, and optimal performance across all modules.

## ✨ Key Features
*   **Data-Driven ECS:** A powerful, cache-friendly Entity Component System for highly performant and flexible game logic.
*   **PBR Rendering:** Physically Based Rendering for realistic 3D graphics, including advanced lighting, shadows, and post-processing effects.
*   **Comprehensive Animation:** Support for skeletal animation, morph targets, and advanced animation graphs.
*   **Flexible UI Framework:** A declarative and ergonomic UI system, perfect for in-game menus and application interfaces.
*   **Modular Asset Pipeline:** Efficient asset loading and management with built-in support for GLTF, images, audio, and custom asset types.
*   **Cross-Platform Input:** Unified input handling for keyboard, mouse, gamepad, and touch across various platforms.
*   **Realtime Raytracing:** Experimental support for high-fidelity, real-time raytracing using the Solari module.
*   **Powerful Math & Transforms:** Optimized math primitives and a robust scene graph for 2D and 3D transformations.
*   **Developer Tools:** Integrated diagnostics, logging, and debugging overlays to streamline development.
*   **Asynchronous Task System:** High-performance multi-threaded task management for parallel workloads.

## Who is this for?
Bevy is ideal for:
*   Game developers seeking a modern, high-performance, and modular engine.
*   Graphics programmers interested in low-level control and cutting-edge rendering techniques.
*   Developers building real-time interactive applications and simulations.
*   Rust enthusiasts who value a strong type system, performance, and a growing ecosystem.

## Technology Stack & Architecture
Bevy is predominantly written in **Rust**, leveraging its safety, concurrency, and performance features. The build system is powered by **Cargo**. Graphics rendering is built upon **WebGPU** through `wgpu`, allowing for broad compatibility.

**Key Components:**
*   **`bevy_app`**: The application lifecycle and plugin management.
*   **`bevy_ecs`**: The core data-driven Entity Component System.
*   **`bevy_render`**: Low-level rendering primitives and pipeline management.
*   **`bevy_pbr`**: Physically Based Rendering implementation.
*   **`bevy_animation`**: Handles skeletal, morph, and graph-based animations.
*   **`bevy_ui`**: Manages UI element layout and interaction.
*   **`bevy_asset`**: Generic asset loading, hot-reloading, and processing.
*   **`bevy_gltf`**: Integrates GLTF model loading.
*   **`bevy_audio`**: Sound playback and spatial audio.
*   **`bevy_input`**, **`bevy_gilrs`**: Input event handling across devices.
*   **`bevy_window`**, **`bevy_winit`**: Cross-platform window creation and management.
*   **`bevy_solari`**: Experimental real-time raytracing module.

## 📊 Architecture & Database Schema
```mermaid
graph TD
    A[Bevy Application] --> B(Plugin Management);
    B --> C[Core Systems (ECS, Events, Schedules)];

    C --> D1[Rendering Pipeline];
    D1 -- "powered by" --> D1_1(bevy_render);
    D1_1 -- "implements" --> D1_2(bevy_pbr);
    D1_1 -- "uses" --> D1_3(bevy_shader);
    D1 -- "specialized by" --> D1_4(bevy_solari - Raytracing);

    C --> D2[Asset Management];
    D2 -- "core logic" --> D2_1(bevy_asset);
    D2 -- "specific loaders" --> D2_2(bevy_gltf);
    D2 -- "media assets" --> D2_3(bevy_image, bevy_audio, bevy_text);

    C --> D3[User Interface];
    D3 -- "layout & interactions" --> D3_1(bevy_ui);
    D3 -- "widgets" --> D3_2(bevy_core_widgets, bevy_feathers);

    C --> D4[Input & Windowing];
    D4 -- "window API" --> D4_1(bevy_window, bevy_winit);
    D4 -- "device input" --> D4_2(bevy_input, bevy_gilrs);

    C --> D5[Animation System];
    D5 -- "logic" --> D5_1(bevy_animation);

    C --> D6[Utilities & Diagnostics];
    D6 -- "low-level tools" --> D6_1(bevy_math, bevy_transform, bevy_tasks, bevy_platform);
    D6 -- "monitoring" --> D6_2(bevy_log, bevy_diagnostic, bevy_dev_tools);

    D1 --> F[GPU (WebGPU API)];
    D1_4 --> F;
    D4_1 --> F;
    D2_3 --> D1; 
    D3 --> D1;

    F -- "Rendered Output" --> G[Display / Window];
    D4_2 -- "User Interactions" --> G;
    G --> A;
```

## ⚙️ Configuration & Deployment
Bevy projects are configured using standard Rust `Cargo.toml` files, allowing for easy dependency management and feature toggling (`docs/cargo_features.md`).

**Build & Run:**
The project is built using `cargo`. Configuration for fast builds is provided in `.cargo/config_fast_builds.toml`.
For mobile deployment (`examples/mobile`): Android projects require the Android NDK, and iOS projects are set up within Xcode.
For web deployment (`examples/wasm`): Projects can be built for WebAssembly, requiring `wasm-bindgen` and a simple web server.

## ⚡ Quick Start Guide
1.  **Install Rust:** If you don't have Rust installed, follow the instructions on [rustup.rs](https://rustup.rs/).
2.  **Clone the repository:**
    ```bash
    git clone https://github.com/grewal16/bevy.git
    cd bevy
    ```
3.  **Run an example:** To see Bevy in action, run one of the many examples. For instance, a 3D scene:
    ```bash
    cargo run --release --example 3d_scene
    ```
    Or a 2D sprite animation:
    ```bash
    cargo run --release --example sprite_animation
    ```
    Explore the `examples/` directory for more!

## 📜 License
This project is dual-licensed under either:
*   Apache License, Version 2.0 ([`LICENSE-APACHE`](./LICENSE-APACHE))
*   MIT license ([`LICENSE-MIT`](./LICENSE-MIT))

at your option.