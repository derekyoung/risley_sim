# Dual Prism Risley Scanner Visualizer

Interactive browser demo of a **dual Risley prism** steering a laser beam, plus a simple **coastal LiDAR-style strip** so you can see how the scan pattern lands on terrain from the side and from above.

The whole app is one file: [`risley_sim.html`](risley_sim.html). No build step or dependencies.

## Quick start

1. Clone or download this repository.
2. Open `risley_sim.html` in a modern desktop or mobile browser (double-click the file, or drag it into a browser tab).

For the most predictable behavior (especially if anything loads oddly from `file://`), serve the folder locally, for example:

```bash
python3 -m http.server 8080
```

Then visit `http://localhost:8080/risley_sim.html`.

## What you’re looking at

### Panel 1 — Risley scanner

Canvas animation of two wedge prisms (**P1** blue, **P2** red) rotating about the beam axis. The outgoing beam direction traces a pattern on the **scan plane** depending on wedge angles, rotation speeds, directions, and optional **galvo** motion on P2.

Use **Clear trail** to wipe the accumulated trace on the scan plane; **Pause / Play** stops or resumes time evolution.

### Panel 2 — Coastal terrain (side + nadir)

Two linked views of the same simplified shore strip:

- **Side profile** — distance offshore vs elevation (cross-shore × height).
- **Nadir plan** — cross-shore vs along-shore footprint.

They share geometry and sensor placement; on wide windows they appear side by side, on narrow screens they stack. The strip is a simple coast model: ocean on one side, a sloped beach, and a flat backbeach on the other (labeled on the drawings).

## Controls (overview)

**Playback**

| Control | Purpose |
|--------|---------|
| Pause / Play | Freeze or run the simulation clock |
| Clear trail | Reset the drawn scan trace |

**Presets**

| Preset | Role |
|--------|------|
| Original ratio scan | Default: P2 spins faster than P1 (ratio 1.7), galvo off |
| Fixed P2 circle reference | P2 held steady via galvo while P1 rotates—useful circular reference |
| Counter-rotate 1:1 | Equal-speed counter-rotating prisms (classic Risley pair) |
| Clover 2:1 | P2 at half of P1’s rate, same rotation direction—cloverleaf-style trace |
| Custom | Whatever you set manually after touching sliders |

**Prism / beam**

- **Base RPM** — overall rotation rate scaling.
- **P1 speed**, **P2 speed**, **Ratio** — relative rotation rates (ratio ties P2 to P1).
- **P1 dir**, **P2 dir** — clockwise vs counter-clockwise per prism.
- **P1 α₁**, **P2 α₂** — wedge (deviation) angles; **Lock** keeps α₁ and α₂ equal.

**Optional P2 galvo**

When enabled, P2 can follow a sinusoidal **galvo** motion instead of steady rotation. Tune **Amplitude**, **Galvo freq**, **Phase**, and **Center** to shape that motion.

**Terrain / sensor**

- **Sensor height** — altitude of the sensor above the reference surface (meters).
- **Look angle** — downward tilt (degrees).
- **Scene width** — cross-shore extent of the modeled strip (meters).
- **Backbeach width / height** — flat upland platform geometry.
- **Slope width** — width of the sloped beach segment.

Sliders and numeric fields stay in sync; you can type exact values where supported.

## Limitations

This is a **visualization and intuition tool**, not a calibrated optical or survey instrument. Prism optics, atmosphere, waveforms, and real instrument geometry are simplified or omitted.

## Contributing / hosting

To publish on GitHub Pages, place `risley_sim.html` at the site root (or link to it from an `index.html`) so visitors load it over `https://`.

Suggestions and fixes are welcome via issues or pull requests.
