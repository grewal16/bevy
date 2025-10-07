# 🚀 Bevy Engine

<p align="center"><img src="./assets/branding/banner.png" alt="Bevy Engine Banner" width="700"></p>

<p align="center">
  <a href="https://github.com/grewal16/bevy/stargazers"><img src="https://img.shields.io/github/stars/grewal16/bevy?style=for-the-badge" alt="GitHub stars"></a>
  <a href="https://github.com/grewal16/bevy/network/members"><img src="https://img.shields.io/github/forks/grewal16/bevy?style=for-the-badge" alt="GitHub forks"></a>
  <a href="https://github.com/grewal16/bevy/issues"><img src="https://img.shields.io/github/issues/grewal16/bevy?style=for-the-badge" alt="GitHub issues"></a>
  <a href="./LICENSE-MIT"><img src="https://img.shields.io/github/license/grewal16/bevy?style=for-the-badge" alt="GitHub license"></a>
</p>

## Short Description
Bevy is a refreshingly simple and powerful data-driven game engine built in Rust. It's designed for maximum flexibility, performance, and developer ergonomics, allowing you to build anything from small 2D games to complex 3D simulations. With its modular architecture, Bevy provides a solid foundation for game development with a focus on ECS (Entity Component System), modern rendering pipelines, and extensive asset management.

## 🛡️ Project Health & Status
Bevy is in active and robust development. A comprehensive suite of unit and integration tests, alongside extensive GitHub Actions workflows (`.github/workflows/ci.yml`, `docs.yml`, `example-run.yml`), ensures high code quality, stability, and continuous validation across multiple platforms (including mobile and WASM). Benchmarks are actively maintained (`benches/`), demonstrating a strong commitment to performance.

## ✨ Key Features
*   **Entity Component System (ECS):** A highly performant and flexible ECS architecture for managing game state and logic.
*   **Modular Design:** Built as a collection of independent crates, allowing developers to pick and choose components or extend functionality with ease.
*   **Modern 2D/3D Rendering:** Physically Based Rendering (PBR), advanced lighting (directional, point, spot), real-time shadows, post-processing effects (Bloom, SSAO, SSR, Volumetric Fog), and multiple anti-aliasing options (FXAA, SMAA, TAA, DLSS).
*   **Animation System:** Support for animated meshes, skinned meshes, morph targets, and flexible animation graphs.
*   **Advanced UI Toolkit:** Declarative UI system with flexible layout, interaction management, widgets (buttons, checkboxes, sliders), and robust navigation (directional, tab).
*   **Comprehensive Asset Management:** Load 3D models (GLTF/GLB), images, fonts, audio, and custom asset types with hot-reloading capabilities.
*   **Input Handling:** Full support for keyboard, mouse, gamepad (with rumble), and touch input events.
*   **Diagnostics & Profiling:** Integrated tools for monitoring performance, FPS overlays, and system information.
*   **Web & Mobile Support:** Build for WebAssembly (WASM) and Android/iOS platforms.
*   **Gizmos:** In-editor visualization tools for debugging and development of 2D/3D scenes, lights, and physics.
*   **Real-time Ray Tracing (Bevy Solari):** Experimental features for advanced global illumination.

## Who is this for?
Bevy is ideal for:
*   **Game Developers:** From hobbyists to professional studios looking for a powerful, open-source, and unopinionated engine.
*   **Rust Enthusiasts:** Developers passionate about Rust and wanting to build performant, low-level applications in a safe and modern environment.
*   **Engine Hackers:** Those who love to dive deep, extend, and customize core engine functionality.
*   **Educational Purposes:** Its clear, modular design and excellent documentation make it a great tool for learning game development and Rust programming.

## Technology Stack & Architecture

Bevy is written almost entirely in **Rust**, leveraging its performance, memory safety, and concurrency features.

*   **Core Language:** Rust
*   **Graphics Backend:** `wgpu` (WebGPU implementation), supporting Vulkan, Metal, DX12, OpenGL, and WebGPU targets.
*   **Shader Language:** WGSL (WebGPU Shading Language), with support for GLSL.
*   **Windowing:** `winit` (cross-platform windowing library).
*   **Input Handling:** `gilrs` (gamepad input), `winit` (keyboard, mouse, touch).
*   **Asset Serialization:** Primarily `RON` (Rust Object Notation) for its human-readability and strong typing.
*   **Asset Formats:** GLTF/GLB for 3D models, PNG/JPG/HDR/EXR/KTX2 for images, TTF for fonts, OGG for audio.

The engine follows a highly **modular, data-driven architecture**, built around the **Bevy ECS**. Each major feature (rendering, UI, audio, animation, etc.) resides in its own crate, allowing for granular control and easy customization.

