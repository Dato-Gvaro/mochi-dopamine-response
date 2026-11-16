# card_cascade
- New scene (batch38): the 90s PC card-game victory cascade as a Mochi vs Bolt duel (nostalgia hook, research/scroll_stop.md). No brand names, no copied card backs: the faces are our own drawing of the public-domain standard faces (pips; J/Q/K are a framed letter, not court art). The foundations are face-up, so no card back appears.
- Rule: "Every card that bounces leaves a TRAIL". Caption (baked, `--cap`): `Every card that bounces leaves a ^TRAIL^|~First to fill the table WINS~`.
- World: a beige 90s CRT monitor (rounded tube, faint scanlines, edge vignette, glare, power LED) in a dark room. The green felt screen (x 60-900, y 404-1292) is split at x 480 by a 12 px divider bar.
  - Mochi's half is on the left, Bolt's on the right. Each sits on a face-up foundation pile in a top corner (x 95 / 865; Bolt's face ends at x 914).
  - Every frame each card stamps a copy of itself (white card with a coral or teal edge): the smeared trail.

## Physics and the choice
- g = 1700 px/s². Felt restitution 0.60 (vx x0.97 per bounce); side walls and the divider 0.85, and a card is stamped AT the wall on its contact frame. A rebound under 160 px/s makes the card slide out (500 px/s²) and stop.
- Ranks A → K, one beat each, beats 1.80 s → 0.55 s (the escalation).
- **Mochi, HIGH toss**: one card per rank, thrown up off the top of the screen (vy 820-1120 up, vx 0-460). She "eyeballs the bare patch" by picking the best of 24 random tosses by fresh coverage. Each card falls from above the screen, so every arc is tall and paints top to bottom.
- **Bolt, LOW flick**: four cards per rank (every suit, 0.09 s apart), flat off the pile (vy +40), faster every rank (vx 400 → 1100, ±1.5%). More cards and fast low coverage, but a flat flick can never rise above the pile it leaves. The top band and the pocket under his own pile stay bare: he stalls at 86%.
- Coverage: a 6 px grid per half; a cell counts once a card has covered its centre. The pile and character column, the rounded tube corners and the divider bar are excluded. The HUD shows floor(%), so 100% means every cell.
- Seed search (`--search N --from S`). Filter: Mochi wins, clip 15-19 s, Mochi leads at the end, the first lead change at 2-8 s, Bolt under 97%, and at most 1.4 s at 99% (the last cells are slivers by the divider; a long 99% stall reads as dead air). Good seeds at D0 1.8 (of 150): 43, 50.

## s43 (default)
- Frame 0 (sim 1.72 s): Bolt leads 36% to 18%. Mochi's first tossed card has painted a full-height diagonal and lands at 0.10 s; Bolt's rank-2 flick burst comes at 0.08.
- Lead change "MOCHI TAKES THE LEAD!" at 2.55 s (59/60 → 69/64).
- "TOO LOW! the top stays bare" at 4.15 s, with a dashed bracket on Bolt's top band.
- Mochi at 94% vs 73% at 8.4 s.
- LAST RANK! at 12.62 s. Mochi reaches 99% at 12.53 s; her last bare cells pulse gold with a target ring.
- CLEAR! at 13.73 s: a sheen sweeps her half, then sparkles. MOCHI WINS! at 14.03.
- Bolt's screen FREEZES: his live cards hang, the newest stutters 4 times (0 / 0.11 / 0.24 / 0.40 s, 3 px lower each), a cold grey wash comes up, a generic hourglass flips every 0.8 s, and FROZEN! appears at 14.28 with an annoyed stare at the hourglass.
- Clip 16.88 s (1013 frames): 2.55 s hold, then the last 0.6 s dissolves into the pre-roll (sim frames f0-36..f0-1).

## Sound
No music, no beds, no whoosh, hiss or noise; everything is synthesized in the scene.
- **snap**: a card leaving the pile, a tonal transient cluster (1.4 / 2.05 / 2.85 kHz, about 1-1.5 ms decay) plus a light 300 Hz body. Mochi's toss is 0.86x pitch, softer and rounder; Bolt's flick is crisper.
- **tap**: a soft papery knock (720-880 Hz plus a 2.4x partial and a 170 Hz body) on felt impacts above 330 px/s and wall hits above 380 px/s, louder for harder hits. Thinned to at most one per 45 ms (loudest kept).
- **pluck**: a warm additive pluck on each new rank, walking G2 major up to E4 (no high notes). The lead change is a two-note pluck.
- **CLEAR**: a rolled pluck chord G2-D3-G3-B3-D4-G4. A soft G4 pluck (392 Hz) plays at the win.
- **Freeze**: 4 stutter taps, then a soft low flump (an 80 Hz tonal fwump plus a puff low-passed at 240 Hz).
- Onsets are kept at least 12 ms apart. `master(peak_db=-6)`. No events in the last 1.0 s; the tail fades over 0.6 s.
- Mix centroid about 340 Hz, energy above 4 kHz 0.01%.

## Flags
`--seed` (43), `--label`, `--cap`, `--vote` (Team Mochi or Team Bolt? in a dark pill plus a drawn gold arrow at y 1180, x 80-880, from win+0.55 s to the dissolve; default OFF), `--search N --from S`, `--dry`, `--still --frame N` (negative = pre-roll), `--sound 0`. Tuning flags: `--g --ey --d0 --d1 --bv0 --bv1 --mk --m0 --stall`.

## Checks (encoded Full HD)
- h264 yuv420p 1080x1920, 60 fps, 1013 frames = 16.88 s.
- -14.01 LUFS, peak -5.0 dBFS, last 0.5 s at -45 dBFS.
- flash_check PASS: one isolated flash at 14.67 s (the CLEAR sheen), worst 1 s window = 1.
- Seam: pre-encode last → 0 is 0.744 against a normal step of 0.724, and the last frame is closer to 0 than to 1 (1.10), so the loop is perfect. Encoded seam 1.64 (high-motion opening, I-frame).
- Events per 5 s: 83 / 97 / 61 (241 sound events: 164 taps, 60 snaps, 15 plucks). The longest gap is 0.47 s.
- Safe zone: caption y 196-270, ladder at y 352, monitor y 372-1346 (content ≤ 0.70h), scoreboard y 1352-1534 (0.80h, as in edge_slide). Nothing important sits at x > 918; only the bezel edge and the LED are there.

Delivered <VIDEOS_DIR>\batch38\card_cascade.mp4 (no vote). Owner review: pending.

Owner review (2026-10-16): approved -> 4K (after spiral_roll2 + 2 new research videos are delivered).

Owner review (2026-10-16): APPROVED. 4K render with the vote banner OFF (the A/B control).
- Render: `NF_SCALE=2.0 --seed 43 --label ship` → output/card_cascade_ship_9x16.mp4.
- Encoded 4K: h264 yuv420p 2160x3840, 60 fps, 1013 frames = 16.883 s.
- -14.01 LUFS, peak -5.0 dBFS, last 0.5 s at -45 dBFS.
- flash_check PASS.
- Not staged yet: the copy to <VIDEOS_DIR>\Schedule\2026-10-21\3_card_cascade.mp4 was blocked by a permission check.
