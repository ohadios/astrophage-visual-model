# Astrophage — Solar Infection Model

An interactive, single-file web visualization of how **Astrophage** — the star-eating microbe from Andy Weir's *Project Hail Mary* — infects the Sun, forms the Petrova line, and dims the star toward a planetary ice age. It also lets you introduce **Taumoeba**, the predator that keeps the infection in check, and watch the Sun recover.

> ⚠️ **Spoiler / disclaimer:** This is an unofficial fan project based on *Project Hail Mary* by Andy Weir. It is **not** affiliated with or endorsed by the author or publisher, it contains plot spoilers, and it is an *illustrative* model — faithful to the book's framing, but not a rigorous astrophysical simulation. See **The Model: Facts vs. Assumptions** below.

---

## Live demo

Hosted on Github Page: `https://ohadios.github.io/astrophage-visual-model/`


---

## What it shows

A tilted, pseudo-3D view of the inner solar system with the full Astrophage lifecycle running as an agent-based particle system:

- The **Sun** rotating on a ~25-day period, with **Venus** (0.72 AU) and **Earth** (1 AU) on their orbits.
- Astrophage **charging** on the Sun, **departing straight out from the solar pole**, then turning sharply toward Venus — tracing the glowing infrared **Petrova line**.
- Astrophage **breeding** in a spherical cloud around Venus, then returning to the Sun.
- The Sun **dimming** as the colony grows: escaping light rays are attenuated in crowded directions, the photosphere develops dark mottling, and the headline "Solar Output" falls toward the canonical ~10% ceiling.
- **Taumoeba** (optional) blooming inside Venus's CO₂ atmosphere and crashing the Astrophage population.

---

## Features

- **Faithful lifecycle** — charge (~8 d) → polar departure → Petrova transit → breed at Venus → return.
- **Book-calibrated dimming** — caps at ~10% (canon) and reaches it ~30 years after first detection.
- **Telemetry panel** — Days Since Detection, Astrophage Population, Generation, Solar Output, Saturation, and Taumoeba bloom, each with a hover tooltip explaining it.
- **Toggleable time-series graph** — traces Astrophage saturation, Solar output, and Taumoeba over time.
- **Taumoeba predator** — introduce/remove a Lotka–Volterra predator confined to Venus's atmosphere.
- **Zoom & pan** — scroll/pinch to zoom, drag to pan, double-click to reset.
- **Adjustable controls** — starting population (defaults to the first-detection baseline) and time rate (0.25 d/s up to 5 yr/s).
- **Model Notes modal** — a transparent breakdown of what's canon vs. what we assumed.
- **Embedded feedback form** — collects corrections and suggestions to tighten the model.
- **Zero dependencies / no build** — one self-contained HTML file; only external resource is Google Fonts over CDN.

---

## The lifecycle (the science)

In *Project Hail Mary*, Astrophage runs a closed migration loop driven by two needs — stellar energy and CO₂ to reproduce:

