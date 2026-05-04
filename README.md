# 💎 Neon Voronoi

*Dynamic Voronoi diagram: the plane is tessellated into colored cells, each belonging to the nearest seed point. Seeds drift slowly, causing the cellular boundaries to shift and morph in real time. Click to add new seeds. Adjust seed count, movement speed, color cycling. Hypnotic geometric glow.*

---

## What is this?

A Voronoi diagram partitions space into regions based on the closest point in a set of "seeds" or "sites". It appears in nature (cells, cracks, biology), GIS, and procedural generation. This live visualization shows the diagram evolving as the seeds move. Each region is filled with a neon color derived from its seed's hue, creating a constantly shifting mosaic of glowing cells.

---

## Features

- **Real-time Voronoi** computation on a low-resolution grid (pixelated aesthetic)
- **Drifting seeds** with bounce-off-walls physics
- **Neon glow** via HSL color cycling, with a precomputed RGB palette for performance
- **Interactive** — click anywhere to inject a new seed; the diagram re-tessellates around it
- **Adjustable parameters:**
  - Seed Count (2–50) — more seeds = smaller cells, more complex boundaries, heavier CPU
  - Move Speed (0–2) — how fast seeds drift; 0 = static diagram
  - Color Cycle Speed (0–2) — global hue rotation speed
- **Pause/Resume** to freeze seed motion
- **Clear** — remove all seeds (canvas goes dark)
- **Randomize** — random seed count, speed, color speed, and re-randomize seed positions/hues
- **Stats overlay** — seed count, FPS
- **Single HTML file** — no dependencies

---

## How to Use

1. Open `index.html`
2. The canvas fills with colored cells, each centered on a moving seed. Watch the boundaries undulate as seeds drift.
3. **Click** to add a new seed at the cursor. The diagram instantly re-computes nearest neighbors.
4. Use sliders:
   - **Seed Count** — more seeds = finer mosaic, but more CPU (distance checks)
   - **Move Speed** — controls drift velocity of seeds; try 0 for a static pattern you can rotate colors on
   - **Color Cycle** — rotates hue of all seeds over time, creating rainbow shifts
5. **Pause** to freeze seeds (colors may still cycle if that slider > 0)
6. **Clear** to remove all seeds (blank canvas); **Randomize** to generate a fresh random configuration

---

## Technical Details

- **Grid:** The Voronoi is computed on a coarse grid (`SCALE = 10` screen pixels per cell) to keep CPU cost manageable. For each cell, we compute the squared Euclidean distance to every seed and pick the nearest. Complexity: O(cols × rows × seedCount). With ~200×120 grid and 20 seeds, that's ~480k distance checks per frame, which runs at interactive rates on modern hardware.
- **Rendering:** Results are written into an `ImageData` buffer (RGBA) for the small grid canvas. That canvas is then upscaled with `drawImage` to fullscreen, yielding a crisp pixelated look without extra fillRect calls.
- **Color:** A precomputed 360-entry RGB palette for full-saturation, medium-lightness HSL colors gives fast hue lookup. Final cell hue = (seed.baseHue + global hueCycle) mod 360.
- **Seeds:** Point masses with velocity vectors; bounce off canvas edges.
- **Performance tips:** Lower seed count or increase `SCALE` (by editing code) for better FPS on slow machines.

---

## The Real Story

Voronoi diagrams are everywhere: in giraffe spots, honeycomb, cracked mud, city service areas, and procedural terrain. Watching them morph in real time as points drift is like seeing a living mosaic. The neon palette gives it a retro-futuristic vibe. It's simple yet mesmerizing — the kind of thing you can stare at while your brain relaxes. Try setting move speed to 0 and just cycle colors; the static geometry with shifting hues is pure visual meditation.

---

*Made with 💎 and nearest-neighbor searches.*

**Repo:** https://github.com/Kiloooai/neon-voronoi
