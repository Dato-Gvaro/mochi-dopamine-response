# ol_lightning_strike (DopamineEXE, batch62 #6)

## v1 (2026-10-31)
A slow-motion stepped leader grows down from a violet cloud base toward 5 numbered rods, forking into hundreds of branches; the deepest tip (gold dot) changes branch as they race. Near the ground upward streamers rise from rods 3 and 4. The leader meets rod 3's streamer: that one path lights up as a white-gold channel with a violet glow (the return stroke), every other branch fades, "ROD 3 / one branch struck / ≈30,000 A (typical)".

- Caption (baked; `--cap ''` = base): `The lightning keeps ^SPLITTING^…|only ~ONE~ branch hits the ground`. True: the branch count climbs every step; exactly one path connects.
- **Coordinator check (photosensitivity):** no full-frame white; the strike is a bright channel (core 3-7.5 px + glow ≤30 px) on black for ~0.3 s, then a dimmer afterglow. flash_check: see Checks. No swap to glass_stairs needed.

## Model (dielectric-breakdown model, Niemeyer, Pietronero & Wiesmann, PRL 52, 1033 (1984))
- Grid 4 px (216 × 217 cells) from the cloud base y 400 to the ground y 1268. Cloud row φ = 1, ground row + 5 rods (80 px, at x 151 / 329 / 508 / 686 / 864) φ = 0, sides Neumann. The leader channel is held at φ = 1.
- Each step: one empty cell next to the leader grows with probability ∝ (1 − φ)^η, **η 1.2**; Laplace re-solved by red-black SOR (ω 1.85; 300 sweeps at start, 6 warm-start sweeps per step).
- Streamers: the same growth (∝ φ^η) from a rod's cluster, every 2nd step, once φ next to it passes **0.10**. Contact = the first leader cell touching a streamer/rod (or the ground row; this seed hits a streamer).
- Seed **3** (leader starts 60-110 px off-centre, side by seed): 1,720 steps, 1,817 cells, 458 branch tips; streamers from rods 3 and 4; the deepest tip at the halfway beat was over rod 4 (the early favourite); **rod 3 is struck**. Seed scan (η 1.2): 1 rod 2 (fav 2), 2 rod 4 (fav 4), **3 rod 3 (fav 4)**, 4 rod 2 (fav 2), 5 rod 3 (fav 2, 1 streamer), 6 rod 2 (fav 2), 7 rod 3 (fav 3), 8 rod 2 (fav 3). η 1.6 gave one trunk with stubs (no visible race); η 1.0 was bushier but always hit the rod under the start.
- Branch counter = live count of leader tips (cells with no leader child) on screen.

## Scale and clock
- Frame 0 = the leader 25% down; that gap is defined as 1,000 m → 0.646 px/m (cloud base ≈1,340 m). The leader meets the streamer at 195 m (the streamer bridges the rest; the meter then reads 0).
- Stepped display: all growth between two beats appears as one 0.1 s burst on the beat (real leaders step ~10-200 m in ~1 µs, pause 20-50 µs); 18 steps of ≈45 m.
- SLOW-MO computed from a typical average leader speed **2×10^5 m/s** (Rakov & Uman, *Lightning: Physics and Effects*): 805 m in 4.0 ms shown over 7.2 s → **×1,800** (rounded); ms clock 0 → 4.00 ms. "≈30,000 A (typical)" = the median first-stroke peak current of negative cloud-to-ground lightning (Berger et al. 1975, ~30 kA), labelled typical.

## Timeline (Night on Bald Mountain at 150 bpm, a step per beat)
- Frame 0: 72 branches, step bursts at 0.10 + 0.4 k s; 3.3 s ~357, the fan ~650 px wide; 6.6 s streamers rise from rods 3 and 4; **7.30 s strike** (step 18): channel + D-minor chord; 7.35 "ROD 3"; branches fade by 8.0; afterglow fades 9.5-10.3; dissolve 10.4-11.0 into frame 0. **11.0 s, 660 frames.**

## Screen
- Cloud base band (dark violet scallops) y 300-410; leader hue by depth violet → blue → cyan (S 0.75); live tips white, deepest tip gold.
- Ground y 1268 with rods; rod number discs on the ground band (struck rod gold). Meter y 1372: GAP TO GROUND n m (1,000 m → STRIKE). Counter y 1530 BRANCHES + STEP n pill. Top right: SLOW-MO ×1,800, ms clock, "LEADER ≈200 km/s". Banner on the side away from the channel. Watermark 35%. Side safe zone: rods 0.14-0.80w, text ≤ 884.

## Sound
- M. Mussorgsky, Night on Bald Mountain (1867/1886, PD), Mutopia piano arrangement by K. Chernov (d. 1937; engraving CC BY 3.0, PD notes only), `<SOUNDFONTS_DIR>\scores\mussorgsky_bald_mountain\SOURCE.txt`, read at runtime. The opening whirl over the A pedal (beats 0-17) an octave down at 150 bpm (piano + tremolo strings pedal + contrabass/tuba/piano bass), a timpani roll into the strike; the strike resolves A → a rich D-minor chord (brass, strings, organ, timpani, low boom, harp). Replaces the brief's Bach "Little" Fugue BWV 578 (not on Mutopia; no PD MIDI/MusicXML reachable).
- SFX: a soft pitched crackle per fork (A / B♭ / D / E, ≥14 ms apart, growing), a warm tonal "zap" chord on the strike. No thunder (at ×1,800 the thunder would arrive hours later on screen); the low boom is a musical hit.

## Checks (encoded mp4, output/ol_lightning_strike_fhd_9x16.mp4)
- h264 yuv420p 1080x1920 60 fps, 660 frames, 11.00 s; **-14.00 LUFS**, peak -5.59 dBFS, last 0.5 s digital silence; **flash_check PASS (0 flashes, worst 1 s = 0, mean lum 0.006)**; seam mean |Δ| 0.220.
- Stills read at 0, 0.15, 1.5, 3.3, 5.0, 6.7, 7.25, 7.32, 7.45, 8.0, 9.5, 10.7 s; 1:1 at 7.33 s (strike) and the banner at 8.67 s.

## Flags
`--seed` (3), `--eta` (1.2), `--th` (0.10), `--scan a,b`, `--resim`, `--label`, `--cap`, `--still --frame`, `--dry`, `--audio`, `--sfx`, `--sound 0`.

## Upload draft
- `The lightning keeps splitting… only one branch hits the ground ⚡ #satisfying #physics #shorts`
- `1 cloud, 5 rods: which one gets struck? ⚡ #satisfying #physics #shorts`
- `458 branches raced down. Only one touched the ground ⚡ #satisfying #physics #shorts`
- Pinned: `the branch over rod 4 led most of the way and still lost. which one did you pick?`
- Lead by step (rod under the deepest tip, beats 0-18): 4 4 4 3 3 4 3 3 4 4 4 4 4 4 4 3 3 3 3 (rod 4 leads 12 of 19 steps; 5 lead changes).

## Shipped 4K (2026-11-01)
- `NF_SCALE=2.0 python scenes/ol_lightning_strike.py --label k4ship` (defaults) → `<VIDEOS_DIR>\DopamineExe\schedule\2026-11-11\1_ol_lightning_strike.mp4`. h264 yuv420p 2160x3840 @60, 660 frames 11.00 s; -14.00 LUFS, peak -5.59 dBFS, last 0.5 s silent; flash PASS (0); seam 0.12; events json bit-identical to fhd. Frames read at 1.5 / 8.67 s. FHD review file → `archive\ol_lightning_strike_fhd.mp4`.
