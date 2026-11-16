# spin_arms — Arms OUT or arms IN: who spins more TURNS? (batch59, 2026-10-29)

- Brief: docs/BRIEF_batch59.md (Mochi & Bolt 2). New scene file; caption/banner/HUD/sound chain copied from coffee_milk / ice_cubes; lib/ and tools/ untouched. A custom spinning-skater drawer (arms orbit the axis, the face sweeps round the body, back view when facing away, motion-blur ghost faces + white swooshes when fast).
- Deliverable: `<VIDEOS_DIR>\MochiAndBolt\review\batch59\spin_arms.mp4` (**v1**, Full HD 9:16, 13.10 s, 786 frames; output label v1).
- Caption (baked; `--nocap` gives the base): "~Arms OUT~ or ~arms IN~:" / "who spins more ~TURNS~?"
- **Story:** an ice rink, both skaters already spinning at frame 0 (push-off 0.45 s before). "BOLT PUSHES OFF HARDER" (115 vs 64 RPM, he leads on TURNS). On every bar (1.2 / 2.4 / 3.6 / 4.8 s) Mochi pulls her arms in further (reach 80 → 62 → 48 → 34 cm, HUD) and her RPM jumps (64 → 137). "ARMS IN = SPINS FASTER"; 5.7 s "MOCHI TAKES THE LEAD!". Bolt's wide arms bleed his spin (115 → 56 RPM). Cadence 9.6 s: Mochi throws her arms OUT and visibly slows 2.6x (the same law, backwards), toe-stops; "MOCHI WINS · 19 vs 14 TURNS". Twist: Bolt (who spun less) gets X-eyes + stars and wobbles off the right edge: "…and HE'S the dizzy one".

## Layout
- Ice y 1192; skaters r 110 at x 322 / 694; arm reach 1.62 r (hands x 144-872 at full reach). TURNS boxes y 448-616 (big number, MORE pill on the leader), RPM gauges y ~728 (0-200). HUD y 1366-1544: SPIN TIME (real time), ARM REACH cm + bar, spin inertia kg·m².
- Static camera; navy/ice palette, no flash. Bolt's exit goes past the right edge on purpose (the twist, after the result).

## The physics (honest; dt 1/60, real time)
- I = 1.0 + 2.0 × reach² kg m² (3.0 arms out, 1.1 arms in). L = I ω is conserved while the arms move.
- Torques only: blade friction 0.20 N m + arm air drag 0.024 ω² reach³ (wide arms at speed lose much more). After the finale a toe-pick stop (9 N m) for both.
- Push: Mochi 1.10 rev/s, Bolt 2.00 rev/s (arms out). Result 19 vs 14 turns; Mochi's peak 137 RPM, Bolt's 115 → 56 RPM by the cadence.

## Sound
- **Piece:** P. I. Tchaikovsky, The Seasons Op. 37a, "February: Carnival" (1876; d. 1893, PD). Not on any used/banned list; not kid-coded.
- **Source:** Mutopia Project PD, `<SOUNDFONTS_DIR>\scores\tchaikovsky_seasons_feb\Tschaikowsky-op37.2.mid` + SOURCE.txt; read at runtime.
- **Excerpt:** 2/4, quarter = 100 (bar 1.2 s): bars 1-8 (the theme), cadence = D major tonic on bar 9 (9.6 s; the score's Bb5 run resolves to A5 over D).
- **Arrangement:** piano (score), violin top line, flute 8va soft, pizzicato bass, celesta glint per downbeat; cadence = timpani D, strings, harp sweep, piano chord, celesta, held strings.
- **SFX (tonal):** a blade tick per half turn per skater (exact times, full turn louder, lane pitch), a rising 3-note ding at each arm pull, lead-change and cadence dings, two soft sinking vibrato tones for Bolt's dizzy wobble.
- Mastering: `level_bed` (+3 dB crescendo, findb 2.0) → `master_keep_lift` (-14 LUFS, -2 dBFS); last 0.5 s zeroed.

## Checks (v1 encoded, Full HD)
- h264 yuv420p 1080x1920 @ 60 fps, 786 frames = 13.10 s. -14.00 LUFS, peak -2.00 dBFS, last 0.5 s -240 dBFS.
- RMS/s: -18.5 -18.1 -17.7 -17.6 -17.2 -17.0 -16.5 -16.1 -16.0 -15.6 -15.2 (cadence) -26.2 -35.0.
- SFX events/s: 7 8 9 9 10 9 6 7 6 9 4 2 0.
- flash_check PASS (0). Seam mean |delta| 0.93 (inside the 1.1 limit; both skaters are moving at the seam, true dissolve).
- Frames read from the mp4: 0.5, 2.5, 5.0, 5.8, 9.0, 10.4, 12.0 + a 1:1 crop of both skaters at 7.1 s.

## Doubts
- Mochi spinning at ~2.2 rev/s shows her back half the time (an honest rotation); swooshes and blur ghosts carry the speed.
- Bolt's harder push is the source of the early lead; stated on screen at 0 s.
- Event rate dips after the last pull (ticks only, 6-7/s) and falls after the cadence (the stop is the finale).
- The arms-in hug is drawn as forearms folded under the face (toon simplification).

## Args and cost
- `--sfx --findb`; `--still --frame a,b`, `--audition`, `--report`, `--reuse`, `--nocap`, `--label`.
- Sim < 1 s; Full HD render ~25 s at 2 encoder threads.

## Outcome
- (fill after upload)
