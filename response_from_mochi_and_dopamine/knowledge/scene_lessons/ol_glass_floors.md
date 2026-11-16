# ol_glass_floors (Dopamine.exe)
- New character-free scene (docs/BRIEF_batch51.md "ol_glass_floors"; batch50 + overnight_1023 rules). A stack of steel balls smashes down a glass tower. Every time the stack stops, a new ball as heavy as the whole stack drops onto it, and they go down together.
- Caption (baked, `--cap`; `--cap ''` = base): `Every time it ^STOPS^, add another ball|how many to reach the ~GROUND~?` (`^x^` = glass cyan, `~x~` = gold).
- Delivered: `<VIDEOS_DIR>\DopamineExe\review\ol_glass_floors_asmr.mp4` (**v4 ASMR**, Full HD, label fhd5asmr, 20.70 s, 1,242 frames). Archived: v3 music `archive\ol_glass_floors_v3_music.mp4`, v3 ASMR `archive\ol_glass_floors_v3_asmr.mp4`, v2 `archive\ol_glass_floors_v2.mp4`. **4K shipped (batch 56): `schedule\2026-11-05\2_ol_glass_floors.mp4`**; the FHD review copy = `archive\ol_glass_floors_fhd.mp4`. The v2 sections below still describe the sim, look and music; v3 changed the camera; v4 the stop holds.
- History:
  - **v1** (2026-10-25, label fhd2): one 1-TON ball against 100 floors, with two stubborn floors that held for a beat. The v1 scene file is kept at scratchpad `ol_glass_floors_v1.py`.
  - Owner review: "maybe start with a smaller ball, and when it stops, another ball is added and they both go down, with physics". The coordinator also found v1's shard cloud above the ball cluttered.
  - **v2** made these changes:
    - the ball-stack mechanic, a 64-floor tower and total mass ×2 per added ball;
    - shards clear within about 0.6 s;
    - a new caption and HUD.
  - Kept from v1: the glass, the camera, the music and the finale.

## SHIPPED v4 ASMR (batch 56, 2026-10-28): owner "ok"
- 4K: `NF_SCALE=2.0 python scenes/ol_glass_floors.py --asmr --hx 0.8 --label ship` -> `<VIDEOS_DIR>\DopamineExe\schedule\2026-11-05\2_ol_glass_floors.mp4`, 16:00 local Nov 6 (= 07:00 US East Nov 6). FHD review copy -> `archive\ol_glass_floors_fhd.mp4`.
- Checks (encoded 4K): h264 yuv420p 2160x3840, 60 fps, 1,242 frames, 20.70 s; -14.01 LUFS, peak -7.76 dBFS, last 0.5 s digital silence; seam 0.842; flash PASS (0 flashes). Events json + audio wav bit-identical to the reviewed fhd5asmr. Frames read at 0, 2.1, 9.33, 17.75, 20.68 s.

## v4 ASMR (2026-10-28, batch 55): each stop SITS longer
- Owner review of v3: "ok, but when it stops, don't drop the next ball that fast: let it sit a little longer. I like the ASMR more." The ASMR soundtrack is the only version now (no music cut of v4).
- `--hx 0.8` (default 0 = v3): 0.8 s of stillness inserted into every stop, 0.1 s after the hit (after the bounce), before the next ball starts falling. Implemented as a warp of the score-beat clock (`tt`/`bt`): every event after a stop's pause point shifts by 0.8 s; the sim, camera, stack and glass all run on clip time, so the physics is unchanged. Each stop now sits hit -> add 1.2 s (was 0.4), hit -> give 1.6 s (was 0.8). Clip 17.5 -> **20.70 s** (`--dur` defaults to 17.5 + 4 x hx). Use `--hx` with `--asmr` only (the music bed would no longer line up).
- While it sits: the spiderweb creeps a little (crack length +0.12 floor over the pause) and soft settling sounds fill the quiet: crack ticks every 0.11-0.24 s (gain 0.05-0.08) + 2 shard tinks per stop.
- Stops: floor 59 hit 0.90 / ball lands 2.10 / gives 2.50; floor 53 4.10 / 5.30 / 5.70; floor 43 8.10 / 9.30 / 9.70; floor 25 12.90 / 14.10 / 14.50; **ground 17.70 s**. Crashes/s 4, 0, 2, 4, 0, 1, 4, 5, 0, 1, 4, 5, 8, 0, 2, 6, 10, 7 (the runs still get longer and faster; each stop is a deliberate rest).
- Command: `NF_SCALE=1.0 python scenes/ol_glass_floors.py --asmr --hx 0.8 --label fhd5asmr` (4K: `NF_SCALE=2.0 ... --asmr --hx 0.8 --label ship`).

