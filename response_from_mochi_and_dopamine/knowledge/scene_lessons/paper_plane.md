# paper_plane — Dart or glider: whose plane flies FARTHER? (batch59, 2026-10-29)

## v3 (batch61, 2026-10-30): the two designs obviously different at a glance
- Owner on v2: "better, but it's not clear what the difference between them is." v2 script: scratchpad `paper_plane_v2.py` (builder S); v2 video → `MochiAndBolt\archive\paper_plane_v2.mp4`. Deliverable: `<VIDEOS_DIR>\MochiAndBolt\review\batch59\paper_plane.mp4` (**v3**, Full HD, label v3, 16.25 s, 975 frames). Sim, story, banners, stats and sound unchanged (events json bit-identical to v2).
- **Shape card 0-2.7 s** (in the chart box, crossfades to the speed chart over 0.35 s): both planes from ABOVE at the same scale (same sheet), drawn to their stated areas (the glider outline is 2.1x the dart's): "MOCHI'S GLIDER · WING 160 cm² · LIGHT NOSE" (short, blunt, very wide wings) vs "BOLT'S DART · WING 80 cm² · HEAVY NOSE" (long, narrow, swept, a shaded folded nose). Gold tags: **"BIG WINGS = FLOATS"** / **"SMALL WINGS = FAST"**.
- **Persistent:** HUD names carry a tiny top-view icon of each plane, and the sub line reads "BIG WINGS = FLOATS · gentle 5.5 m/s toss" / "SMALL WINGS = FAST · thrown HARD: 14 m/s".
- Proof-read: tags are true for this model (dart trims ~6.4 m/s vs glider ~3.3 m/s: lower wing loading floats slower); "HEAVY NOSE" = the dart's folded nose layers (not a separate mass in the sim; a point-mass model).
- Checks (encoded): h264 High yuv420p 1080x1920 60 fps, 975 frames; -14.00 LUFS, peak -2.76 dBFS, last 0.5 s silent; flash PASS. Frames read at 0.1, 1.5, 2.8 (crossfade), 13.3 s.

## v2 (batch60, 2026-10-30): FLAT ground, the dart wins + NERD STATS, less cartoon
- Owner on v1: "ok but too cartoonish" + add nerd stats (lift, drag, L/D, angle of attack, speed vectors). Coordinator: Bolt wins where physics honestly allows it → flat ground. v1 video → `MochiAndBolt\archive\paper_plane_v1.mp4`; v1 script at scratch `m60/paper_plane_before.py`. Deliverable: `<VIDEOS_DIR>\MochiAndBolt\review\batch59\paper_plane.mp4` (**v2**, Full HD, 16.25 s, 975 frames, label v2). Caption unchanged ("Dart or glider: / whose plane flies FARTHER?").
- **Physics (same model as v1, new throws):** both release at x 0, 1.8 m (same hand height). Dart 14 m/s at +4° (S 80 cm², CL 0.25, L/D 3.68); glider 5.5 m/s level (S 160 cm², CL 0.45, L/D 6.90); 5 g sheet, lift capped at 1.8 g. Angle of attack shown = CL_eff / lift slope (dart 2.0, glider 4.0 per rad; trim 7.2° / 6.4°, lower while the flex cap acts). Result: the dart zooms to 5.26 m and lands at **18.81 m after 3.20 s**; the glider phugoids (slows to 1.9 m/s at its first crest) and lands at **16.97 m after 5.23 s**. From hand height the throw energy beats the glide ratio (v1's 6 m hill flipped it).
- **Story / banners (all checked literally true):** "SAME PAPER · SAME 1.8 m HAND HEIGHT" → 1.25 s "THE DART TRADES SPEED FOR HEIGHT" (climbing while slowing) → apex "THE GLIDER GLIDES BETTER: L/D 6.9 vs 3.7" → 7.67 s "DART DOWN: 18.8 m" → "…THE GLIDER IS STILL FLYING" + live "GAP TO THE DART: x.x m" (5 → 1.8) → cadence 13.04 s the glider lands short: "BOLT WINS / 18.8 m vs 17.0 m". Twist: Mochi (annoyed): "mine stayed up LONGER" / "5.2 s vs 3.2 s in the air"; Bolt grins next to his dart.
- **Nerd stats:** force vectors on each plane (v white, L blue, D red, W grey; 1.3 px/mN, 8 px per m/s); a stat panel per plane (SPEED, LIFT · DRAG in mN, live L/D · ANGLE OF ATTACK; after landing: distance + time in the air) with a dashed leader line; a SPEED-vs-FLIGHT-TIME chart (the dart spends 14 → 3.9 m/s climbing, dives back to 7; the glider sits at 3-4 m/s). HUD: distance per plane, FLIGHT TIME (real) + "slow-mo x2.6".
- **Less cartoon:** white folded-paper planes with crease lines and a thin coloured trailing edge (not candy-coloured), thin dashed trails, a sports field with mown stripes, a yellow measuring tape (labels every 2 m), chalk throw line, soft real sky. Characters unchanged (they chase their planes at real speeds, so they run in slow motion too).
- Timing: frame 0 = 0.30 s after release (planes already apart); slow motion x2.65 so the glider lands on the cadence. Camera: one smooth pan (σ 0.6 s), PPM 56, ground y 1225.
- Sound: as v1 (Bach Gavotte en Rondeau, same excerpt and cadence); ticks every 0.5 m per plane, after the dart is down the glider ticks every 0.25 m, every 0.125 m inside 4 m of the mark (the rate climbs to the landing), rising in pitch; banner dings; no running pats.
- **v2 checks (encoded):** h264 High yuv420p 1080x1920 @ 60, 975 frames = 16.25 s; muxed -14.00 LUFS, peak -2.76 dBFS, last 0.5 s silent; flash PASS (0); seam 0.93 vs 0→1 0.77 (good band). SFX/s 10 7 6 6 5 7 7 13 6 6 5 9 10 5 0 (climbs into the landing). Frames read: 0.0, 2.5, 3.5, 7.8, 10.5, 12.6, 12.9, 14.0, 14.5 s. Key content x 110-906 (the tape and trails run to the edges = decoration).
- **v2 doubts:** the 1.8 g lift cap + fixed trim CL make the glider phugoid hard (1.9 m/s at its first crest, nose-down dive after it): honest for this model, may look odd. In the last ~0.2 s of the glider's flight the W/D labels overlap the plane near the ground. The trimmed-CL model has no stall/loop, so "a hard-thrown glider loops" is NOT shown (only claimed in the pinned-comment option; keep it out of the screen). 100 % slow motion (x2.65) until the landing.

- Brief: docs/BRIEF_batch59.md (Mochi & Bolt 3). New scene file; caption/banner/HUD/sound chain copied from coffee_milk; lib/ and tools/ untouched.
- Deliverable: `<VIDEOS_DIR>\MochiAndBolt\review\batch59\paper_plane.mp4` (**v1**, Full HD 9:16, 16.25 s, 975 frames; output label v1).
- Caption (baked; `--nocap` gives the base): "~Dart~ or ~glider~:" / "whose plane flies ~FARTHER~?"
- **Story:** a grassy hill (6 m) over a field with a metre ruler. Frame 0 is 0.22 s after release: Bolt (behind) has thrown a slim DART hard, Mochi (in front) launched a wide GLIDER gently overhead. A DISTANCE race meter (0-45 m) sits above. "THE DART IS WAY FASTER!": it swoops up to 9.2 m and dives; Bolt sprints after it. 5.9 s "DART DOWN: 36.7 m" (flag). 7.2 s "…THE GLIDER IS STILL FLYING" (3.4 m/s, flat 1:7 glide); Bolt walks out past his dart to "catch" it. 10.9 s "THE GLIDER PASSES IT!" (gold ring on the meter). Cadence 13.04 s: it lands ON Bolt's head at 43.9 m; "MOCHI WINS · 43.9 m vs 36.7 m", "(it landed ON HIS HEAD and still won)". Bolt deadpan, Mochi laughs.

## Layout
- Ground y 1180, 50 px/m, hilltop 6 m (x ≤ 0, cosine slope to 8 m). Characters r 44 (1.62 m tall). Planes drawn ~80 px (cartoon size), dotted flight trails in each colour.
- One smooth pan (camera planned offline: Gaussian-smoothed midpoint of the action, σ 0.7 s, no zoom). Meter y 420-650 (track x 240-760, values at x ~846). HUD y 1366-1544: FLIGHT TIME (real time), per plane SPEED m/s · height, or LANDED.
- Safe zone: key content x 108-907 except Mochi/hill briefly sliding off the left as the camera pans (she walks back into frame by the end).

## The physics (honest; dt 1/600 s, real time)
- 2-D point mass, 5 g sheet. Lift q S CL at a fixed trim CL, capped at 1.8 g (a paper wing flexes and spills lift); drag q S CD; gravity; air 1.2 kg/m³.
- Dart: S 80 cm², CL 0.25, CD 0.068 (L/D 3.7, trims ~6.4 m/s); thrown 12 m/s at −2° from 7.0 m. Glider: S 160 cm², CL 0.45, L/D 6.9 (trims ~3.3 m/s); launched 4 m/s level from 7.75 m (overhead).
- Dart lands at 36.7 m after 6.1 s. The glider's free flight would reach ~55 m at 16.6 s; it meets Bolt's head height (1.62 m) at 43.9 m after 13.3 s (that's where Bolt stands, and where its distance is measured). Distances are from each thrower's release point.
- Honest caveat: the result needs the launch height. From hand height on flat ground a hard-thrown dart can win; from a hill the glider's better glide ratio wins (on screen: "SAME HILL").

## Sound
- **Piece:** J. S. Bach, Partita No. 3 in E BWV 1006, Gavotte en Rondeau (1720; d. 1750, PD). The Preludio of the same partita was used before (different movement); not on the used/banned lists; not kid-coded.
- **Source:** Mutopia Project PD, `<SOUNDFONTS_DIR>\scores\bach_gavotte_bwv1006\bwv-1006_3.mid` + SOURCE.txt; read at runtime.
- **Excerpt:** the rondeau theme from its half-bar upbeat, quarter = 138 (tempo chosen so the glider lands on the cadence); cadence = the theme's E major close (beat 30, 13.04 s).
- **Arrangement:** violin (the score's top line + its double stops), soft piano doubling, flute 8va, cello roots + pizzicato on a written E-major continuo (the solo-violin score has no bass); cadence = timpani E, strings, harp sweep, violin E5, celesta, held strings.
- **SFX (tonal):** release flicks, a tick per whole metre per plane (every 5 m brighter), after the dart lands a half-metre glider tick rising in pitch toward the mark, Bolt's soft running pats, the dart's skid flicks, banner dings, a paper pat on Bolt's head + cadence chime.
- Mastering: `level_bed` (+3 dB crescendo, findb 2.0) → `master_keep_lift` (-14 LUFS, -2 dBFS); last 0.5 s zeroed.

## Checks (v1 encoded, Full HD)
- h264 yuv420p 1080x1920 @ 60 fps, 975 frames = 16.25 s. -14.00 LUFS, peak -2.78 dBFS, last 0.5 s -240 dBFS.
- RMS/s: -19.4 -18.9 -18.7 -18.6 -17.9 -18.0 -17.7 -17.6 -17.5 -17.3 -16.8 -16.5 -16.9 -14.4 (cadence) -19.7 -34.5.
- SFX events/s: 15 18 17 16 17 19 8 15 13 14 11 6 7 5 0.
- flash_check PASS (0). Seam mean |delta| 0.51 (good band).
- Frames read from the mp4: 0.5, 3.0, 6.0, 11.0, 13.6 + a 1:1 crop of the head landing at 13.6 s.

## Doubts
- The long middle (6-11 s) is one slow glider + a climbing meter; the "still flying" banner and the rising ticks carry it. Event rate falls after the dart lands.
- The planes and characters are drawn larger than scale (readability).
- Mochi walks off the left edge for ~3-8 s while the camera follows the planes.

## Args and cost
- `--sfx --findb`; `--still --frame a,b`, `--audition`, `--report`, `--reuse`, `--nocap`, `--label`.
- Sim < 1 s; Full HD render ~35 s at 2 encoder threads.

## Outcome
- (fill after upload)
