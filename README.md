# 3D Wormhole Generator

Interactive Site: https://codepen.io/pierremaw/pen/vENqzER

A real-time, GPU-driven portal visualisation built with three.js. Activate a shimmering wormhole, explore vortex rings and dimensional streams, and capture high-resolution screenshots. Designed for simplicity, performance, and a bit of sci-fi delight. Vibe coded with GPT-5.

https://github.com/user-attachments/assets/71653f8e-079e-4665-98b0-82a011966d45

---

## Features

* GPU shaders for the portal core, space distortion and emissive pulse effects
* Post-processing with bloom and FXAA
* Orbit camera with damped motion and autorotate
* Procedural stars, crystals, energy particles and dimensional tube streams
* Interactive control panel with ripple feedback and keyboard shortcuts
* One-click screenshot capture (`.png`)

---

## Live Controls

> Mouse: navigate. Double-click: fullscreen.
> Keys: `Space` activate • `R` reset • `X` change • `P` perf

Toolbar buttons and shortcuts:

* Activate Wormhole: button or `Space`
* Reset Camera: button or `R`
* Change Dimensions (randomise colours and layout): button or `X`
* Toggle Performance Mode: button or `P`
* Save Screenshot: camera button
* Fullscreen: double-click anywhere or press `F`

An on-screen indicator shows wormhole stability and energy.

---

## Configuration

Most parameters are adjustable at runtime via the GUI (press the lil-gui toggle if hidden).

| Parameter           | Description                          |   Range |   Default |
| ------------------- | ------------------------------------ | ------: | --------: |
| Complexity          | Number of vortex rings and streams   |  1 to 8 |         4 |
| Crystals            | Floating crystal count               | 6 to 24 |        12 |
| Wormhole Energy Hue | Accent colour used by portal shaders |  colour | `#e74c3c` |
| Bloom On            | Toggle Unreal Bloom pass             | boolean |      true |
| Bloom Strength      | Bloom intensity                      |  0 to 3 |       1.2 |
| Spin                | Global rotation speed                |  0 to 1 |       0.3 |

---





