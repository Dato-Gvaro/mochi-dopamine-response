# ol_metronome_sync (DopamineEXE, batch64 #1)

## v1 (2026-11-01)
144 metronomes on ONE rolling shelf (12 boards × 12, two rollers on a floor line), every one at its own tempo: 112 → 128 ticks/min by position (hue = tempo, red top-left → violet bottom-right, S 0.75). Only the shelf couples them. Under TIME-LAPSE ×2 they fall into step band by band; the last red holdout joins at 5.46 s (144/144, SYNC 100%, "all 144 at 127 /min"); Haydn's Clock theme plays over the next 8 unison ticks, the finale chord lands on tick 8 (7.48 s) and the clip eases back to REAL TIME for the held unison. Dissolve into frame 0. **9.98 s, 599 frames.**

- Caption (baked; `--cap ''` = base): `Every metronome ticks at its ^OWN^ tempo…|until all 144 tick as ~ONE~`. True: natural tempos 112-128 all differ; all 144 end in sync (within ±20° of the beat, then converging to <12° by the finale chord).
- Effect chip at the payoff: "Huygens synchronization (1665)". None of MathMotion's on-screen lines or board look.

## Model (`simulate`, RK4 dt 1/600 s, ~1 s CPU)
- Pantaleone 2002 (Am. J. Phys. 70, 992): θ_i'' = −ω_i² sin θ_i − ε ω_i ((θ_i/θ0)² − 1) θ_i' − cos θ_i X''; shelf X'' (1 − b Σcos²θ) = −b Σ(cos θ_i A_i − sin θ_i θ_i'²), b = B/N. Free-rolling shelf, total momentum 0 (it rocks in place, sway ≤16 px).
- **B 0.45** (pendulums ~45% of the moving mass: a light shelf), **ε 0.15**, **θ0 0.55** (swing ≈ 1.1 rad), seed **9** (random phases).
- Probed: small swings (θ0 ≤ 0.45) or base damping never sync (in-phase needs the pendulum's amplitude-dependent frequency); B 0.5 locks at ~134/min (above every natural tempo: confusing) → kept 0.45 (locks at 127/min). Seeds 3/9/12 lock fastest.
- IN SYNC: phase φ = atan2(−θ'/ω, θ); gap to the mean phase, averaged over ~one swing (EMA τ 0.5 s real); in when < 20°, out when > 24°. Lock = first time after which all 144 stay in: real 11.92 s. Max phase gap at the finale chord (real 16 s) < 12°; <8° by real 18 s.
- Brief deviation: the meter is SYNC % = IN SYNC / 144 (not Kuramoto r): r ran far ahead of the ±20° count (r 0.78 vs 53/144), which read as a contradiction.
- Truth over brief: the holdouts are the SLOWEST (red, top row; the shelf locks near the fast end, 127/min), not violet. LAST 4 → LAST 1 (metronome #3, 113 /min) at ~5.0-5.45 s.

## Timeline (screen)
- 0 s: real 1.0 s, SYNC 19% (27/144), shelf rocking, ×2 time-lapse · 2 s 45 · 3.5 s 71 · 4.4 s 117 (+32) · 5.0 s 140 · **5.46 s 144/144** (gold, meter ring, "all 144 at 127 /min") · 5.60 theme · **7.48 finale chord**, ease to REAL TIME (0.5 s) · 9.38-9.98 dissolve.
- "+k" pill when the in-sync count rises ≥6 within 0.5 s (true jumps).

## Sound
- Haydn, Symphony No. 101 "The Clock", II. Andante (1793-94, PD). Theme read from the PD engraving excerpt on Commons (`<SOUNDFONTS_DIR>\scores\haydn_clock_andante\SOURCE.txt`), hand-encoded. Before SYNC 70%: ticks only over a soft G pedal; from 70%: pizz + bassoon tick-tock (I, V7 for the 4 eighths before the lock) on every 2nd collective shelf tick (= real tempo); bar 2 (D.. B | G G) on the unison ticks, one 8th per 2 ticks; bar 3's downbeat (grace A → B, an octave down) = the finale: rich G chord + horns + harp + soft timpani. Theme an octave down (violin) + cello 2 octaves down (owner's low/mid rule).
- SFX: woody pitched ticks (G-major chord tones by row, partials < 2.5 kHz), the 144 ticks merged ≤1 per 14 ms (span 45 ms; 130 ms after the lock = one big low tock per unison beat), gain ∝ count^0.62.
- Flag for the owner: Wikipedia notes this Andante was used on a Baby Einstein DVD (as were most famous classical pieces). Not a children's tune; MFK risk judged low, but swap is easy (`music_parts`).

## Checks (encoded, output/ol_metronome_sync_fhd_9x16.mp4)
- h264 yuv420p 1080x1920 60 fps, 9.98 s; **-14.01 LUFS**, peak -5.95 dBFS, last 0.5 s digital silence; flash_check PASS (0); seam mean |Δ| 0.46 (natural per-frame motion ~2.0). Centroid 0.8 kHz pre-lock, 1.5-1.8 kHz after.
- Side safe zone: shelf x 130-886 ± 16 px sway → 0.11-0.84w.
- Stills read at 0, 1, 5, 5.6, 6.7, 7.5, 8.0, 8.7, 9.3 s; 1:1 crops at 1.0 s (dimmed out-of-sync vs bright) and 8.3 s (rods parallel).

## Flags
`--seed` (9), `--B`, `--eps`, `--th0`, `--tau0` (1.0), `--lapse` (2.0), `--label`, `--cap`, `--still --frame`, `--dry`, `--audio`, `--sfx`, `--sound 0`.

## Upload draft
- `144 metronomes at 144 different speeds… until they tick as ONE ⏱️ #satisfying #physics #shorts`
- `Every metronome has its own tempo… until the shelf syncs them ⏱️ #satisfying #physics #shorts`
- `112 to 128 beats a minute, one rolling shelf: wait for the beat ⏱️ #satisfying #physics #shorts`
- Pinned: `the slowest red one held out till the very end. did you think it would join?`

## v2 (2026-11-01, owner review: "never states what made that sync… maybe too short")
- `--v2`: the cause on screen from 0.6 s to the end, under the floor: "the shelf ^ROLLS^: every tick nudges the shelf," / "the shelf nudges ^every^ metronome" (29 px), plus gold roll arrows beside the rollers that point the way the shelf is moving (brightness ∝ shelf speed, from the sim). Huygens chip moved under it; meter moved to y 1348.
- Length 9.98 -> **13.98 s** (HOLD_AFTER 6.5, T_REAL 25): a 6.5 s real-time unison ending. Lock unchanged (real 11.92 s; all 144 stay in sync to 25 s). Music: finale chord held 3.2 s, then the Clock's own tick-tock (pizz + bassoon, I) on every unison tick in real time, a soft G (harp + strings) on the last tick; gold frame pulse on every unison tock.
- Weak: the event rate is flat (unison tocks) for the last 6 s by design (owner asked for the long ending).
- Deliverable `...\DopamineExe\review\fixes_1101\ol_metronome_sync_v2.mp4`. 13.98 s, -14.00 LUFS, peak -5.76, silent tail, flash 0, seam 0.46. v1 -> archive/ol_metronome_sync_v1.mp4.

- **STAGED 4K** (2026-11-01): `--v2 --label v2k4` at NF_SCALE 2.0 -> `<VIDEOS_DIR>\DopamineExe\schedule\2026-11-14\1_ol_metronome_sync.mp4` (events json byte-identical to the reviewed Full HD). 2160x3840 h264 yuv420p 60 fps, 839 frames, -14.00 LUFS, peak -5.76, flash 0, seam 0.27. Full HD -> archive/ol_metronome_sync_v2.mp4.
