# 🚀 Bevy Engine

<p align="center"><img src="./assets/branding/banner.png" alt="Bevy Engine Banner" width="500"></p>

<p align="center">
  <a href="https://github.com/grewal16/bevy/stargazers"><img src="https://img.shields.io/github/stars/grewal16/bevy?style=for-the-badge" alt="GitHub stars"></a>
  <a href="https://github.com/grewal16/bevy/network/members"><img src="https://img.shields.io/github/forks/grewal16/bevy?style=for-the-badge" alt="GitHub forks"></a>
  <a href="https://github.com/grewal16/bevy/issues"><img src="https://img.shields.io/github/issues/grewal16/bevy?style=for-the-badge" alt="GitHub issues"></a>
  <a href="./LICENSE-MIT"><img src="https://img.shields.io/github/license/grewal16/bevy?style=for-the-badge" alt="GitHub license"></a>
</p>

## Short Description
Bevy is a refreshingly simple and powerful data-driven game engine and app framework built in Rust. It's designed for maximum developer productivity, providing a complete feature set for 2D and 3D applications, from high-performance rendering to robust asset management and intuitive UI. Bevy empowers developers to build ambitious projects with speed and ease, all while leveraging Rust's renowned performance and safety.

## 🛡️ Project Health & Status
This project is in active and robust development, showcasing exceptional health and stability. Its continuous integration is meticulously managed through comprehensive GitHub Actions workflows, covering automated testing, static analysis (CodeQL), and dependency management (Dependabot). The presence of extensive benchmarks and compile-fail tests underscores a commitment to both performance and code correctness, making it a highly reliable and production-ready framework.

## ✨ Key Features
*   **Data-Driven ECS:** A custom, high-performance, and incredibly modular Entity Component System (ECS) at its core, enabling scalable and organized game logic.
*   **Stunning 2D/3D Graphics:** Supports Physically Based Rendering (PBR), advanced post-processing effects (Bloom, SSAO, SSR, Depth of Field, Anti-Aliasing with TAA, FXAA, SMAA, and DLSS integration), realistic atmospheric scattering, volumetric fog, and precise shadow mapping.
*   **Comprehensive Animation:** Features skeletal animation, flexible animation graphs for complex state machines, and morph targets for dynamic mesh deformations, all integrated with powerful easing functions.
*   **Multi-Platform Reach:** Seamlessly deployable across native platforms (Windows, Linux, macOS), mobile devices (Android, iOS), and the web (WebAssembly), maximizing your audience.
*   **Responsive UI System:** Build rich user interfaces with a flexible layout engine, built-in widgets, robust focus management, gradients, and customizable box shadows.
*   **Advanced Input Handling:** Full support for keyboard, mouse, gamepad (via Gilrs), and touch input, ensuring a broad range of interaction possibilities.
*   **Efficient Asset Pipeline:** A flexible asset loading and management system featuring hot-reloading for rapid iteration, custom asset readers and processors, and first-class GLTF support.
*   **Modular & Extensible:** Built as a collection of composable plugins and crates, allowing developers to pick and choose components and easily extend the engine.
*   **Powerful Dev Tools:** Includes an FPS overlay, advanced profiling tools, and an interactive scene viewer to streamline debugging and optimization.
*   **Experimental Ray Tracing:** Explores real-time ray tracing capabilities with the Solari plugin for cutting-edge visual effects.

## Who is this for?
Bevy is ideal for Rust developers and teams aiming to create high-performance 2D and 3D games, interactive applications, or complex simulations. Its data-driven design appeals to those who value performance, modularity, and a clean architecture. Whether you're building a small indie game or a large-scale application, Bevy provides the tools and flexibility to bring your vision to life.

## Technology Stack & Architecture
*   **Core Language:** Rust (`.rs` files, `Cargo.toml`)
*   **Engine Core:** Bevy's custom Entity Component System (ECS), Application, Transform, Asset, Input, Window, Time, Log, and Diagnostic crates.
*   **Rendering Backend:** WGPU (a Rust implementation of WebGPU), allowing for high-performance, cross-platform graphics.
*   **Shading Languages:** WGSL (WebGPU Shading Language) for modern GPU programming, with support for GLSL and WSL.
*   **Windowing & Events:** Winit (for native platforms) and WebSys (for WebAssembly).
*   **Gamepad Support:** Gilrs library for comprehensive gamepad input.
*   **UI Layout Engine:** Integrates `taffy` for a powerful, flexible, and performant UI layout system.
*   **Asset Formats:** Supports a wide array including GLTF/GLB (3D models), PNG, JPG, HDR, EXR, KTX2 (images), OGG (audio), TTF (fonts), and RON (custom data serialization).
*   **Asynchronous Tasks:** Leverages Bevy's integrated task pool for efficient parallel processing and I/O.
*   **Build & CI:** Utilizes Cargo for dependency management and building, and relies on GitHub Actions for robust Continuous Integration and deployment.
*   **Target Platforms:** Designed for cross-platform compatibility, including Windows, Linux, macOS, Android, and WebAssembly.

## 📊 Architecture & Database Schema

The Bevy engine architecture is highly modular and data-driven, primarily operating across a main thread (App/ECS) and a dedicated render thread (GPU).

