# EMRI Orbits

Interactive 3D visualization of Extreme Mass Ratio Inspirals (EMRIs) — a stellar-mass
compact object spiraling into a massive Kerr black hole — together with the
source-frame gravitational-wave strain it emits.

The orbital evolution and waveform are computed live in the browser using the
**Analytic Kludge** (AK) of

> Barack & Cutler, "LISA capture sources: Approximate waveforms, signal-to-noise
> ratios, and parameter estimation accuracy", *Phys. Rev. D* **69**, 082005 (2004).
> [arXiv:gr-qc/0310125](https://arxiv.org/pdf/gr-qc/0310125)

## Run it

It's a single HTML file — no build, no server.

```sh
open index.html        # macOS
xdg-open index.html    # Linux
```

Or drop it on any static host (GitHub Pages, S3, etc.).

## What it does

- Integrates the AK orbital ODEs for `(Φ, ν, e, γ̃, α)` with RK4
  (Eqs. 27–31 of the paper).
- Computes source-frame `h₊` and `h_×` from the Peters–Mathews quadrupole
  harmonic sum (Eqs. 7–10), with a numerically stable Bessel `J_n` via
  Miller's downward recurrence and a bucketed harmonic count
  (6 → 60, depending on eccentricity).
- Renders the orbit in 3D with Three.js: Kerr horizon, equatorial ISCO ring,
  spin axis Ŝ, orbital angular momentum L̂ (precessing around Ŝ).
- Shows the modern Kerr-EMRI parameters: `p/M`, `e`, `cos ι`, and the three
  fundamental frequencies `f_r`, `f_θ`, `f_φ`.

## Controls

- **Presets**: Generic Kerr, Spherical Kerr (inclined circular), High-e generic,
  Near plunge.
- **System**: MBH mass, CO mass.
- **Initial orbit**: spin `a/M`, semi-latus rectum `p₀/M`, eccentricity `e₀`,
  inclination `ι`.
- **Animation**: time speedup (×10 to ×100,000), play/pause, reset, freeze
  inspiral (hold orbital elements; orbit keeps cycling — useful at high e where
  the system would otherwise plunge in seconds of viz time).
- **View**: snap to side / top-along-Ŝ / plane-of-sky; toggles for trail, L̂,
  Ŝ, ISCO ring.

## Caveats

- Source-frame strain only — no LISA detector response (Eqs. 11–17 not included).
- ISCO ring uses the closed-form Kerr equatorial-prograde formula; for inclined
  or eccentric orbits the true LSO differs slightly.
- Pericenter angle in the waveform uses `γ ≈ γ̃` (skips the observer-dependent
  `β` term in Eq. 21); visually negligible.
- Near plunge the AK breaks down; the animation auto-freezes the slow elements
  rather than letting the integrator blow up.

## Author

Daniel Oliver. Built with assistance from Claude Code.
