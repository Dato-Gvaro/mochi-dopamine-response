# ol_blade_split (DopamineEXE, channel 2)
- Batch 54 (docs/BRIEF_batch54.md), the owner's idea: "balls getting tiny and more in number, in some action". Rule: **every blade a ball lands on cuts it into 2 half-volume balls** (radius / 2^(1/3)); 15 rows of blades, each row finer (blade pitch = the arriving ball's diameter, so nothing slips through uncut); after 15 cuts the pieces are sand-sized grains that pour into the glass and fill it to the FULL line.
- Caption (baked, `--cap`; `--cap ''` = base): `Every cut ^SPLITS^ it in 2…|until it pours like ~WATER~` (`^x^` = current hue, `~x~` = gold).
- Delivered: `<VIDEOS_DIR>\DopamineExe\review\ol_blade_split.mp4` (**v4: 13 rows / 8,192 grains, short drop into the glass**, Full HD, seed 7, label fhd6, **18.68 s, 1121 frames**). Archive: `archive\ol_blade_split_v3.mp4` (v3, 17.90 s), `archive\ol_blade_split_v2sfx.mp4`, `archive\ol_blade_split_v2.mp4`, `archive\ol_blade_split_v1.mp4`; the v1 scene file is at scratchpad `bD55/ol_blade_split_v1.py`.
- **Shipped 4K (batch60, v4 approved "ok"):** `<VIDEOS_DIR>\DopamineExe\schedule\2026-11-07\1_ol_blade_split.mp4` (`NF_SCALE=2.0 python scenes/ol_blade_split.py --label ship`, defaults = v4, seed 7), 04:00 local Nov 8 (= 19:00 US East Nov 7). FHD review copy archived as `archive\ol_blade_split_fhd.mp4`.
- 4K checks: h264 High yuv420p 2160x3840, 60 fps, 1121 frames, 18.68 s; **flash_check PASS** (0, mean lum 0.0097); **-14.00 LUFS**, peak -5.70 dBFS, last 0.5 s digital silence. Events json + audio wav bit-identical to the reviewed fhd6. Frames read at 0.5, 9, 15.0, 16.45 (FULL), 18.6 s = the FHD timeline.

## v4 (2026-10-29, batch58): more grains, a short drop into the glass
- Owner on v3: "more balls, or make the final drop shorter: that much space at the end makes it look like we don't have many balls."
- **Both:** a 13th row of knives (`--rows 13`: 8,192 grains of 1.5 mm, was 4,096 of 1.9 mm) and the empty drop above the glass cut from +300 to **+60 px** (`--xglass 60`). The glass is computed from the grain count, so the FULL column is ~45 px taller. Cut SFX (sound v3), the v3 row spacing, the knives and the opening 0-12.5 s are unchanged (same timeline to gen 12).
- Effect: the 4,096 pieces of gen 12 rain 400+ px between rows 12 and 13 (the densest rain of the clip, 13.5-14.5 s); the grains then fall only ~100-200 px into the glass, so the pour is a dense rain (927 grains by 15 s, 7,503 by 16 s; v3 3,322 of 4,096 by 15 s) and the liquid fills a quarter of the frame at FULL (v3 ~a fifth).
- Music: same Mendelssohn span (score beats 12-69, bar 23 cadence = FULL) at **209.8 bpm** (v3 220.4): the extra row adds 0.8 s, so the tempo is 5% slower.
- v3 = `--rows 12 --xglass 300`.

### Timeline v4 (clip s, seed 7)
- New generations at 1.07, 2.30, 3.32, 4.33, 5.22, 5.96, 6.94, 7.96, 9.10, 10.19, 11.36, 12.46, **13.51** (SAND 1.5 mm).
- Cuts/s 1, 2, 2, 6, 8, 22, 42, 66, 96, 178, 316, 613, 1,047, 1,912, 3,105, 775 (climbing to the last row). Balls at s ... 1,353 (12), 2,400, 4,312, 7,417, 8,192.
- First grain in the glass 14.29 s; **FULL 16.38 s** on the cadence; hold 1.7 s + 0.6 s dissolve = 18.68 s.
- SFX events/s 3, 2, 7, 9, 15, 26, 28, 36, 43, 47, 50, 58, 64, 67, 60, 57, 30 (FULL bells), 604 events.