1. **Charge at the Sun.** A cell absorbs stellar energy and stores it as mass near the E=mc² limit. It holds a constant internal temperature of 96.415 °C and can bank ~1.5 MJ before it is "enriched."
2. **Depart the pole.** Once enriched, it launches straight away from the solar pole (it only responds to the Sun's magnetic field at the very start of the trip), then turns sharply toward Venus.
3. **The Petrova line.** That curved path glows in infrared at 25.984 µm — the line first spotted by Dr. Irina Petrova, and the signature that revealed the crisis.
4. **Breed at Venus.** In Venus's CO₂-rich upper atmosphere it divides; parent *and* child both fly back to the Sun.
5. **Dim the star.** A growing shroud of cells absorbs sunlight before it escapes — an "umbrella" effect (the Sun's fusion is untouched). It stops at ~10% dimming for reasons the book leaves unexplained, which is enough to trigger a terminal ice age.

**Taumoeba** is the predator from the planet Adrian that preys on Astrophage. It requires CO₂, so it lives in the target planet's atmosphere and cannot follow Astrophage to the Sun — making Venus the natural place to deploy it.

---

## The model: facts vs. assumptions

The in-app **Notes** modal carries the authoritative, detailed version. In brief:

### Treated as canon (from the book)
- ~10 µm single-celled organism; constant 96.415 °C; stores energy as mass (E=mc²); ~1.5 MJ per enriched cell.
- Lifecycle: charge → depart the solar pole → CO₂-lock on Venus → breed → return (the Petrova line).
- Propulsion / Petrova-line emission at **25.984 µm**; CO₂ detection bands at **4.26 µm and 18.31 µm** (these are *not* the propulsion wavelength).
- Dimming caps at **~10%**, unexplained; ~30 years to ice age.
- Tau Ceti resisted because Adrian hosts **Taumoeba**, which needs CO₂ and dies at Venus's nitrogen levels (hence the bred "Taumoeba-82.5").

### My assumptions (to make it run)
- **8-day charge time** — a working figure, not pinned down in the book.
- **Growth rate** (the big one): canon implies each ~15-day cycle *doubles* the population, which would shroud the Sun in months — yet canon also says ~30 years to 10%. We reconcile this internal tension by imposing a slow logistic curve (~1.4% net per cycle, ~2.1-year doubling) so the colony climbs from ~0.01% dimming at detection to 10% in ~30 years. A real limiter (self-shading, CO₂-limited breeding, migration mortality) would make it emergent.
- **Detection start:** the clock begins at first detection (~0.01% dimming ≈ ~30 trillion cells ≈ 0.1% of peak).
- **Head-count** (~3×10¹⁶ peak) is illustrative; the true number is vastly larger.
- Circular/coplanar orbits, uniform 25-day Sun rotation, slowed near-light-speed transits, tuned Taumoeba predator-prey constants, and on-screen particles as a representative visual sample.

---

## Controls reference

| Control | What it does |
| --- | --- |
| **Starting Astrophage Population** | Sets the initial colony size. Defaults to the first-detection baseline (~30 T / ~0.01% dimming). |
| **Time Rate** | Simulation speed, 0.25 d/s up to 5 yr/s. Low = watch one cell's journey; high = span the decades. |
| **❚❚ Pause / ▶ Play** | Pause or resume. |
| **↻ Reset** | Restart from the current slider settings. |
| **Light Rays / Petrova Glow / Field Lines** | Toggle visual layers. |
| **⊕ Introduce Taumoeba** | Seed the predator into Venus's atmosphere (toggle off to remove). |
| **⤢ Reset View** | Reset zoom/pan. |
| **▤ Graph** | Show/hide the time-series traces. |
| **ⓘ Notes** | Facts & assumptions. |
| **✉ Feedback** | Open the feedback form. |
| Mouse/touch | Scroll or pinch to zoom, drag to pan, double-click to reset view. |

---

## Running locally

No build step, no server required. Just open the file:

```
open index.html        # macOS
# or double-click index.html in your file browser
```

An internet connection is recommended so the Google Fonts load; without it the layout still works with fallback fonts.

---

## Tech notes

- **Stack:** vanilla JavaScript + HTML5 Canvas 2D. No frameworks, no bundler.
- **Fonts:** Chakra Petch (display) and IBM Plex Mono (telemetry), loaded from Google Fonts.
- **Rendering:** orthographic projection of 3D (AU) coordinates with a fixed view tilt; depth-sorted particle/planet rendering; additive glow compositing.
- **Population model:** an analytic logistic curve drives the population, dimming, and shading; the on-screen particle swarm is a capped visual sample decoupled from the true count. Taumoeba adds a coupled predator-prey term, integrated with sub-stepping for stability at high time rates.
- **No browser storage** is used.

---

## Feedback

The app embeds a feedback form behind the **✉ Feedback** button so visitors can flag bad facts or suggest better-justified assumptions. To point it at a different form, replace the form URL in the `#fbFrame` iframe (and the "open in a new tab" link) inside `index.html`.

---

## Credits & attribution

- Concept and all *Project Hail Mary* lore © **Andy Weir**. This project is an unofficial, non-commercial fan tribute and is not affiliated with or endorsed by the author or publisher.
- Built collaboratively as an exploration of the Astrophage lifecycle and population dynamics.

## License

No license is set yet. If you intend to share or accept contributions, add one (e.g. MIT for the code) and keep the attribution/disclaimer above. Note that the underlying *Project Hail Mary* concepts remain the intellectual property of their rights holders.
