# blob_brawl — his hammer GROWS, her saw makes a COPY (shorts_1115 M3, 2026-11-15)

- Brief: docs/BRIEF_shorts_1115.md §M3 (the bounded fighter test, STRATEGY §2). New file `scenes/blob_brawl.py`; built fresh (the orb_battle / clones_battle / tug_war ideas, own code). lib/ untouched.
- Deliverable: `<VIDEOS_DIR>\MochiAndBolt\review\blob_brawl.mp4` (Full HD 9:16, label v1) + `blob_brawl_files\`.
- Caption (baked; `--nocap` = base): "Every hit: his hammer ~GROWS~, her saw makes a ~COPY~" / "Who breaks the other's ~SHIELD~ first?"

## Rules (sim, dt 1/240, seeded)
- Arena centre (508, 820), r 340 (x 168-848). Blobs r 44 (exact rest shape, faces upright ±10° wobble) inside glass shields r 70, HP 100.
- Constant 520 px/s, elastic wall + blob-blob bounces, no gravity. **Added: HOMING 3 rad/s** (both turn toward each other at the same rate). Without it the billiard blobs met ~1×/s and nothing happened for seconds; homing 1.5 → 0.5 saw hits by 6 s, 3.0 → 6.7. Stated in the doc, same for both.
- Props float (no limbs), orbit radius 100 at 4 rad/s (hammer +, saws −). Hit = prop touching the other shield; 0.3 s cooldown per prop; knockback 300 px/s × prop mass (hammer 1.15^n, saw 0.35), fading in 0.25 s.
- Hammer: damage 3 × 1.15^n, then grows ×1.15 (handle + head length and width, mass).
- Saws: each hit does **2.43** and adds a COPY that splits off the saw that hit; the ring re-spaces evenly (0.15 s ease). **Cap 24 saws** (a full ring at r 100); hits still count after that.
- D_S set ONCE by `--calib` (seeds 1-200, HP infinite, t ≤ 6 s): D_S 2.43 → Mochi 16.2 = Bolt 16.2 expected damage at 6 s (6.7 saw hits vs 4.2 hammer hits). The brief's "each saw does 1" could never break a 100 HP shield before ~100 saws; its "equal at 6 s" principle set the number instead.
- Outcome over seeds 1-580: KO < 13 s in 402; **Mochi wins 493 / Bolt 87** (the swarm usually wins). Seed chosen for timing only, within the majority outcome.
- K.O.: shield shatters (28 seeded shards), the loser is ejected (1500 px/s, decays 0.3 s, clamped inside x 200-820, y ≤ 1300) with an annoyed face, its prop fades in 0.4 s; the winner glides to a stop.

## Seed 74 (default)
- Hits: hammer 0.25 (frame-0 mid-swing, aimed), 1.82, saw 2.16, ... LEAD: Bolt from 0.25 s; **Mochi takes the lead 8.05 s**; **K.O. 11.80 s, Bolt's shield**. Hammer ×3.52 (9 hits), saws 24 (cap from ~9 s), 51 hits total.
- HP/s: 1s M97/B100 · 4s M90/B93 · 6s M80/B83 · 8s M67/B66 · 9s M67/B37 · 10s M59/B15 · 11s M59/B3.
- Hits/s: 1 1 1 3 1 5 2 7 12 10 5 3 (falls in the last 2 s: the ring is capped and Bolt is pushed around).
- Clip 15.02 s (901 f) = KO + 2.6 s stamp/recap + 0.6 s dissolve to frame 0.

## Sound
- Grieg, In the Hall of the Mountain King (1875, PD; Mutopia #1888, Grieg's piano score, read at runtime from `<SOUNDFONTS_DIR>\scores\grieg_mountain_king\`). Excerpt: beats 4-36 (the theme, bassoon/cello/pizz/basses 8va) + beats 324-340 (the presto hammer bars, violins/strings/horns/cellos) + the final B-minor chord (beat 349) ON the K.O. One accelerando: tempo linear in beats, doubling start → K.O.
- **Deviation:** the brief asked one melody note per landed hit up to ~8/s. Hits are 1/s and irregular early (owner 2026-10-23: event-triggered note walks sound choppy), so the piece plays as real music and every hit is SFX pitched to the sounding chord.
- SFX (own synth, no noise beds): glass-shield crack per hit (chord tone), hammer bonk (+12 ms), saw ting per new copy (+24 ms), K.O. shatter (14 glass tinks), ring-out thud at K.O. + 0.55 s.
- Master: own −14 LUFS / −2 dBFS lift (ice_cubes chain); music silent from T − 1.25, last 0.5 s digital silence.

## Checks (encoded Full HD, label v1)
- h264 yuv420p 1080x1920 @ 60, 901 f = 15.02 s; −14.01 LUFS (muxed, stereo), peak −1.98 dBFS, last 0.5 s −240 dB; flash_check PASS (0 flashes, mean lum 0.006); seam mean delta 0.24.
- Sound onsets: 83 of 94 event times (88 %) within 40 ms. Sound events/s 2 2 2 6 2 10 4 14 21 11 5 14 5.
- Frames read every ~1 s from the mp4; 1:1 crops of the swarm at 9.0 s and the K.O. at 11.85 s.

## Doubts
- Hit rate falls in the last ~2 s before the K.O. (saw cap + knockback separation).
- The arena (brief size) leaves the props small at frame 0; the hammer is a small block until ~×2.
- 24 saws overlap on the r 100 ring (reads as a buzz-saw ring).

## Args
- `--seed` (74) `--calib` `--homing` `--ds` `--dh` `--kb` `--d0`, `--still --frame a,b`, `--report`, `--nocap`, `--reuse`, `--label`. Sim < 1 s; seed search `output/tmp/mochi_1115/bb_search.py`.
