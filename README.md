# 🚀 Bevy Engine

<p align="center"><img src="./assets/branding/banner.png" alt="Bevy Engine Banner" width="700"></p>

<p align="center">
  <a href="https://github.com/grewal16/bevy/stargazers"><img src="https://img.shields.io/github/stars/grewal16/bevy?style=for-the-badge" alt="GitHub stars"></a>
  <a href="https://github.com/grewal16/bevy/network/members"><img src="https://img.shields.io/github/forks/grewal16/bevy?style=for-the-badge" alt="GitHub forks"></a>
  <a href="https://github.com/grewal16/bevy/issues"><img src="https://img.shields.io/github/issues/grewal16/bevy?style=for-the-badge" alt="GitHub issues"></a>
  <a href="./LICENSE-APACHE"><img src="https://img.shields.io/github/license/grewal16/bevy?style=for-the-badge" alt="GitHub license"></a>
</p>

## Short Description
Bevy is a refreshingly simple, yet powerful data-driven game engine built in Rust. It's designed for maximum productivity and performance, leveraging a modern Entity Component System (ECS) architecture to create anything from intricate 2D games to stunning 3D worlds. Bevy empowers developers with full control and modularity, making it ideal for crafting bespoke game experiences.

## 🛡️ Project Health & Status
Bevy is in active, highly accelerated development, boasting a robust and comprehensive Continuous Integration (CI/CD) pipeline powered by GitHub Actions. This ensures every commit is rigorously tested for correctness, performance regressions are identified early through dedicated benchmarks, and code quality is maintained with automated linting and security analysis (CodeQL). The project benefits from structured issue templates, clear contribution guidelines, and continuous documentation efforts, reflecting a healthy, community-driven, and production-ready ecosystem.

## ✨ Key Features
*   **Entity Component System (ECS):** A cache-friendly, data-driven architecture that maximizes performance and flexibility for game logic.
*   **Powerful 2D & 3D Rendering:** Leverage modern PBR (Physically Based Rendering), advanced lighting (directional, point, spot lights, light probes, lightmaps), shadow mapping (PCSS), and post-processing effects including Bloom, Depth of Field, SSAO, SSR, and Volumetric Fog. Experimental real-time ray tracing (Solari) hints at future capabilities.
*   **Flexible Animation System:** Support for skeletal animation, morph targets, and advanced animation graphs for lifelike character movement and dynamic scene elements.
*   **Declarative User Interface (UI):** Build responsive and interactive user interfaces with a powerful UI framework, supporting complex layouts, gradients, and customizable widgets.
*   **Cross-Platform Support:** Seamlessly deploy your applications across Desktop (Windows, macOS, Linux), Web (WebAssembly), and Mobile (Android, iOS).
*   **Intuitive Asset Management:** Hot-reloading of assets, support for industry-standard formats like GLTF, custom asset types, and efficient background loading.
*   **Robust Input Handling:** Comprehensive input system supporting keyboard, mouse, touch, and gamepad inputs with custom rumble effects.
*   **Audio Engine:** Play and control 2D and 3D spatial audio with pitch and volume manipulation.
*   **Developer Tools:** Integrated debugging with gizmos, FPS overlays, and diagnostics for performance monitoring and rapid iteration.

## Who is this for?
Bevy is perfect for:
*   **Game Developers:** Seeking a performant, flexible, and opinionated game engine that offers deep control and leverages modern Rust development practices.
*   **Engine Developers & Researchers:** Interested in exploring advanced rendering techniques, ECS architectures, and contributing to a growing open-source project.
*   **Rust Enthusiasts:** Looking for a challenging and rewarding project to build games and applications using their favorite language.
*   **Those Building Simulations:** The robust ECS and rendering capabilities make it suitable for a wide range of interactive simulations beyond traditional games.

## Technology Stack & Architecture
Bevy is built entirely in **Rust**, a language renowned for its performance, memory safety, and concurrency.

*   **Core Language:** Rust
*   **Graphics Backend:** Utilizes **WGPU**, a Rust-native, cross-platform graphics API that provides a modern, low-level interface over Vulkan, Metal, DirectX 12, and WebGPU.
*   **Shading Language:** Primarily **WGSL** (WebGPU Shading Language), with support for GLSL for custom materials.
*   **Build System:** **Cargo**, Rust's powerful package manager and build tool.
*   **Cross-Platform:** Employs **Winit** for window management, enabling broad desktop and mobile support. WebAssembly (WASM) targets extend reach to the web.
*   **Asset Serialization:** Leverages **RON** (Rusty Object Notation) for declarative scene and asset definitions.
*   **CI/CD:** Orchestrated by **GitHub Actions** for continuous testing, benchmarking, and quality assurance.

