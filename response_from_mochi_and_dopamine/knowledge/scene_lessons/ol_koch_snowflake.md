# ol_koch_snowflake (Dopamine.exe)
- New scene, character-free (docs/BRIEF_channel2.md). Skeleton: ×4 growth toward a named end state. The Koch snowflake: every edge grows a new triangle out of its middle third, so the edges go ×4 each generation. The inside shatters into ever-finer crystal facets in step, and the perimeter races toward ∞ while the area never passes 1.6×.
- Caption (baked, `--cap`; `--cap ''` = base): `Every edge grows a new ^TRIANGLE^|until the snowflake is ~INFINITE~` (`^x^` = current generation colour, `~x~` = gold).
- Delivered: `<VIDEOS_DIR>\DopamineExe\review\ol_koch_snowflake.mp4` (**v3**, Full HD, label fhd3, 13.95 s, 837 frames). No 4K yet.

## History
- **v1** (label fhd, 12.75 s): whole snowflake throughout. Coordinator: from ~5 s the generations are sub-pixel and it looks static.
- **v2** (label fhdz): Koch dive into a notch of the coastline (rotating view). v2's code is saved as `ol_koch_snowflake_v2.py` in the session scratchpad.
- **Owner review of v2 (2026-10-23):** "not engaged at the start; maybe you need to spread those things INSIDE too and faster, and zoom into the MIDDLE". **v3:**
  - gens 1-4 burst inside 1.5 s;
  - the interior is a crystal lattice that splits every triangle into 4 each generation, as a ripple from the centre;
  - a slow, steady zoom into the centre, with no rotation and no pulsing;
  - pull-back on the tonic.
  - Kept unchanged: the Fauré sync, HUD, counter and colour rule.

## World (logical 1080x1920)
- Snowflake centre (508, 790), circumradius 405. Triangle / snowflake x 157-859, y 385-1195.
- Edge: exact Koch construction (numpy). `subdivide()` turns each edge into A, A+d/3, apex, A+2d/3, with the apex popping out (ease-out-back). 8 generations: **3 → 12 → 48 → 192 → 768 → 3,072 → 12,288 → 49,152 → 196,608 edges**.
- **Inside (v3): the crystal.** A triangular lattice anchored on the base triangle. Generation k adds the level-k lines (spacing side/2^k), so every triangle splits into 4.
  - The new lines spread from the centre as a ripple with a bright front (white-cyan, α 0.8), then settle to a faint grid (α 0.30 → 0.20 → 0.13 → 0.09 as they age).
  - The newest facets light up softly as the front passes (α ≤ 0.11).
  - Every lattice level ≥ 28 px on screen carries a faint light/dark facet pattern (hash per triangle, α 0.07).
  - Lines fade in between 3 and 13 px screen spacing, so there is no aliasing mesh. Everything is clipped to the snowflake.
- Colour rule: one radial icy gradient (white-cyan h .52 → aqua → azure → blue → indigo → violet h .765, S ≤ 0.70), fill V 0.58-0.65. Each generation's ripple shifts the tint one step (0.05) along the ramp, so the crystal slowly cools from aqua to azure/blue. Rim gradient white-cyan → violet at the tips. Gold = only ∞ (the meter goal, "→ ∞", INFINITE).
- Sprout glints on the rim: white-cyan ADD fill + bright new edges, 0.3 s.
- HUD: meter y 1262 "PERIMETER ×N.NN" (fill 1 − (3/4)^n, gold ∞ goal from frame 0). A "×4" pill y 1336 pops on each generation's beat. Counter y 1478 "N EDGES" (true count). Watermark "DOPAMINE.EXE" (900 right, 1338), 35%.

## Camera (v3)
- Pure zoom about the centre (a vertex of every lattice level): no rotation, no translation, no pulsing.
- From 1.3 s it eases in (0.6 s) to a steady ×2 per generation (one generation = 3 beats = 2.14 s, 0.29 log3/s). That rate keeps each new facet level at ~18-38 px on screen. It eases to a stop over the 0.6 s before the tonic.
- Zoom ×1.1 (2 s), ×1.6 (3 s), ×3.0 (5 s), ×7.9 (8 s), ×14 at the tonic. Then a 1.5 s log-space pull-back to ×1.
- While zoomed, the picture fades out at y 300-410 (clean caption band) and y 1090-1228 (HUD band).