### Checks v4 (encoded Full HD, fhd5asmr)
- h264 yuv420p 1080x1920, 60 fps, 1,242 frames, 20.70 s. **flash_check PASS** (0 flashes).
- **-14.01 LUFS**, peak -7.76 dBFS, last 0.5 s digital silence. RMS/s -17.3, -18.5, -16.4, -18.1, -17.3, -16.6, -18.0, -17.1, -17.1, -16.4, -17.4, -16.9, -16.8, -17.4, -16.1, -16.9, -16.5, -15.8, -15.3 (ground), -20.4, silence. 873 SFX events (all >= 12 ms apart).
- Seam mean |delta| 0.916 (same as v3: held camera at frame 0).
- Frames read from the mp4 at 0, 0.95, 1.6, 2.1, 2.6, 4.6, 8.7, 13.5, 17.75, 20.65 s (the 10 kg ball sits alone on floor 59 for 1.2 s, the 10 kg ball drops in at 2.1, the pane gives at 2.5).

### Doubts v4
- Longer (20.7 s). The stops are now calm rests; the event rate dips to ~0-1 crash/s in each stop by design (the owner asked for it), and climbs again on every run.
- Still unheard by me: the settle ticks are quiet (-26 dB under a shatter); if the stop feels empty, raise them (`build_events_asmr`, HX block).

## v3 (2026-10-28, batch 53): the camera LAGS + an ASMR twin
- Owner review of v2: "the camera goes down very fast: it feels like WE move and the balls try to catch up. Let the balls crash more glass before we follow down (camera/perspective only, don't change the physics). Maybe glass-shatter sound and no music: make a second ASMR version."
- Cause: v2's camera was a CENTRED Gaussian (σ 0.22 s) of the pile, held at y 620 (upper part of the window). A centred filter is non-causal: it started moving ~0.3 s BEFORE each pane gave, and the pile sat above centre with empty floors below = the view ran ahead.
- **v3 camera (`--cam lag`, default; `--cam v2` = the old one):** a causal controller, same sim, same events, same zoom.
  - **hold**: the view stays still while the pile smashes down the frame from y ~600 to the trigger line **y 1040** (predicted 0.14 s ahead) = 2.5-3 floors of glass broken in a still frame.
  - **follow**: then it eases in (velocity smoothing τ 0.16 s) and follows with the pile LEADING low in the frame (line y 960, catch-up τ 0.30 s). It never moves up and never moves before the balls do.
  - **settle**: on every stop the camera eases on until the stopped pile sits at **y 600**, braking at 20 floors/s² so it never overshoots; then it holds again for the next fall. It brakes into the ground stop the same way (no jerk).
  - Flags `--yrest 600 --ytrig 1040 --yfol 960 --tauf 0.30 --taus 0.24 --tauv 0.16 --abrake 20`.
  - Pile screen y (camera analysis): run 1 holds 0-0.4 s (620 → 950), stop 1 at y ~1019, settles to 585-600 by 1.5 s; runs 2-4 hold ~0.8 s each (600 → 1000) before following; the final 25-floor run holds to 12.4 s, peaks at y 1090, then follows at y ~955 into the ground. The stopped piles are always fully in frame.