## 📊 Architecture & Database Schema
Bevy's architecture revolves around a highly performant and modular **Entity Component System (ECS)**. Unlike traditional object-oriented game engines, Bevy separates data (Components), behavior (Systems), and unique identifiers (Entities) for optimal data locality and parallelism. The engine's core loop orchestrates these elements, feeding into a flexible render graph.

```mermaid
graph TD
    A["User Input / OS Events"] --> B["Bevy App (Main Loop)"];
    subgraph ECS World
        B -- Runs Schedules --> C[Systems (Data-driven Logic)];
        C -- Manipulate --> D["Components (Raw Data)"];
        D -- Attached to --> E["Entities (Unique IDs)"];
        E -- Grouped by --> F["Archetypes (Component Combinations)"];
        D -- Processes --> G[Resources (Global Data)];
        C -- Execute Commands --> H[Commands Queue];
        H -- Applied after Systems --> I{"Deferred Changes"};
    end
    I -- Extract Render Data --> J["Render World"];
    J -- Passed to --> K["Render Graph (GPU Instructions)"];
    K --> L["GPU / Window Output"];

    style A fill:#e0f7fa,stroke:#00bcd4,stroke-width:2px;
    style B fill:#fff3e0,stroke:#ff9800,stroke-width:2px;
    style C fill:#e8f5e9,stroke:#4caf50,stroke-width:2px;
    style D fill:#fbe9e7,stroke:#ff5722,stroke-width:2px;
    style E fill:#e0f2f7,stroke:#2196f3,stroke-width:2px;
    style F fill:#fce4ec,stroke:#e91e63,stroke-width:2px;
    style G fill:#f3e5f5,stroke:#9c27b0,stroke-width:2px;
    style H fill:#e3f2fd,stroke:#2196f3,stroke-width:2px;
    style I fill:#f9fbe7,stroke:#8bc34a,stroke-width:2px;
    style J fill:#f8bbd0,stroke:#e91e63,stroke-width:2px;
    style K fill:#fffde7,stroke:#ffc107,stroke-width:2px;
    style L fill:#efebe9,stroke:#795548,stroke-width:2px;
```

## ⚙️ Configuration & Deployment
Bevy projects are configured primarily through Rust's `Cargo.toml` for dependencies and features. Custom build profiles are defined in `.cargo/config_fast_builds.toml` for optimized compilation.
For platform-specific deployment:
*   **Desktop:** Standard `cargo build` and `cargo run` commands.
*   **WebAssembly (WASM):** Examples show usage with `wasm-bindgen` and a basic `index.html`.
*   **Mobile (Android/iOS):** Dedicated `examples/mobile` directory includes `Makefile`s and platform-specific project structures (`android_example/`) for building and deployment to target devices.
Continuous deployment is managed via GitHub Actions workflows (`.github/workflows/`), handling compilation, testing, and release processes for various targets.

## ⚡ Quick Start Guide
To get started with Bevy, you'll need the Rust toolchain installed.

1.  **Install Rust:** If you don't have Rust, install it using `rustup`:
    ```bash
    curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh
    ```
    Follow the on-screen instructions.
2.  **Clone the Bevy Repository:**
    ```bash
    git clone https://github.com/grewal16/bevy.git
    cd bevy
    ```
3.  **Run an Example:** Bevy's examples are a great way to learn. Try running a basic 3D scene:
    ```bash
    cargo run --release --example 3d_scene
    ```
    Or a 2D sprite example:
    ```bash
    cargo run --release --example sprite
    ```
    For specific platform instructions (WASM, Android, iOS), refer to the `examples/` directory and related documentation within the repository.

## 📜 License
This project is **Dual-licensed** under either:
*   [Apache License, Version 2.0 (LICENSE-APACHE)](./LICENSE-APACHE)
*   [MIT license (LICENSE-MIT)](./LICENSE-MIT)

at your option.

This means you can choose whichever license you prefer for your project when using Bevy.