### Checks v4 (encoded Full HD, fhd6)
- h264 High yuv420p 1080x1920, 60 fps, 1121 frames, 18.68 s. **flash_check PASS** (0, mean lum 0.010).
- **-14.00 LUFS**, peak -5.70 dBFS, last 0.5 s digital silence. RMS/s -18.9, -19.4, -17.1, -17.2, -17.3, -17.1, -17.8, -17.7, -17.7, -18.0, -17.5, -17.5, -17.2, -16.8, -18.0, -18.5, -15.9 (FULL), -16.7, silence. Seam mean |delta| 0.318.
- Frames read from the mp4 at 0.5, 5.5, 9, 13.8, 15.0, 16.45 (FULL), 18.6 s (dissolve); 1:1 crop at 15.0 s (the grain rain pouring into the glass past the FULL line). Fast stills at 0, 10, 13, 14.5, 15.3, 16.4 s.

### Doubts v4
- 18.7 s is long for the channel's 9-13 s rewatch sweet spot; it follows the owner's "slower" v3 note.
- At FULL the top ~60% of the frame is the (now empty) last two knife rows; the liquid is a quarter of the frame. A closer end camera would crop the glass's sides.
- Titles changed: 13 rows, 8,192 pieces.

### Upload draft v4
- Titles: "Every cut splits it in 2… until it pours like WATER 💧 #satisfying #physics #shorts" · "1 ball, 13 rows of knives, 8,192 pieces 🌈 #satisfying #physics #shorts" · "Will 1 ball fill the whole glass? 💧 #satisfying #physics #shorts".
- Pinned comment: "one 3 cm ball got cut 13 times into 8,192 grains and filled the glass right to the line… did you think it would make it?"

## v3 (2026-10-29): the second half slowed (the tiny-ball rain lasts longer)
- Owner on v2+sound v3: "good, but after half the whole thing goes too fast; let people watch those tiny balls dropping a little longer, maybe they like it."
- **Rows further apart, not slow motion** (gravity stays 1100 px/s²; a time-warp would make the balls float): from row 5 the free fall between rows grows by up to **+400 px** (ramp over rows 5-7, `--xfall 400 --xk0 5 --xkr 3`), and the last row hangs **+300 px** higher above the glass (`--xglass 300`). Rows 0-5, the cut, the knives, the sound design and the opening 0-5 s are unchanged (frame 0 identical).
- Generation spacing from gen 7 on ~1.0-1.15 s (v2 0.5-0.6 s); 7 s -> FULL lasts 8.6 s (v2 5.2 s) = **1.65x**. The pieces now visibly RAIN 400+ px between rows.
- **Camera** (`--camv 3`): the v2 camera aimed at the next row's tips, which with the wider gaps showed empty air (stills 8-11 s were black). Now, blended in over 4.6-5.8 s (`--camb0/--camb1`), it frames the median y of every piece alive (in flight, on a knife, grains falling) at 40% of the window; Gaussian 0.4 s. Scroll 90 -> 450 px/s, settles on the glass at ~14 s. Zoom as v2.
- **Music**: the same Mendelssohn, now score beats 12-**69**: bar 4 -> the next V-I (E, E7 -> A) at **bar 23** = FULL; 220.4 bpm (v2 223). bar 19's A-major (v2's FULL) now passes mid-rain at ~12.1 s as part of the phrase.
- **Pour plips** sampled >= 12 ms + 0-10 ms (v2/v3-sound: 16 + 0-20 ms) so the SFX rate doesn't dip when the pour plays alone (`--pgap/--pgapx`).
- v2 picture = `--xfall 0 --xglass 0 --camv 2 --sb1 57 --pgap 0.016 --pgapx 0.020`.

### Timeline v3 (clip s, seed 7)
- New generations at 1.07, 2.30, 3.32, 4.33, 5.22, 5.96, 6.94, 7.96, 9.10, 10.19, 11.36, 12.46 s (SAND).
- Cuts/s 1, 2, 2, 6, 8, 22, 42, 66, 96, 178, 316, 613, 1,047, 1,476, 220 (still climbing into the pour). Balls at s ... 84 (7), 150, 246, 424, 740, 1,353 (12), 2,400, 3,876, 4,096.
- First grain in the glass 13.41 s; 3,322 by 15 s; **FULL 15.60 s** on the cadence; hold 1.7 s + 0.6 s dissolve = 17.90 s.
- SFX events/s 3, 2, 7, 9, 15, 26, 24, 35, 40, 47, 51, 58, 66, 62, 56, 35 (pour ends 15.6) + FULL bells; 542 events. The rate saturates at the 12 ms thinning cap (~55-66/s) from 11 s; it does not fall before FULL except the last 0.6 s of the pour.

