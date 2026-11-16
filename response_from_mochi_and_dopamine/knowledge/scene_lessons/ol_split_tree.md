# ol_split_tree (channel 2, now "Dopamine.exe")
- New scene, character-free (docs/BRIEF_channel2.md). Owner direction 2026-10-21: "more math, splits, exponents, triangles". Skeleton: ×2 growth toward a named end state. A fractal tree: every branch splits in 2 until the crown reaches the SKY line, then every tip blooms.
- Caption (baked, `--cap`; `--cap ''` = base): `Every branch ^SPLITS^ in 2|until the tree fills the ^SKY^`. Highlights in the colour at the crown top.
- Delivered: `<VIDEOS_DIR>\DopamineExe\review\ol_split_tree.mp4` (**v3: calm bloom**, Full HD, seed 12, label fhdv4, 8.40 s). No 4K yet. Watermark "DOPAMINE.EXE". (The old `channel2` folder was retired by the owner.)
eview\ol_split_tree.mp4` (**v3: calm bloom**, Full HD, seed 12, label fhdv4, 8.40 s). No 4K yet. Watermark "DOPAMINE.EXE". (The old `channel2` folder was retired by the owner.)
- Owner review of v1 (2026-10-22): "the first 2 seconds are ok, but at 3 or 4 seconds it goes very slow and gets boring" → v2: no post-burst slowdown, 16 generations at ≤ the burst's pace, bloom at 5.99 s; colour rule (ordered height gradient, S 0.75, gold accent only for SKY/bloom); shorter Bach walk.
- Owner review of v2 (2026-10-22): "speed is ok, but the final view is too over-coloured and bright, not satisfying" → v3: only the bloom changed (timing, growth, music unchanged). Hold trimmed to 1.8 s on the coordinator's note (swipe risk).

## World (logical 1080x1920)
- Ground: one thin white line y 1196 (x 150-866, 2.5 px, 85%). SKY: a dashed GOLD line at y 372 (x 132-884) + "SKY" label and a sun icon, from frame 0; it turns solid bright gold at the bloom.
- Frame 0: a glossy white seed (r 13, soft glow hugging it) on the ground at x 508; it shrinks into the trunk root over 0.25 s after the launch.
- Tree (seeded, numpy): gen g has exactly 2^g branches, N = 16 → **65,536 tips, 131,071 branches**. Child angle = parent ± 26° (σ 15%) + a per-fork lean (σ 0.05 rad), then a 0.25 pull toward vertical. Length ratio 0.70 (gen 1) → 0.90 (gen 8+), ±5% left/right asymmetry, σ 3.5% noise. Scaled so the final crown top = the SKY line; tips x 133-887 (inside 0.10-0.84 w). Seed search `--search a,b` (pick a height-limited one: sky 372).
- **Colour rule (v2):** trunk white; every other branch coloured by the HEIGHT of its midpoint on one ordered ramp (S 0.75, V 1): coral (0) → rose (0.22) → violet (0.38) → blue (0.52) → aqua (0.66) → teal (1.0 = SKY). The warm half sits low so the first 2 s already show rose/violet/blue. Gold (hue 0.125, S 0.72) is a single small accent: the SKY line, the meter goal mark, 14 sparkles at the touch point.
- Gens ≤ 5 are glossy tubes (dark edge, core, light highlight line); width 14·0.7^g, 0.65 px for gens 10-12, 0.45 px (75%) for 13+. Growing tips are glossy spheres (r 10·0.8^g, ≥ 0.8). Newest ≤ 60 forks get a 0.16 s 4-ray glint.
- HUD: meter y 1252 "CROWN N%" (crown top / SKY height; fill = the height ramp) with the gold sun + "SKY" goal from frame 0; counter y 1478 "N BRANCHES" (true tip count = 1 + splits) + "×2" pill in the crown-top colour, "GEN g" above it, pops when log2(count) passes g − 0.5; watermark (900 right, 1338), 35%.

## Clock (clip s, v2)
- Launch 0.05 s. Nominal generation durations: burst 0.25, 0.26, 0.28, 0.31, 0.36, 0.44 (6 splits by ~1.95 s, 2 → 64), then 0.44, 0.43, 0.42, 0.41, 0.39, 0.37, 0.35, 0.33, 0.31, 0.29 and the last generation 0.30: never slower than the burst's last step, speeding up into the bloom.
- Per-branch growth-time jitter σ 10% (burst) / 12% (mid) / 12%, 8% (last two), with a catch-up of 0.3-0.85 × the branch's lag; the last generation ends exactly on the bloom.
- **0.5 s**: 2 branches (a rose V on the white trunk), CROWN 30%. **1 s**: 8 (gen 3), 45%. **2 s**: 62 (gen 6), 60%. **3 s**: 255 (gen 8), 70%. **4 s**: 1,303 (gen 10), 80%.
- ×2 pops 0.30, 0.51, 0.82, 1.13, 1.46, 1.92, 2.36, 2.80, 3.23, 3.64, 4.02, 4.40, 4.75, 5.08, 5.39, 5.68 (GEN 16): steady ~0.4 s steps, shrinking at the end.
- Splits per second: **7, 54, 193, 1,048, 7,237, 56,996** (climbing every second). Meter ~+10%/s after 2 s.
- **BLOOM 5.99 s (v3, calm)**: all 65,536 last-generation tips land, the crown touches the SKY line; every tip opens into a small soft point (r 2.6 ±20% + a 10% halo at 1.8×, alpha 0.70) in the crown's OWN height gradient at S 0.65, V 0.95 (blue → aqua → teal, 200 fine height bins: no banding), as a gentle ripple from the touch point over 0.9 s (smoothstep 0.35 s each, no overshoot). No glow, no rings, no motes. The SKY line turns solid soft gold (75%); 60 slow crown-coloured twinkles + 14 gold sparkles at the touch point through the hold. Brightness stays near the pre-bloom level: mean relative luminance 0.0635 just before the bloom (5.92 s) → 0.0654 (6.67 s) → 0.0682 (7.77 s, end of the hold). v2's bloom was a bright gold → amber → coral wall (glossy r 6 discs, ADD glow, gold rings and motes).
- Hold 1.8 s (coordinator 2026-10-22: the 3.4 s hold was a swipe risk) → 0.6 s dissolve into the seed frame. **8.40 s, 504 frames.**

## Sound
- **Melody:** J. S. Bach, Cello Suite No. 1 in G major BWV 1007, Prelude (Bach d. 1750, PD). v2 walk (`--walk 0-12,156-164`): bars 1-3 (the famous G-pedal arpeggio opening) then bars 40-41 (the D7 bariolage over the D pedal) = 80 sixteenth slots; bar 42's G-major close lands on the bloom. v1 used bars 1-4 + 37-41 (144 slots). Source: Mutopia "Mutopia-2018/01/19-517" (Schirmer 1916, A. Scherer), Public Domain; `<SOUNDFONTS_DIR>\scores\bach_cello_suite1\` + `SOURCE_mutopia_517.txt`.
- One slot per sampled event (slot 1 = the launch, then splits), greedy min gap shrinking 45% over the build: notes per second **4, 9, 11, 17, 20, 19** (the last in 0.78 s).
- Arrangement: piano plays the stream an octave up, harp at written pitch, cello + contrabass hold each half-bar's bass note, slow strings the half-bar chord; oohs G-major pad under the opening, D7 swell under bars 40-41; timpani G2 + soft boom on the launch, D2 at bar 40, a D roll into the bloom. BLOOM: rolled G-major chord (G1-D5) + strings, oohs, contrabass G1, timpani G2, boom, rising celesta + harp G-major cascade, 25 glass tinks. `--fin` 4.2.
- SFX: a woody-glassy tick per split (tonal partial on the G-major pentatonic G5-D7, rising with the generation; a 2.76× glassy partial ≤ 5.5 kHz; 0.3-0.6 kHz wooden knock; 1.5 ms soft click; no noise bed), ≥ 12 ms apart, gain ÷ √(rate/10), ×1.5 in the burst. 276 ticks, sfx ×0.30.
- `audio.master(peak_db=None, reverb=0.5)`. RMS per second: −21.5, −20.4, −19.2, −18.3, −18.7, −15.4, −13.1 (bloom), −20.9 (cadence ringing out into the fade), then silence. Late body (4.0-5.9 s) −16.7 vs bloom (6.0-7.5 s) −14.1 (+2.6 dB).

## Checks (encoded Full HD, v3)
- h264 yuv420p 1080x1920, 60 fps, 504 frames, 8.40 s. **flash_check PASS** (0 flashes, mean lum 0.018).
- Audio (muxed mp4): **−14.01 LUFS**, peak −3.91 dBFS, last 0.5 s digital silence; energy > 6 kHz 0.015%.
- Seam (check_clip, encoded): mean |Δ| **0.083**.
- Frames read from the mp4 at 5.92 s (pre-bloom), 6.67 s (bloom), 7.77 s (end of hold) and the last frame (= the seed frame); 1:1 crops of the crown before and after the bloom.
- Frames read from the mp4 at 0, 1, 2, 3, 4, 6.0 (bloom), 6.67 s and the last frame; 1:1 crops of the densest pre-bloom crown and the open canopy (v2 cut blossom highlights to 35% and the glow to 18% after the first v2 render looked pale/peachy in the centre).

## v1 (superseded 2026-10-22)
- 15 generations, build durations 0.65 → 1.40 → 0.45 s (×2 steps 2.55, 3.5, 4.7, 6.0, 7.35 s: the slowdown the owner flagged), hue by generation (S 0.85, red → magenta, crown magenta before the bloom), rainbow-by-x blossoms, bloom 12.22 s, 14.83 s. Reproduce: `--gens 15` plus v1's DUR_BUILD and colours (not kept as flags).

## Flags
`--seed (12) --label --cap --still --frame a,b --dry --search a,b --sound 0 --sfx (0.30) --fin (4.2) --gb (1.0) --walk (0-12,156-164) --hold (1.8)`. Tree: `--gens (16) --th (26) --k (0.25) --r0 (0.70) --r1 (0.90) --asym (0.05)`. Changing a tree flag changes the crown: re-run `--search` and check the fit.

Owner review 5 (2026-10-22): "speed is ok but the final view is too over-coloured and bright, not satisfying" -> v3: calmer bloom in the crown gradient, gold as a single accent.

Owner review 6 (2026-10-23): "idk, I am not the target audience, you decide" -> SHIP (x2 skeleton, calm finale): Dopamine.exe Oct 29.
