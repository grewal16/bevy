# 🚀 Bevy Engine

<p align="center"><img src="./assets/branding/banner.png" alt="Bevy Engine Banner" width="700"></p>

## Short Description
Bevy is a refreshingly simple and powerful data-driven game engine built in Rust. Designed for performance, modularity, and rapid iteration, it offers a complete suite of tools for crafting 2D and 3D games and interactive applications. Leveraging a modern Entity Component System (ECS) architecture, Bevy empowers developers to build ambitious projects with clean, idiomatic Rust code.

## ✨ Key Features
*   **Data-Driven ECS:** A high-performance, parallelizable, and flexible Entity Component System at its core.
*   **2D & 3D Rendering:** Robust rendering capabilities including Physically Based Rendering (PBR), sprite rendering, post-processing effects (Bloom, SSAO, SSR, Motion Blur, Volumetric Fog), and sophisticated lighting.
*   **Asset Management:** Integrated asset loading for diverse formats (images, fonts, sounds, GLTF models), with hot-reloading for rapid development.
*   **Animation System:** Comprehensive animation support, including keyframe animations, animation graphs, and skinned meshes for dynamic character movement.
*   **Flexible UI System:** Powerful UI framework with declarative syntax, custom widgets, gradients, and advanced layout capabilities, supporting interactive elements and accessibility.
*   **Cross-Platform Support:** Seamlessly deploy to desktop (Windows, macOS, Linux), WebAssembly, Android, and iOS (via examples).
*   **Input Handling:** Extensive input management for keyboard, mouse, touch, and gamepads, including advanced features like gamepad rumble.
*   **Debugging & Diagnostics:** Built-in development tools like FPS overlays, frame time graphs, and configurable gizmos for visual debugging.
*   **Modular Architecture:** The engine is split into small, reusable crates, allowing developers to pick and choose components, fostering a lean and efficient development process.
*   **Developer Experience:** Focus on ergonomics, compile-time checks, and clear error messages, powered by Rust's strong type system.

## Who is this for?
Bevy is ideal for:
*   Game developers seeking a modern, high-performance, and open-source engine.
*   Rustaceans eager to build games and interactive experiences with their favorite language.
*   Developers who value modularity, explicit control, and a data-driven approach.
*   Teams looking for an engine that scales from small indie projects to complex applications, with strong community support.

## Technology Stack & Architecture
Bevy is built entirely in **Rust**, a language renowned for its performance, memory safety, and concurrency. The engine embraces a highly modular **ECS (Entity Component System)** pattern, where entities are mere IDs, components store data, and systems define behavior. This architecture promotes parallel processing and clear separation of concerns.

Key technological highlights include:
*   **WGPU:** Powers high-performance, cross-platform graphics rendering.
*   **WGSL/GLSL:** Shader languages for custom rendering effects.
*   **Bevy ECS:** A custom, highly optimized ECS implementation.
*   **Modular Crates:** The engine is composed of numerous crates (e.g., `bevy_render`, `bevy_ui`, `bevy_animation`, `bevy_asset`), each handling specific functionality, leading to a lean codebase where only necessary features are compiled.

## 📊 Architecture & Database Schema
```mermaid
graph TD
    A[Bevy App] --> B(Plugin Group)
    B --> C(Core Plugins)
    C --> D[Bevy ECS]

    D -- Manages Data --> E[Components]
    D -- Executes Logic --> F[Systems]
    D -- Organizes Data --> G[Resources]
    D -- Tracks Changes --> H[Events]

    C -- Renders --> R(Bevy Render)
    R --> R1(2D Rendering)
    R --> R2(3D Rendering)
    R -- Post-Processing --> R3(Bloom, SSAO, SSR, etc.)
    R -- Shaders --> R4(WGSL)

    C -- Handles Input --> I(Bevy Input)
    I --> I1(Keyboard, Mouse, Touch)
    I --> I2(Gamepad)

    C -- Builds UIs --> U(Bevy UI)
    U --> U1(Widgets & Layout)
    U --> R

    C -- Manages Assets --> AS(Bevy Asset)
    AS --> AS1(Image/Font Loaders)
    AS --> AS2(GLTF Loader)
    AS --> C

    C -- Animate --> AN(Bevy Animation)
    AN --> AN1(Skins & Graphs)
    AN --> R

    C -- Timing --> T(Bevy Time)
    C -- Utilities --> UT(Bevy Utils)
    C -- Platform Abstraction --> P(Bevy Winit/Android)

    R -- Depends on --> D
    I -- Generates Events --> H
    U -- Creates/Modifies --> D
    AS -- Loads Data For --> D, R, AN, U
    AN -- Modifies --> D
```

## ⚡ Quick Start Guide
To get started with Bevy, ensure you have a Rust toolchain installed.

1.  **Clone the Repository:**
    ```bash
    git clone https://github.com/grewal16/bevy.git
    cd bevy
    ```
2.  **Run an Example:**
    Explore the examples to see Bevy in action. For a simple "Hello World" application:
    ```bash
    cargo run --example hello_world
    ```
    For a comprehensive UI showcase:
    ```bash
    cargo run --example ui --features bevy_winit/x11
    # Or, to run a 3D example:
    cargo run --example 3d_scene
    ```
    *(Note: Some examples might require specific platform features or Rust toolchain components. Refer to individual example files for details.)*

## 📜 License
Bevy is dual-licensed under both the Apache 2.0 License and the MIT License. You may choose either license to govern your use of this software.

For details, see:
*   [LICENSE-APACHE](./LICENSE-APACHE)
*   [LICENSE-MIT](./LICENSE-MIT)