### Checks v3 (encoded Full HD, fhd5)
- h264 High yuv420p 1080x1920, 60 fps, 1074 frames, 17.90 s. **flash_check PASS** (0, mean lum 0.009).
- **-14.01 LUFS**, peak -5.51 dBFS, last 0.5 s digital silence. RMS/s -18.7, -19.3, -16.8, -17.0, -17.6, -16.4, -17.6, -18.3, -18.1, -17.8, -17.3, -17.2, -17.3, -18.0, -18.5, -16.9, -15.3 (FULL), silence. Seam mean |delta| 0.319.
- Frames read from the mp4 at 0.5, 4.6, 5.3 (camera blend), 7.0, 9.5, 12.0, 13.6, 14.6, 15.7 (FULL), 17.5 (dissolve); 1:1 crop at 11.0 s (the rain falling onto a fine row). Fast stills every 0.67 s over 5-12.7 s.

### Doubts v3
- 13.4-15.6 s the pour itself is ~2.2 s (v2 2.1 s): the RAIN above it is what got longer; the grains still arrive within ~1.5 s of each other (their birth spread). Longer would need a slower honest mechanism (e.g. flinging pieces up).
- Behind the camera's follow the upper rows scroll away faster than v2 (up to 450 px/s at 12-13 s).
- Unheard by me: the music now runs 4 bars further (bars 19-23) at the same tempo.

## v2 + SOUND v3 (2026-10-28, batch 56): cut and round-off SFX
- Owner on v2: "the split and the ball need some sound; it goes kind of without sound effects." The picture is unchanged (the reviewed v2 video, re-muxed: `--video output/ol_blade_split_fhd3_9x16.mp4 --label fhd4`). Delivered `<VIDEOS_DIR>\DopamineExe\review\ol_blade_split.mp4`; the v2 file archived as `archive\ol_blade_split_v2.mp4`.
- **Why v2 sounded empty (measured stems):** v2's per-cut shing was pitched INTO the score (blended with the music) and its gain was divided by sqrt(RAW cuts/s / 6) = /17 at 1,869 cuts/s. SFX stem -31.2 LUFS vs music -22.6 (8.7 dB under); per second it fell to -44..-48 dB from 7 s on.
- **v3 sound (`--sfxv 3`, default; `--sfxv 2` = v2):** per cut
  - a **nick** when the edge touches the ball's bottom (gens 0-3 only, the slow big cuts);
  - the **shink** at the cut-through (contact + 72% of the slice): a sine-grain scrape running up to it (0.64 s on the big ball, 0.04 s on small ones), then a click + ringing steel tone (bar partials 1/2.76/5.40 + a slow beat), on a chord tone, pitched DOWN as the balls shrink (E6 on the big ball -> ~B4 at row 12);
  - a soft liquid **blup** per half as it pulls round (a rising-pitch sine, deeper for bigger halves; 2 per cut 18 ms apart, panned to each side; 1 per cut when dense).
  - Priority thinning: FULL bells/last grain > the pour's plips (v2 rule) > cut sounds; every onset >= 12 ms apart (+0-16 ms jitter when > 40 candidates/s). Gain / sqrt(KEPT events/s / 6).
- Stems now: SFX -23.3 LUFS vs music -22.6 (to FULL: -23.1 vs -23.6, equal level). SFX events/s 3, 2, 7, 9, 15, 27, 29, 42, 54, 64, 64, 52 (FULL bells) = climbing; 384 events (v2 301).
- Sync measured on the muxed file (>2 kHz envelope): biggest rises at 0.79 s and 2.10 s = the first two shinks (events 0.792 / 2.102); frames 47 (V fully open) and 59-66 (halves rounding) match.

### Checks (encoded Full HD, fhd4)
- h264 yuv420p 1080x1920, 60 fps, 869 frames, 14.48 s (video stream = fhd3). **flash_check PASS**.
- **-14.01 LUFS**, peak -5.40 dBFS, last 0.5 s digital silence. RMS/s (audio test) -19.6, -19.8, -16.7, -16.9, -17.0, -16.5, -17.8, -18.3, -17.5, -17.5, -17.8, -19.4, -15.1 (FULL), -18.8, silence. Seam 0.319.
- Spectrum: 60% 200-1000 Hz, 31% 1-3 kHz, 4.0% 3-6 kHz, 0.23% > 6 kHz (v2: 0.37% > 6 kHz): no hiss.

