# 3D Wormhole Generator

Real-time WebGL wormhole visualization in a single HTML file using Three.js r166 ES modules.

Live interface: https://codepen.io/pierremaw/pen/vENqzER

## Highlights

- Single-file app (`Index.html`) with no build tooling
- Custom shader core + distortion shell
- Bloom + FXAA post-processing pipeline
- Portal energy/cooldown system with HUD
- Portfolio-aligned UI skin (rose/blue/green palette, glass panels, pill badges)

## UI and Theme

The interface now mirrors the portfolio wormhole styling:

- Dark Catppuccin-inspired surface colors (`--ctp-*` variables)
- Top-center status badges (`Interactive Preview`, `Theme Synced`)
- Updated control panel and indicator styling
- Energy bar gradient aligned to portfolio accent colors
- Mobile layout adjustment that docks controls near the bottom

Default scene colors were also shifted to the portfolio palette:

- Primary: `#e05aa0`
- Secondary: `#34d399`
- Accent: `#4a90d9`
- Vortex: `#5ea0e5`

## Architecture

### Scene Graph

The scene is rebuilt from these systems:

- `CosmicBackground` (4200 points)
- `PortalCore` (custom shader sphere)
- `VortexRings[n]` (`n = 3 + portalComplexity`)
- `Crystals[m]` (`m = crystalCount`)
- `DimensionalStreams[k]` (`k = 4 + portalComplexity`)
- `PortalFrame`
- `EnergyParticles` (1500 points)
- `SpaceDistortion` (custom shader sphere)

### Render Pipeline

`Scene -> RenderPass -> UnrealBloomPass -> FXAA -> Output`

Key renderer settings:

- `antialias: true`
- `preserveDrawingBuffer: true` (for screenshot export)
- `ACESFilmicToneMapping` with exposure `1.18`
- `SRGBColorSpace`

Bloom defaults:

- Strength: `1.2`
- Radius: `0.7`
- Threshold: `0.2`

## Shader and Portal System

Portal activation injects a pulse through `onBeforeCompile` materials.

- Pulse speed: `8.0`
- Pulse width: `1.5`
- Core burst window: `1.0s`

Energy model:

- Regen: `8/sec`
- Activation cost: `25`
- Cooldown: `900ms`

## Controls

### Mouse and Keyboard

- Drag: orbit camera
- Scroll: zoom
- Double-click: fullscreen
- `Space`: activate portal pulse
- `R`: reset camera
- `X`: randomize palette / dimension shift
- `P`: toggle low-power mode
- `F`: fullscreen toggle

### GUI (top-right)

- Complexity (`1-8`)
- Crystals (`6-24`)
- Wormhole Energy Hue
- Bloom On
- Bloom Strength
- Spin

### Other

- Screenshot button exports PNG
- Reduced motion disables auto-rotate and clamps bloom strength to `0.6`

## Run

```bash
python -m http.server 8000
```

Then open `http://localhost:8000`.

## Browser Support

WebGL2 + ES modules capable browsers (modern Chrome, Firefox, Safari, Edge).

## License

MIT