```mermaid
graph TD
    subgraph User Input & OS Events
        A["OS/Platform Events (Winit)"] --> B{{"Input Events (Keyboard, Mouse, Gamepad, Touch)"}};
        B --> BevyInput["Bevy Input Plugin"];
    end

    subgraph Bevy Core Loop (Main Thread)
        C_START["App Start"] --> C1["Startup Schedule"];
        C1 --> C2["Main Schedule (e.g., Update, FixedUpdate)"];
        subgraph ECS Processing
            D["ECS World (Entities, Components, Resources)"] --> E["Systems & Business Logic"];
            E --> F["Commands (Deferred Operations)"];
            F --> D;
        end
        C2 --> E;
        BevyInput --> C2;
        BevyAsset["Asset Plugin"] --> C2;
        BevyAudio["Audio Plugin"] --> C2;
        BevyUI["UI Plugin"] --> C2;
        BevyWindow["Window Plugin"] --> C2;
        E_TASKS["Bevy Task Pool (Async)"] --> E;
    end

    subgraph Render Pipeline (Render Thread)
        R_EXTRACT("Render Extraction (From ECS)") --> R_PREP("Render Asset Preparation");
        R_PREP --> R_QUEUE("Draw Command Queueing");
        R_QUEUE --> R_PHASES("Render Phases (Opaque, Transparent, UI, Post-Process)");
        R_PHASES --> R_GPU("GPU Execution (WGPU)");
        R_GPU --> R_PRESENT("Present to Window/Framebuffer");
        C2 -- "Renderable Data" --> R_EXTRACT;
        BevyWindow --> R_PRESENT;
    end

    style C_START fill:#add8e6,stroke:#333,stroke-width:2px;
    style C_END fill:#add8e6,stroke:#333,stroke-width:2px;
    style R_PRESENT fill:#add8e6,stroke:#333,stroke-width:2px;
    classDef plugin fill:#90ee90,stroke:#333,stroke-width:2px;
    class BevyInput,BevyAsset,BevyAudio,BevyUI,BevyWindow,BevyRender plugin;
```

## ⚙️ Configuration & Deployment
Bevy projects are built using `cargo`. For examples, navigate to the project root and run `cargo run --example <example_name>`.

*   **Native Development:**
    *   Ensure Rust is installed via `rustup`.
    *   Fast builds can be configured in `.cargo/config_fast_builds.toml`.
*   **Mobile (Android):**
    *   Requires Android NDK and `cargo-apk`.
    *   Build with `cargo apk --release` from the example directory.
*   **Mobile (iOS):**
    *   Utilizes Xcode projects for iOS deployment (e.g., `bevy_mobile_example.xcodeproj`).
    *   The `build_rust_deps.sh` script assists in compiling Rust dependencies for iOS.
*   **Web (WASM):**
    *   Requires `wasm-bindgen` and `trunk` for deployment.
    *   Example setup can be found under `examples/wasm`.
*   **CI/CD:** Leverages GitHub Actions (`.github/workflows/`) for automated build, test, and deployment processes.

## ⚡ Quick Start Guide

To get started with Bevy, ensure you have Rust installed via [rustup.rs](https://rustup.rs/).

1.  **Clone the Bevy repository:**
    ```bash
    git clone https://github.com/grewal16/bevy.git
    cd bevy
    ```

2.  **Run an example:**
    ```bash
    cargo run --example breakout
    ```
    This will compile and run the "breakout" game example. You can find many more examples in the `examples/` directory.

3.  **Start your own Bevy project:**
    Create a new Rust project:
    ```bash
    cargo new --bin my_bevy_game
    cd my_bevy_game
    ```
    Add Bevy as a dependency to your `Cargo.toml`:
    ```toml
    # Cargo.toml
    [dependencies]
    bevy = "0.13" # Use the latest stable Bevy version
    ```
    Create a simple Bevy application in `src/main.rs`:
    ```rust
    // src/main.rs
    use bevy::prelude::*;

    fn main() {
        App::new()
            .add_plugins(DefaultPlugins)
            .add_systems(Startup, setup)
            .add_systems(Update, greet_people)
            .run();
    }

    fn setup(mut commands: Commands) {
        commands.spawn(Camera2dBundle::default());
        commands.spawn(
            TextBundle::from_section(
                "Hello, Bevy!",
                TextStyle {
                    font_size: 100.0,
                    color: Color::WHITE,
                    ..default()
                },
            )
            .with_text_alignment(TextAlignment::Center)
            .with_style(Style {
                position_type: PositionType::Absolute,
                left: Val::Percent(50.),
                top: Val::Percent(50.),
                ..default()
            }),
        );
    }

    fn greet_people() {
        // This system could do something in a loop, but for a minimal example, it just exists.
    }
    ```
    Run your new Bevy application:
    ```bash
    cargo run
    ```

## 📜 License
This project is dual-licensed under both the MIT License and the Apache License, Version 2.0. You may choose either license to govern your use of this software.

See [LICENSE-MIT](LICENSE-MIT) for details on the MIT License.
See [LICENSE-APACHE](LICENSE-APACHE) for details on the Apache License, Version 2.0.