- **ASMR twin (`--asmr`)**: the same video (`--video <mp4>` re-muxes without re-rendering), NO music. All our own numpy/scipy synthesis, no samples:
  - every crash: 2 glass crack ticks (−26/−13 ms), then the **pane shatter** (a cloud of 34-74 tiny glass grains 1.6-6.4 kHz, 2-22 ms each, densest at the start, on a soft 400-2,400 Hz crunch body, low-passed at 7 kHz), a weight thud (lower as the stack gets heavier), 3 (7 on a give) shard tinks tinkling down on an F-minor pentatonic;
  - **steel**: the stack's real ball-ball contacts as steel clinks (modes 1/2.43/4.1, ≥ 30 ms apart); a continuous **roll** per ball from its real speed on a stopped pane / the ground (band-noise rumble, darker for heavier balls, a faint singing tone), ×0.25;
  - every **added ball**: a deep round thud (95 Hz for 20 kg → lower for heavier) + a steel clank + crack ticks; stops: a ringing glass-plate bonk; 5 creak ticks before each pane gives;
  - ground: tonal boom + big shatter + deep thud + 10 concrete clacks; shard landings as soft tinks (≥ 24 ms apart); the gold glints on the two closing chords.
  - Density gain 1/√(rate/5); all onsets ≥ 12 ms apart (783 events); `audio.master(peak_db=-6, reverb=0.6)`; last 0.6 s digital silence. Spectrum: 51% < 200 Hz, 26% 1-3 kHz, 11% 3-6 kHz, 0.7% 6-8 kHz, 0.09% > 8 kHz.

