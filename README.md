# 3D Wormhole Generator

A real-time, GPU-driven wormhole you can *poke*, *spin*, and *photograph*. It renders a portal core with shader-driven pulses, wraps it in vortex rings and dimensional streams, then finishes the frame with bloom + FXAA for that clean sci-fi glow. Hit **Space** to “fire” the portal, scramble the universe with **X**, and save crisp **.png** screenshots straight from the renderer.

Live demo: https://codepen.io/pierremaw/pen/vENqzER

Preview video/GIF:
https://github.com/user-attachments/assets/0524dc40-ae06-436e-b641-7d1d40c2adc7

## What it does

The scene is built in **three.js** with a lightweight post-processing stack and a shader pipeline designed for speed. The portal effect is driven by uniforms like `time`, `pulseTime`, and `dimensionShift`, so “activation” feels like a travelling wave rather than a simple on/off toggle. Everything is procedural: starfield, crystals, particle energy, and the tube-like streams that imply motion through something bigger than space.

## Features

- **GPU shaders** for portal pulses, emissive surges, and space distortion
- **Post-processing**: Unreal Bloom + FXAA via `EffectComposer`
- **Orbit camera** with damping + autorotate (comfortable, gallery-style movement)
- **Procedural set dressing**: stars, crystals, energy particles, dimensional tube streams
- **Control panel UX** with ripple feedback, plus keyboard shortcuts
- **One-click PNG screenshots** using `preserveDrawingBuffer`

## Controls

Mouse navigates the orbit camera. Double-click toggles fullscreen.

Keyboard shortcuts:
- **Space**: activate the wormhole pulse
- **R**: reset camera
- **X**: change dimensions (randomise colours + rebuild layout)
- **P**: performance mode toggle
- **F**: fullscreen toggle

The **Wormhole Stability** indicator shows current energy and state (Stable → Fluctuating → Unstable → Collapsed) as energy drains and regenerates.

## Runtime tuning

Most settings are adjustable live via **lil-gui** (toggle it open if it’s hidden). These are the main knobs:

| Parameter            | Meaning                                   | Range   | Default   |
|---------------------|--------------------------------------------|--------:|----------:|
| Complexity          | Number of rings + streams                   | 1 to 8  | 4         |
| Crystals            | Floating crystal count                      | 6 to 24 | 12        |
| Wormhole Energy Hue | Accent colour used by portal pulse shaders  | colour  | `#e74c3c` |
| Bloom On            | Toggle Unreal Bloom pass                    | boolean | true      |
| Bloom Strength      | Bloom intensity                             | 0 to 3  | 1.2       |
| Spin                | Global rotation speed                       | 0 to 1  | 0.3       |

## Performance notes

Performance mode (**P**) reduces load by disabling bloom, lowering pixel ratio, and slowing autorotate. It’s the “keep it smooth” switch for integrated GPUs and laptops. The default renderer caps pixel ratio to `min(devicePixelRatio, 2)` to avoid accidentally melting the frame-time on high-DPI displays.

## Screenshots

Click the camera button (or wire your own hotkey) to save a `.png`. The renderer runs with `preserveDrawingBuffer: true` specifically so screenshots are clean and immediate.

## Tech stack

- three.js (WebGL renderer, materials, geometry, controls)
- EffectComposer + RenderPass + UnrealBloomPass + FXAAShader
- lil-gui for runtime parameters
- Vanilla HTML/CSS UI overlay (ripple buttons + energy indicator)