## Clock (84 bpm, clip beat 2.0 = 0.05 s)
- Generation ripples start on the beat grid:
  - gens 1-4 on the eighths 2, 2.5, 3, 3.5 (0.05, 0.41, 0.76, 1.12 s; 0.3-beat ripples centre → rim);
  - gen 5 on beat 4 (1.48 s, the flute's entry), gens 6/7/8 on beats 7/10/13 (3.62, 5.76, 7.91 s);
  - 3-beat windows (gen 8: 2.75 beats).
- On screen the ripple front runs from the centre to 760 px over its window; its world speed is c/Z, so the zoom never outruns it. An off-frame tail carries it to the rim before the tonic.
- Edge sprouts:
  - Gens 1-4 pop where their ripple reaches the edge (symmetric bursts: 3 by 0.46 s, 12 by 0.83 s, 48 by 1.18 s, 192 by 1.53 s).
  - From gen 5 (rim mostly off-frame) they sweep tips → notches, evenly and accelerating, over the window.
  - Sprouts per second: 63, 336, 372, 624, 1,464, 2,052, 5,604, 6,996, 23,412, 24,612.
- **0 s** big glossy triangle. **0.5 s** hexagram cut into lattice facets, 12 edges. **1 s** gen 3 snowflake, 156 edges, the inside 64 facets deep. **2 s** gen 5 ripple (bright hexagonal front) spreading in a 1,128-edge snowflake. **5 s** zoom ×3: the frame is all crystal, a new facet ripple crossing it, 8,364 edges. **8 s** ×7.9, 50,628 edges.
- **TONIC / INFINITE 10.05 s:** 196,608 edges, ×9.99.
- Finale:
  - The meter glides to the gold ∞ and the label becomes "→ ∞".
  - The camera pulls back to the whole crystal snowflake (blue centre → violet tips).
  - "AREA: 1.6×  —  never more" fades in.
  - The rim glow rises and two calm white-cyan shimmers run once around the edge.
- Hold 3.3 s from the tonic → 0.6 s dissolve into the triangle. **13.95 s, 837 frames.**

## Sound
- **Music played as music** (owner rule 2026-10-23): Fauré, **Pavane Op. 50** (1887; Fauré d. 1924, PD), at a steady 84 bpm. Source: Mutopia "Mutopia-2017/10/19-2196" (flute + guitar, after Hamelle 1901; engraving CC BY-SA 4.0, notes PD), `<SOUNDFONTS_DIR>\scores\faure_pavane\GF_pavane50.mid` + `SOURCE_mutopia_2196.txt`. Not on the used/banned lists, not kid-coded, never used by any scene.
- Splice: score beats 2-12 (bar 1's second half = pizzicato arpeggio; bars 2-3 = the flute theme), then bar 16 (closing C#7). Bar 17's F#-minor tonic lands on INFINITE.
- Arrangement (lib/orchestra): pizzicato strings + soft harp on the arpeggios, flute on the melody, strings_slow 8vb + celesta 8va from bar 3, cello/contrabass half-bar bass, oohs pad, timpani F#2 on gen 1 and a C# roll on bar 16. Cadence: rolled F#m harp chord + held strings/oohs/flute F#4/bass, soft timpani. A falling harp glissando goes with the pull-back, and a rising celesta + harp cascade with the shimmer.
- SFX: crystalline ticks.
  - Sources: each on-screen sprout group (symmetric sprouts pop together; gens 1-4 bigger and rounder), plus the ripple front clicking across each third of a new facet row while it is on screen.
  - Tone: bell partial on a chord tone of the half-bar (C#5 → D6 by generation), plus 2× and 2.76× partials < 5.5 kHz, a glassy knock and a 1.2 ms click.
  - Sampling and gain: ≥ 12 ms apart (+ seeded jitter when dense), gain ÷ √(rate/10).
  - 315 ticks; per second 21, 36, 35, 39, 39, 25, 33, 24, 39, 24. sfx ×0.30.
- `level_bed` (fin 7 dB, cresc 3 dB), `audio.master(peak_db=None, reverb=0.5)`, last 0.6 s digital silence.

## Checks (encoded Full HD, v3)
- h264 yuv420p 1080x1920, 60 fps, 837 frames, 13.95 s. **flash_check PASS**: 1 general flash in the worst second (at 10.88 s, the pull-back from the full-frame crystal to the whole flake), limit is 3. Mean lum 0.068.
- **−14.00 LUFS**, peak −5.81 dBFS, last 0.5 s digital silence, energy > 6 kHz 0.002%. RMS per second: −18.1, −17.5, −18.4, −17.6, −17.8, −17.7, −16.9, −17.1, −16.8, −16.9, −13.8 (tonic), −13.9, −14.6, −36.7. Late body (8-10 s) −16.9 vs finale (10.1-11.5 s) −13.7 (+3.2 dB).
- Seam (check_clip, encoded): mean |Δ| 0.164.
- Frames read from the mp4 at 0, 0.5, 1, 2, 5, 8, 10.6, 11.6 s and the last frame. 1:1 crops at 5 s and 8 s: crisp lattice lines and shaded facets.

## Doubts
- The pull-back registers 1 general flash (bright full-frame crystal → mostly black). It passes, but it is the one big luminance change. A longer pull-back (`--pull 2.0`) would soften it.
- The interior lattice (halves) does not line up with the Koch bumps (thirds) near the rim in the whole-flake view. The owner asked for "splits into 4"; a split into 9 would align, but its facets would be too fine on screen early in the zoom.
- Zoomed in, the frame is a uniform aqua-blue crystal; the visible change is the ripple fronts and the slow zoom.

## Flags
`--label --cap --still --frame a,b --dry --sound 0 --sfx (0.30) --fin (2.0) --bpm (84) --hold (3.3)`.
- Geometry: `--rad (405) --gens (8) --sweepa (0.8)`.
- Camera: `--zv (log3 2 / 3 beats)`, `--zt0 (1.3)`, `--pull (1.5)`.
- Ripple: `--rho1 (760)` px.
- Look: `--fillv (0.58)`.
- `--dry` prints ripples, sprouts, facet spacing, zoom and ticks/s.

Owner review (2026-10-23): "nope; search successful versions in example channels" -> research first (research/fractal_shorts.md).

Decision (2026-10-23): shelved after research/fractal_shorts.md (Koch topic underperforms on Shorts); v3 kept in DopamineExe/reserve.