### Checks v3 (encoded Full HD, label fhd4 / fhd4asmr)
- Both: h264 yuv420p 1080x1920, 60 fps, 1,050 frames, 17.50 s. **flash_check PASS** (0 flashes).
- Music version: **−14.00 LUFS**, peak −5.64 dBFS, last 0.5 s digital silence (the soundtrack is v2's, unchanged).
- ASMR version: **−14.01 LUFS**, peak −5.32 dBFS, last 0.5 s digital silence. RMS per second −17.5, −16.2, −18.4, −16.3, −17.6, −17.5, −16.5, −16.8, −17.2, −17.1, −16.5, −16.5, −16.6, −16.9, −15.1 (ground), −16.2, −22.7, silence.
- Seam: mean |Δ| 0.916 (check_clip); luma last→0 0.646 vs a median frame step of 1.75 (v3's frame 0 is a held camera, so the seam is calmer than v2's 3.73).
- Frames read from the mp4 at 0, 0.5, 0.95, 1.33, 2.3, 2.9, 6.0, 6.95, 10.55, 12.7, 14.55, 17.45 s.
- Delivered: `<VIDEOS_DIR>\DopamineExe\review\ol_glass_floors.mp4` (v3, music) + `ol_glass_floors_asmr.mp4`; v2 archived as `archive\ol_glass_floors_v2.mp4`.

### Doubts v3
- Unheard: no listening test of the ASMR mix. The shatter is synthetic (grain clouds); if it reads as "hiss", lower `--asmr` shatter body or raise the tinks.
- In the long runs (stop 3 → 4 and the final 25 floors) the camera follows continuously after its hold (the pile leads at y ~955); a stop-and-go ratchet there would jerk at 5-10 floors/s.

## World (logical 1080x1920)
- Unit = 1 floor = 3.5 m. Window: a thin white frame at 128-888 × 318-1226. Tower centre x 520, **64 floors**; the tower's top shows at frame 0. Floor labels sit left of the left column.
- Glass floors are seen slightly from above. Each plate has a projected depth of 0.40 floor and a back edge 10 % narrower. Colour is one ordered gradient across the width: teal (h 0.47) on the left to blue (0.62) on the right.
- Building: steel columns, a navy back wall and back-wall floor beams. Each broken floor leaves a bracket and a glass stub.
- Balls:

  | Order | Mass | Radius (floor) | Tint |
  |---|---|---|---|
  | 1 | 10 kg | 0.25 | cool steel |
  | 2 | 10 kg | 0.25 | |
  | 3 | 20 kg | 0.31 | |
  | 4 | 40 kg | 0.40 | |
  | 5 | 80 kg | 0.50 | warm bronze |

  - Radius ∝ m^(1/3). The tint is one ordered ramp from cool steel to warm bronze.
  - Each ball carries its mass ("40 kg") as a label that rolls with it.
- Camera: a Gaussian-smoothed follow (σ 0.22 s) of the middle of the landed pile, which stops on the ground. One smooth zoom-out runs from 165 to 140 px/floor.
- HUD:
  - Meter at y 1290: "n/64 FLOORS", with a gold GROUND goal visible from frame 0.
  - Counter at y 1478: amber "FLOOR" + a white number.
  - Line 2: a gold "×2" pill that pops when a ball is added, the total "40 kg" flashing gold, and "· n km/h", which turns amber at 0 while the stack is stopped.
  - Finale: "GROUND REACHED" / "5 BALLS · 160 kg" in gold.
  - Watermark "DOPAMINE.EXE".

## Rule / model
- Crash times sit on the music's 16th grid. Floors are evenly spaced, one floor per interval.
- Inside each interval the stack's support follows a smooth speed curve with the honest per-pane dip d = g·dt / 2v.
- Four stops, each laid out as hit (the stack stops), add (the new ball lands on its beat) and give (the pane breaks on the next downbeat):

  | Stop | Floor | Hit | Add | Gives | Total after add |
  |---|---|---|---|---|---|
  | 1 | 59 | 0.90 | 1.30 | 1.70 | 20 kg |
  | 2 | 53 | 3.30 | 3.70 | 4.10 | 40 kg |
  | 3 | 43 | 6.50 | 6.90 | 7.30 | 80 kg |
  | 4 | 25 | 10.50 | 10.90 | 11.30 | 160 kg |

  - A heavier stack goes further each time: 5, 6, 10, 18 floors, then 25 to the ground.
  - Restart from rest: 4-3-3 sixteenths, then eighths; sixteenths from 1120 (the arpeggio).
- Ball stack (`Stack`): rigid discs simulated in the support's frame, 4 substeps/frame.
  - Forces and contacts: stack gravity of 7 floors/s², the sagging pane as support, the walls, and mass-weighted position projection for ball-ball contacts.
  - Velocity caps (±1.8 / +1.9 floors/s) stop light balls from being flung.
  - Kicks: each crash jolts the bottom balls, each stop bounces them, and the ground scatters the pile outward.
  - Each new ball spawns 2.8 floors above the top of the pile and falls on a real-gravity arc (g = 2.8 floors/s²) timed to land on the add beat. Ball-ball clinks are logged for the sound.
- Glass:
  - Fracture nets (6-7 rays; 12-ray spiderwebs on the stop panes) are centred where the lowest ball hits.
  - Shards fall with gravity and drag, and flying shards fade out between 0.12 and 0.57 s. Shards resting on a stopped pane or the ground stay at 30-35 %.
- Ground: crater (half-width 1.15 floor), lip, cracks, 34 concrete chunks, a small warm glow, and an amber shock ring.

## Timeline (clip s)
- Frame 0: the 10 kg ball has just come through the top floor (64); floor 63 breaks at 0.10 s.
- 0.5 s: floor 60 breaks, at 65 km/h.
- 2 s: the 20 kg pair falls from rest past floor 58, at 37 km/h.
- Floor at each second: 63, 59, 58, 54, 53, 50, 45, 43, 40, 36, 29, 25, 22, 14, 4, then GROUND.
- **Ground at 14.50 s** (beat 1132, fff F-minor chord): the 160 kg pile craters the ground and scatters. The counter turns gold "GROUND REACHED · 5 BALLS · 160 kg" and the frame warms to gold.
- 15.30 / 16.10 s: the two closing chords, each with gold glints.
- 16.9-17.5 s: dissolve into the pre-roll.

## Sound
- **Music:** Beethoven, Piano Sonata Op. 57 "Appassionata", III, the end of the Presto coda (score beats 1095.75-1137), at **150 bpm**.
  - Source: Mutopia `BeethovenLv/O57/LVB_Sonate_57_3` (Breitkopf & Härtel 1862-65, Public Domain). Saved at `<SOUNDFONTS_DIR>\scores\beethoven_appassionata3\` + `SOURCE_mutopia.txt`.
  - The arrangement is the same as v1: the piano as written, strings, cello/contrabass, horns, timpani, and tutti F-minor chords with a boom on the ground.
- SFX (×0.50, all tonal):
  - Every crash is a glass hit pitched to the right hand's note at that 16th, plus 3 shard tinks and a thud on the bass note. The thud grows with the stack's mass.
  - Each stop is a ringing glass-plate bonk with crack ticks.
  - Each add is a heavy steel clank (bell partials 1/2.32/4.25/6.6) with crack ticks and a creak before the give. Each give is a doubled shatter.
  - Ball-ball clinks are soft tinks, at most one per 32nd.
  - The ground gets a tonal boom and concrete clacks, followed by shard tinks and the glints.
- Mix: the music body sits ~4 dB over the SFX. `level_bed` adds a +3 dB crescendo and the cadence sits at +4 dB, then `audio.master(peak_db=None, reverb=0.5)`, then 0.6 s of silence at the end.
- SFX events per second: 26, 36, 20, 34, 23, 25, 32, 26, 25, 30, 47, 30, 41, 50, 46, 44, 20.

## Checks (encoded Full HD v2, fhd3)
- h264 yuv420p 1080x1920, 60 fps, 1,050 frames, 17.50 s.
- **flash_check PASS**: 0 flashes, mean luminance 0.011.
- Audio: **−14.00 LUFS**, peak −5.64 dBFS, last 0.5 s digital silence.
- RMS per second: −18.2, −17.6, −17.8, −18.0, −17.1, −17.2, −17.3, −17.7, −17.0, −16.9, −16.6, −16.2, −16.4, −16.3, −14.7 (ground), −15.0, −20.4, silence.
- Seam: the last frame equals pre-roll frame −1 before encoding.
  - Encoded seam 3.73 (luma mean |Δ|) against a median frame step of 3.02 and a 0→1 step of 3.65. The camera scrolls, so this is a normal motion step.
- Frames read from the mp4 at:
  - the opening: 0, 0.5 and 2 s;
  - stop 1: 0.95 (stops), 1.32 (ball added) and 1.75 s (gives);
  - stop 2: 3.35 and 3.72 s; stop 3: 6.55 and 6.92 s; stop 4: 10.55, 10.92 and 11.4 s;
  - the impact at 14.52 s and the last frame at 17.48 s.

## Flags
`--label --cap --still --frame a,b (−36..1049) --dry --audio --sound 0 --sfx (0.50) --fin (2.0) --bpm (150) --dur (17.5) --vt (3.0) --z0 (165) --z1 (140) --sigcam (0.22) --seed (1)`. The FHD render takes ~4 min.

## Doubts
- **Physics is honest-ish:**
  - The stops are scripted on the beat: "panes slightly stronger lower down" is the story, not a computed strength.
  - Speed jumps from 8ths to 16ths at 9.7 s (65 → 126 km/h).
  - The restart after a give is faster than true free fall.
  - Ball sizes are visual: a real 10 kg steel ball is ~13 cm across.
- On each stop the pile spreads into one layer across the pane. The light balls roll to the walls, and the new ball lands on the top ball and then rolls off. It reads as "added to the pile", not as a tall tower of balls.
- Caption line 2 is a question. It is finite and the video answers it ("5 BALLS").

## Upload draft
- Titles (≤ 95 chars incl. the tags):
  - "Every time it stops, add a ball… how many to hit the ground? 💥 #satisfying #physics #shorts" (91)
  - "10 kg to 160 kg: smashing down through 64 glass floors 💥 #satisfying #physics #shorts" (85)
  - "It kept stopping, so we kept adding heavier balls 😬 #satisfying #physics #shorts" (80)
- Pinned comment: "the little 10 kg ball really thought it was done at floor 59… how many balls did you guess?"