### Doubts (sound v3)
- Unheard by me. The first 2 s carry only the big cut (nick 0.07 s, scrape -> shink 0.79 s, blups 0.99 s) over the music; if the scrape reads as hiss, lower its grain count in `shink_wave`.
- "Pitched down as the balls get smaller" is per the brief; it is the opposite of real physics (small things ring higher). The blups follow size (smaller = higher).

## v2 (2026-10-28, batch 55): slower, cut from BELOW
- Owner review of v1: "interesting, but it happens too fast, and splitting from above on the spike doesn't look natural. Maybe split a different way, from the bottom?"
- **The cut:** the knives stand EDGE UP, seen edge-on (a straight steel shank, a short bevel, a honed edge glint; width 0.08 d, height d + 6). A ball sinks onto the edge: the edge enters its BOTTOM (a bright nick at the edge), the cut climbs through it while the two halves peel apart from below (a V opening under the edge: each half shears outward up to 0.24 rad, still joined above the edge; a light fresh cut face on each), and once cut through (72% of the slice) the halves slide off either side of the knife and pull round into 2 smaller balls with a liquid stretch, then wobble round in flight (~0.3 s). Volume still conserved (r / 2^(1/3)).
- **Slower:** 12 rows (v1 15), wider spaced (each row: d for the cut + a 1.1 d + 45 px free fall). Big ball r 44 (v1 34), "3.0 cm" so 12 cuts end at the same 1.9 mm SAND. Slice time 1.0 s x (r/R0)^0.55 x U(0.75, 1.35) (v1 0.42 s x ^0.3 x U(0.5, 1.8)). Halves leave at vx +-U(50,130) (+ 0.25 parent vx), vy U(-30, 110).
- **Camera:** the tower is now taller than the screen (rows y 404-1724, glass rim 1763, FULL line 1852, floor 2013 world px). It follows the cascade's FRONT (the newest generation's row at 40% of the window), zoomed x1.9 on the first cut and opening out by 1 + 0.9 e^(-gen/3.5), Gaussian-smoothed (0.4 s); it ends framed on the glass. The top opening in the frame fades as it scrolls.
- 4,096 grains (v1 32,768) of r 2.75 px fill the glass to the computed FULL line.
- **Music:** same piece, score beats **12-57**: bar 4 (the theme running from frame 0) to the A-major cadence at bar 19 (bass E -> A) = FULL. **223 bpm** (= the MIDI's own tempo; v1 193.6). `--sb0/--sb1` flags.

### Timeline v2 (clip s, seed 7)
- 0.08 s: the big ball lands on the middle knife; cut through by ~0.8 s, halves part ~1.0 s.
- New generations at 1.07, 2.30, 3.32, 4.33, 5.22, 5.96, 6.69, 7.29, 7.87, 8.38, 8.96, 9.46 s (SAND).
- Cuts/s 1, 2, 2, 6, 8, 22, 54, 134, 436, 1,341, 1,869, 220. Balls at s 1, 2, 4, 6, 12, 20, 42, 96, 230, 666, 2,007, 3,876, 4,096.
- First grain in the glass 10.10 s; 1,215 by 11 s; **FULL 12.19 s** on the cadence; hold 1.7 s, 0.6 s dissolve. 14.48 s.

### Checks v2 (encoded Full HD, fhd3)
- h264 yuv420p 1080x1920, 60 fps, 869 frames, 14.48 s. **flash_check PASS**.
- **-14.01 LUFS**, peak -3.68 dBFS, last 0.5 s digital silence. RMS/s -18.8, -18.9, -19.6, -18.4, -18.3, -18.5, -18.3, -19.1, -18.3, -18.3, -17.2, -18.5, -13.4 (FULL), -17.1, silence.
- Seam mean |delta| 0.319.
- Frames read from the mp4 at 0, 0.6, 1.3, 3, 5, 7.5, 10.5, 12.25 s; 1:1 crops at 0.7 s (the V opening under the edge), 1.05 s (two balls on either side of the knife) and 11.0 s (the grain rain over the glass). Cut stills at 0.6-1.7 s.

### Doubts v2
- 1.5-4 s is calm (2-12 balls, big cuts): that IS the slower pace asked for; the counter and SIZE readout tick on every generation.
- After ~7 s the camera is near x1.1-1.2, so balls near the side walls are briefly out of view.
- The cut is drawn (a shear of the 2 halves under the edge), not a simulated deformation; the halves' liquid stretch is a visual.
- The pour still reads as a rainbow grain rain into a rising level (not a single tap stream).

### Flags v2
`--r0 (44) --rows (12) --t0 (1.0) --texp (0.55) --tv0/--tv1 (0.75/1.35) --sep0/--sep1 (50/130) --vy0/--vy1 (-30/110) --fall0/--fall1 (1.1/45) --phi (0.24) --zoom (1.9) --zk (3.5) --foc (0.40) --camsig (0.40) --sb0/--sb1 (12/57)`. v1 = run the scratchpad v1 file.

### Upload draft v2
- Titles: "Every cut splits it in 2… until it pours like WATER 💧 #satisfying #physics #shorts" · "1 ball, 12 rows of knives, 4,096 pieces 🌈 #satisfying #physics #shorts" · "Will 1 ball fill the whole glass? 💧 #satisfying #physics #shorts".
- Pinned comment: "one 3 cm ball got cut 12 times and filled the glass right to the line… did you think it would make it?"

## v1 notes (below)
## World (logical 1080x1920)
- Arena x 150-866 (inside 0.10-0.84 w), y 318-1226, thin white line, an opening at the top centre the big ball drops through.
- Big ball r 34 (= "6.0 cm"). 15 blade rows from y 404 to 884: row k blade pitch 0.97 x the gen-k diameter, blade height 0.5 d + 2, width 0.1 d (steel gradient + bright edge; rows 9+ are hairlines). Row 0 has a blade exactly in the middle. Row spacing 1.34 d + 4, so the rows get denser toward the bottom (a visibly finer comb).
- Glass = the bottom of the arena (rim lips at y 914, graduation ticks, faint tint + gloss streak). **FULL line y 1022 is computed**: 32,768 grains of r 34/32 in a hex packing across the glass (98 rows).
- Colour: each ball carries an interval of the family tree (left half / right half), hue = its centre on one ordered sweep coral -> amber -> gold-green -> teal -> sky -> violet (S ~0.70). So the colours sort left -> right and the liquid is a rainbow sand.
- Camera: ONE smooth zoom-out, x2 on the top rows at frame 0 -> x1 between 0.55 and 3.6 s (the big ball reads big; the glass enters the view ~3.3 s). Static after that.
- HUD: meter y 1290 = log2(balls)/15 with 15 rungs (one per row), "SIZE 6.0 cm" -> "1.9 mm" (smallest piece that exists; real size = 6 cm x 2^(-k/3)), gold SAND goal from frame 0. Counter y 1488 "BALLS" + "×2" pill (pops when each new generation first appears). Watermark DOPAMINE.EXE 35%.

## Physics (scenes/ol_blade_split.py `simulate`, seeded, exact, event-driven)
- Every ball flies an analytic parabola (g 1100 px/s², elastic side walls) until its bottom reaches its row's blade tips. The blade nearest its centre cuts it: the ball slides onto the edge while the blade passes through (slice time 0.42 s x (r/R0)^0.3 x U(0.5, 1.8); the big ball exactly 0.42 s), drawn as 2 halves opening and rounding off. The halves leave either side of the blade: vx ±U(40,140) + 0.25 x parent vx, vy 0.18 x impact speed + U(-80,160) (some get flung up, so the generations overlap and the pour spreads out).
- Grains (gen 15) fall into the glass; the surface rises level (water): each grain takes the nearest free slot in the lowest unfilled hex row when it reaches the current level. Volume (drawn area) is conserved exactly.
- No ball-ball collisions in flight (the lineages are spatially apart; at the small sizes overlap is invisible).

## Timeline (clip s, seed 7)
- Frame 0 = 0.08 s before the first contact: the big green ball half through the top opening, x2 zoom, 6 rows of blades in view. **0.08 s** it lands on the middle blade (spark), the halves open by 0.25 s.
- Balls at s: 1, 4, 12, 62, 326, 2,477, 16,286, 31,240, 32,768. Cuts/s: 3, 8, 50, 264, 2,151, 13,809, 14,954, 1,528.
- New generations at 0.49, 1.01, 1.41, 1.87, 2.26, 2.55, 2.88, 3.11, 3.35, 3.54, 3.85, 4.09, 4.28, 4.51, 4.65 s (sand = 1.9 mm).
- First grain in the glass 5.28 s; the rainbow rain pours 5.5-8 s (15,448 grains by 7 s, 32,391 by 8 s); the last grain (gold ring) drips in alone.
- **8.45 s FULL** on the cadence: FULL line turns solid gold and pops, a gold shimmer sweeps the surface, 9 sparkles, counter 32,768 gold. Hold 1.7 s, 0.6 s dissolve into the pre-roll (the ball dropping in). 10.75 s.

## Sound
- **Music played as music:** F. Mendelssohn, Symphony No. 4 "Italian" Op. 90, 1st mvt Allegro vivace (1833; d. 1847, PD), bars 1-10 (score beats 3-30): the winds' repeated A-major chords from frame 0, the violins' famous theme from bar 3, the phrase landing on A major at bar 10's downbeat = FULL. One steady tempo, **193.6 bpm** (quarter; the MIDI's 222 x 0.87). Source: midiworld.com `ital-1.mid`, saved at `<SOUNDFONTS_DIR>\scores\mendelssohn_italian1\` + SOURCE.txt. Not on any used list; not kid-coded; not banned.
- Arrangement (lib/orchestra): flute/clarinet/bassoon/horns on the repeated chords, violin + strings on the theme, 2nd violins, viola, cello, contrabass; timpani roll into the cadence; cadence = A-major tutti held 2 s + harp roll, celesta glint, timpani A.
- SFX (x0.55, tonal, no noise): per cut a steel "shing" (inharmonic bell partials < 5.5 kHz + a soft round thock below) pitched to a note the score sounds there, rising ~2 semitones per generation; sampled >= 12 ms apart (+0-16 ms jitter), gain / sqrt(rate/6). Per landing grain a water "plip" (sine with a small rising glide, 90 ms) on chord tones G5-C7, sampled >= 16 ms. Last grain: plip + tink; FULL: 9 tinks on the sparkles.
- `level_bed` (+4 dB crescendo, cadence +6 dB), `audio.master(peak_db=None, reverb=0.5)`, last 0.6 s digital silence; own mux without `-shortest`.

## Checks (encoded Full HD)
- h264 yuv420p 1080x1920, 60 fps, 645 frames, 10.75 s. **flash_check PASS** (0 failing seconds).
- **-14.01 LUFS**, peak -3.06 dBFS, last 0.5 s digital silence. RMS/s (audio test): -17.3, -18.3, -19.2, -20.2, -18.7, -19.7, -18.4, -18.3, -14.5 (FULL), -14.5. SFX events/s: 2, 4, 16, 38, 47, 69, 85, 70, 24.
- Seam (check_clip): mean |Δ| **0.340**.
- Frames read from the mp4 at 0, 0.25, 1, 2, 4, 5.5, 6.5, 7.5, 8.3, 8.6, 9.5, 10.7 s; 1:1 crop of the pour at 6.5 s (fine comb rows, the rainbow grain rain, FULL line, the first liquid layer).

## Doubts
- The pour reads as a dense rainbow rain/mist falling into a rising liquid, not a single narrow stream from a tap. The surface does level like water.
- 2-4 s: the glass (bottom third) is empty and dark while the cascade works through the middle rows.
- Length 10.75 s (shorter than 13-18 s): the cascade is honest gravity; slower would mean floaty balls.
- During the 0.6 s dissolve the counter ghosts (32,768 fading under 1), like ol_brick_breakout.
- The cut count is exact (2^15) but the grains in the glass are drawn at 1 px at Full HD.

## Flags
`--seed (7) --label --cap --still --frame a,b --dry --audio --sound 0 --sfx (0.55) --fin (2.0)`. Physics: `--r0 (34) --rows (15) --g (1100) --t0 (0.42) --texp (0.3) --tv0/--tv1 (0.5/1.8) --sep0/--sep1 (40/140) --vy0/--vy1 (-80/160)`. Camera `--zoom (2.0) --zt0 (0.55) --zt1 (3.6)`. Clip `--lead (0.08) --hold (1.7)`. Sim < 1 s.

## Upload draft
- Titles: "Every cut splits it in 2… until it pours like WATER 💧 #satisfying #physics #shorts" · "1 ball, 15 rows of blades, 32,768 pieces 🌈 #satisfying #physics #shorts" · "Will 1 ball fill the whole glass? 💧 #satisfying #physics #shorts".
- Pinned comment: "one 6 cm ball turned into 32,768 grains of sand and filled the glass exactly to the line… did you think it would make it?"