```mermaid
graph TD
    UserInputs(Input Events) --> App(Bevy App Schedule);

    subgraph Bevy Engine Loop
        App --> PreUpdatePhase(Pre-Update);
        PreUpdatePhase --> CoreLogic(Core Game Logic & State Updates);
        CoreLogic --> AnimationSystem(Animation & Scene Graph Updates);
        AnimationSystem --> RenderExtract(Extract Render Data);
        RenderExtract --> RenderSchedule(Render Schedule);
        RenderSchedule --> PostRender(Post-Render Processing);
        PostRender --> Display(Window & UI Display);
        Display --> CleanUp(Cleanup);
    end

    subgraph Core Components (crates)
        CoreLogic --- BevyECS(bevy_ecs: Entity Component System);
        CoreLogic --- BevyTransform(bevy_transform: Transforms & Hierarchy);
        CoreLogic --- BevyInput(bevy_input: Keyboard, Mouse, Gamepad, Touch);
        CoreLogic --- BevyTime(bevy_time: Timers & Clocks);
        
        AnimationSystem --- BevyAnimation(bevy_animation: Keyframes, Interpolation, Graphs);

        RenderExtract --- BevyAsset(bevy_asset: Asset Loading & Management);
        RenderExtract --- BevyRender(bevy_render: Low-level Graphics API);
        RenderExtract --- BevyPBR(bevy_pbr: PBR Materials, Lighting, Shadows);
        RenderExtract --- BevySprite(bevy_sprite: 2D Graphics, Text2D);
        RenderExtract --- BevyCamera(bevy_camera: Projections, Viewports);
        RenderExtract --- BevyUI(bevy_ui: Layout, Interaction, Widgets);
        RenderExtract --- BevyAudio(bevy_audio: Spatial Audio, Playback);
        RenderExtract --- BevySolari(bevy_solari: Realtime Ray Tracing);
    end

    App -.-> BevyDiagnostic(bevy_diagnostic: Performance Metrics);
    App -.-> BevyDevTools(bevy_dev_tools: Debug Overlays, Picking);

    style UserInputs fill:#f9f,stroke:#333,stroke-width:2px;
    style App fill:#b0f,stroke:#333,stroke-width:2px;
    style Display fill:#9ff,stroke:#333,stroke-width:2px;
    style BevyECS fill:#cbe,stroke:#333,stroke-width:1px;
    style BevyTransform fill:#cbe,stroke:#333,stroke-width:1px;
    style BevyInput fill:#cbe,stroke:#333,stroke-width:1px;
    style BevyTime fill:#cbe,stroke:#333,stroke-width:1px;
    style BevyAnimation fill:#cbe,stroke:#333,stroke-width:1px;
    style BevyAsset fill:#cbe,stroke:#333,stroke-width:1px;
    style BevyRender fill:#cbe,stroke:#333,stroke-width:1px;
    style BevyPBR fill:#cbe,stroke:#333,stroke-width:1px;
    style BevySprite fill:#cbe,stroke:#333,stroke-width:1px;
    style BevyCamera fill:#cbe,stroke:#333,stroke-width:1px;
    style BevyUI fill:#cbe,stroke:#333,stroke-width:1px;
    style BevyAudio fill:#cbe,stroke:#333,stroke-width:1px;
    style BevySolari fill:#cbe,stroke:#333,stroke-width:1px;
    style BevyDiagnostic fill:#ffe,stroke:#333,stroke-width:1px;
    style BevyDevTools fill:#ffe,stroke:#333,stroke-width:1px;
```

## ⚙️ Configuration & Deployment
Bevy projects are configured using standard Rust `Cargo.toml` files for dependency management.
For performance-critical builds, custom `.cargo/config_fast_builds.toml` settings are provided.

*   **Desktop (Rust):** Standard `cargo build` and `cargo run` commands are used.
*   **Web (WASM):** Requires `wasm-pack` for compilation and a local web server to serve the output files (HTML, JS, WASM).
*   **Mobile (Android/iOS):** Android builds require the Android NDK and specific `cargo apk` commands. iOS development typically involves Xcode and command-line tools, building Rust libraries for the iOS target.

## ⚡ Quick Start Guide

To get started with your own Bevy project:

1.  **Install Rust:** If you don't have Rust, install it using `rustup`:
    ```bash
    curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh
    ```
2.  **Create a New Bevy Project:**
    ```bash
    cargo new my_bevy_game
    cd my_bevy_game
    ```
3.  **Add Bevy as a Dependency:** Modify `Cargo.toml` to include Bevy:
    ```toml
    [dependencies]
    bevy = "0.13" # Or the latest version
    ```
4.  **Run an Example (e.g., Hello World):**
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
                color: Color::rgb(0.25, 0.25, 0.75),
                custom_size: Some(Vec2::new(50.0, 50.0)),
                ..default()
            },
            transform: Transform::from_xyz(0.0, 0.0, 0.0),
            ..default()
        });
    }
    ```
    Then run:
    ```bash
    cargo run
    ```
    Explore more examples in the `examples/` directory for specific features like 3D, UI, animation, and more!

## 📜 License
This project is dual-licensed under both the **MIT License** and the **Apache License (Version 2.0)**. You may choose either license to use this software.
*   [LICENSE-MIT](./LICENSE-MIT)
*   [LICENSE-APACHE](./LICENSE-APACHE)