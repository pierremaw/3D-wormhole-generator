# 3D Wormhole Generator

Real-time WebGL wormhole visualisation. Single HTML file, Three.js r166, ES modules.

Live interface: https://codepen.io/pierremaw/pen/vENqzER

https://github.com/user-attachments/assets/ab906f2f-e4c7-49d8-9d27-bd74ff89e2a1

## Architecture

### Scene Graph

Eight objects under the root Scene compose the wormhole, all rendered each frame.

    Scene
    ├── CosmicBackground      4,200 points, r ∈ [80, 130]
    ├── PortalCore            Sphere, custom shader (fresnel + temporal noise)
    ├── VortexRings[n]        Torus, n = 3 + complexity
    ├── Crystals[m]           Octahedron, m = crystalCount, radial placement
    ├── DimensionalStreams    CatmullRomCurve3 → TubeGeometry, 12π helix
    ├── PortalFrame           Torus r=7
    ├── EnergyParticles       1,500 points, additive blend
    └── SpaceDistortion       Inverted sphere, fresnel transparency

### Render Pipeline

Three post-processing passes run after the scene renders. Bloom creates the glow; FXAA smooths edges.

    Scene → RenderPass → UnrealBloomPass → FXAAShader → Output

| Pass | Parameters |
|------|------------|
| Bloom | strength 1.2, radius 0.7, threshold 0.2 |
| Tonemapping | ACES filmic, exposure 1.18 |
| Output | sRGB colour space |

### Shader

Portal activation injects a custom fragment via onBeforeCompile. The pulse expands outward at 8 units/sec.

    float r = timeSincePortal * 8.0;
    float pulse = smoothstep(r - 1.5, r, dist) - smoothstep(r, r + 1.5, dist);

Energy: 8/sec regen, 25 cost, 900ms cooldown.

## Controls

### Keyboard & Mouse

| Input | Action |
|-------|--------|
| Drag | Orbit camera |
| Scroll | Zoom |
| Double-click | Fullscreen |
| Space | Activate portal (25 energy, 900ms cooldown) |
| R | Reset camera to origin |
| X | Randomise colour palette |
| P | Toggle performance mode (disables bloom, pixel ratio 1) |
| F | Fullscreen |

### GUI Panel (top-right)

- Complexity: 1–8 (affects ring count)
- Crystals: 6–24
- Bloom: on/off, strength, radius
- Rotation speed

### Other

- Screenshot: button in control panel exports PNG
- Reduced motion: disables auto-rotate, caps bloom at 0.6

## Run

    python -m http.server 8000

ES modules require a server. The file protocol is blocked by CORS.

## Browser Support

WebGL 2 + ES modules: Chrome 89+, Firefox 89+, Safari 15+, Edge 89+

## License

MIT






