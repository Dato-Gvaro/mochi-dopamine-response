# ol_break_earth2 (DopamineEXE, v2 of ol_break_earth)
- New scene file; `scenes/ol_break_earth.py` (v1) untouched. Same ladder, numbers, sources, meter logic, frame-0 hook, Holst clock, music and SFX design as v1 (see `docs/scenes/ol_break_earth.md`). v2 is the visual jump.
- Owner verdict on v1 (2026-11-15): "If we do a thing like this, it must have MANY particles and very nice visuals."
- Caption: post-pass overlay as v1 (`--capimg` PNG + one ffmpeg overlay, audio copied). Base `--cap ''`.
- Delivered: `<VIDEOS_DIR>\DopamineExe\review\ol_break_earth2.mp4` (FHD, seed 1, label fhd + caption).

## What changed vs v1
- **Big Earth**: R 375 px at (508, 760) = 750 px wide, 94 % of the 0.10-0.84 w band (v1: R 300). Light from the upper left, so a night side shows on the right.
- **Texture**: NASA Blue Marble ("Whole world - land and oceans", Wikimedia Commons thumb 3840x1920) + DMSP city lights 1994-95 (NASA, 3840x1920), both public domain, in `assets/ol_break_earth2/nasa/`. eoimages.gsfc.nasa.gov was unreachable; Commons hosts the same files.
  - The flat navy Blue Marble ocean (11,10,50) is masked and recoloured: deep → mid → shallow blue by distance to the coast + fbm.
  - Clouds are procedural: domain-warped fbm, latitude-banded.
  - Night side: city lights × (1 - day)², killed under fire/magma.
  - Ocean glint, limb Fresnel blue, and an atmosphere halo ring computed in the same numpy raster (lit-side weighted).
  - Twilight band × Z² (without it, a red arc hugs the night limb).
  - Cache `output/_cache_ol_break_earth2_tex_v2.npz`.
- **HUD**: the log meter is HORIZONTAL at y 1210 (x 150-866), with "EARTH BREAKS · 530 MILLION" above its red tick. A vertical meter would cost the Earth ~100 px of width. Stamp y 1296; chip, counter and DINO-KILLERS at v1 positions.
- **Camera**: R 375 for rungs 1-6, then 200 for Theia's approach, 125 for the disc and Moon, and 190 for the twin. The twin zoom pans so the contact point (centre of mass) lands at frame centre on the hit. Finale zoom-out 1 → 0.70 over 3.2 s.
- **Sites**: real sites for 1-3. Per-rung `off` (deg left of the view centre) puts each site toward the upper-left limb, so curtains show against space. The 500 km rock moved to the Pacific (-150, 12) so "oceans boil" happens over ocean. No flags or national markers.

## Particles (all numpy; logical counts, same at every scale)
| rung | particle event | count |
|---|---|---|
| 1 Chelyabinsk | fireball trail + airburst spray | 500 + 800 |
| 2 Tunguska | trail + airburst + surface shock ring/scar | 700 + 1,200 |
| 3 Chicxulub | ballistic ejecta curtain (1/r² gravity) + flames on an irregular fire ring | 6,000 + 2,500 |
| 4 100 km | ejecta + global firestorm flames | 9,000 + 5,000 |
| 5 500 km | ejecta + steam off ocean pixels only | 9,000 + 7,000 |
| 6 Ceres | 1,800 crust PLATES (cairo quads, Earth-textured face / glowing back, tumbling, ballistic) + 7,200 hot debris + 4,000 ejecta over cracked magma | 13,000 |
| 7 Theia | debris disc (v1 logic, vectorised) → Moon | 16,000 |
| 8 twin | ~840 Voronoi chunks of both rasters (~227k textured px at FHD), molten core 45,000 (white-hot core remnant, white-hot jet sheet along the contact plane, mantle cloud), jet sparks 6,000 | ~51k particles + 840 chunks |

- Peak ~101k splatted items/frame (finale, incl. crumbled grains).
- **Ejecta**: world coords, integrated in `simulate()` (4 substeps/frame, G0 3.4 R/s², time-lapse). Landing = clamp to the surface + 0.16 s glow. Views rotate with `lam_at` (camera orbit), occluded behind the disc.
- **Twin chunks**: rigid per-chunk rotation, plus a flip about a random in-plane axis (|cos| squash = 3-D tumble). The face shows the unlit Earth albedo × a tumble light factor. The back shows a molten core: bright at the chunk centre, dark red at the rim. Rims glow orange as the crack front (5.5 R/s) passes. 26 % of chunks (nearest the contact) crumble to grains.
- **Expansion**: `expand_vel`. Head-on means axial momentum cancels: v = 0.50·along + 1.35·side (self-similar), plus sideways jets from the contact zone; braked by `s_exp` (v1).
  - Inner-fastest velocities (v1's law) leave a black hole in the middle. Don't.

## Rendering
- `Layer`: bilinear splat via one bincount per channel (4 taps concatenated), 3-tap motion blur for movers > 1.2 device px/frame, 5-sample footprint for size > 1.3.
- EMISSIVE layers go additive with tone map 1-exp(-E) and a two-scale bloom from the particles themselves (1/4 res σ 1.6, 1/8 res σ 4.5), so the glow hugs the geometry. SOLID layers are alpha-composited with averaged colour.
- **Finale order**: molten + its bloom UNDER the chunks → chunks → rims/sparks/grains + bloom. Blooming the molten layer over the chunks washed them to grey-white.
- Small bodies (Theia, Moon) use the same numpy sphere raster with procedural textures. Theia is clipped outside the Earth as it sinks in.
- **Time**: -Fast ~0.33 s/frame (5.8 min clip); FHD see Checks.

## Checks (encoded FHD, captioned)
- h264 High yuv420p 1080x1920 @60, 1,055 frames, 17.58 s.
- -14.00 LUFS, peak -5.69 dBFS, last 0.5 s at -240 dBFS. RMS per 5 s: -19.5 / -15.6 / -15.1 / -14.7.
- flash_check PASS (0 flashes, mean lum 0.022).
- Seam: pre-encode SEAM EXACT (check_loop, max 0/255); post-encode mean 0.737. That is just above the 0.72 band edge: H.264 noise on the detailed Earth texture, not state.
- SFX events per 5 s: 82 / 261 / 364 (climbing), 707 events in total.
- Peak splats per frame: ~101k at -Fast, ~233k at FHD (chunk pixels scale with resolution).
- Contact sheet + 1:1 crops (3.95, 5.75, 8.85, 10.35, 12.85, 14.0, 16.0 s) in the review folder.

## Doubts
- 500 km "OCEANS BOIL" turns the Earth hazy white for ~0.6 s: honest (steam), but it reads more "snowball" than "boiling".
- Ceres: the crack network + plate shell is busy at 9.0 s, just before Theia's zoom.
- Moon phase: `moon_phi0` is set so the Moon is in front and right of the Earth at T6 + 1.9 s. The first phase had it behind the Earth while "…it made the MOON" was on screen.
- Finale late frames: chunk undersides read as orange glints. They are molten cores, but at phone size they may read as confetti.

## Flags
`--seed (1) --label --cap --capimg --still --frame a,b --dry --audio --sound 0 --sfx (0.55) --hold (1.35)`.
