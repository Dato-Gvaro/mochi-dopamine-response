# ol_merge_sun (Overflow Lab, channel 2)
- New scene, character-free (docs/BRIEF_channel2.md). A merge cascade, our own physical version (no fruit, no game branding): two equal bodies that touch become one bigger body, up a 10-size ladder to a STAR.
- **v2 (2026-10-22, current).** Owner review 3 of v1: "don't bounce the jar or whatever it is; also why SUN, nothing there indicates planets or cosmos". Rebuilt as SPACE: no jar, no shaker, real mutual gravity, the end state is a STAR. v1 parameters are kept at the bottom.
- Caption (baked, `--cap`; `--cap ''` = base): `Every 2 that touch ^MERGE^|until they make a ^STAR^`. MERGE in the current hue (S .65), STAR in gold.
- Delivered: `<VIDEOS_DIR>\channel2\ol_merge_sun.mp4` (Full HD, seed 17, label fhd; overwrites v1). No 4K yet.

## World (logical 1080x1920)
- Black + a very subtle starfield: 170 points, r 0.5-1.5, alpha 0.10-0.38, slow ±25% twinkle, a few warm or cool.
- Bodies: 9 sizes + the STAR. r = 17 × 2^(k/3) (volume-conserving, ×1.26 per merge; L8 = 136 px). Mass = 2^k (volume).
  - Colour = size, one ordered gradient (Colour rule): cyan 0.50 → azure → violet → magenta → rose 0.95, S 0.76 V 1. Gold is reserved for the STAR.
  - Look: lit from the upper left (light core → body colour → dark limb), soft specular, thin lit rim. Rocky sizes L0-L3 have 3 seeded crater spots; gas sizes L4+ have 3 faint tilted bands.
  - New inflow bodies fade in over 0.3 s.
- STAR: r = 1.45 × the L9 volume radius (197 px; it swells as it ignites, over 0.7 s).
  - Gold disc (pale core → gold → deep orange limb) with slow surface swirls.
  - Corona = a gradient from 0.9 r to 1.45 r plus 14 soft turning lobes inside that band (hugs the disc, nothing over empty black).
  - The rose L8 crossfades into gold over 0.5 s; 2 thin gold rings leave it. No white.
- HUD (same geometry as ol_spiral_center):
  - Size ladder y 1252 (x 186-830): dots grow with size, an unreached dot is a hue outline, a dot lights with a ring pop when first reached. A gold ★ "STAR" icon is visible from frame 0.
  - Counter y 1478: "N MERGES" + a "COMBO ×N" pill in the current hue.
  - Watermark "OVERFLOW LAB" at (900 right, 1338).

## Physics (fixed dt 1/60, 4 substeps, seeded)
- N-body gravity on all pairs, G 70,000 px³/(unit·s²), softening 12 px.
- Contacts: sequential impulses (6 iterations), restitution 0.35 above 60 px/s, friction μ 0.05, split-impulse position correction. No walls.
- View = barycentre frame: each frame a uniform boost removes the net momentum, and a uniform 5% drift pulls the barycentre back to (508, 800). No forces. Bodies beyond 900 px are dropped (a safety cut).
- Merge: same size, gap < 1.5 px → one body of the next size at the centre of mass, mean velocity, inflating in 0.12 s. COMBO = the product merges again within 0.55 s.
- STAR: no contacts. Bodies fall into it under its gravity and are swallowed once their centre is inside 0.55 r (drawn under the disc, so they sink in). Inflow stops.
- Inflow: rate = 1.0 + 1.0·e^(t/30) /s (cap 60). Sizes L0/L1 50/50. Entry ring r 390 ±10 (x 118-898). 70 px/s inward + 0.75 × the circular speed, counter-clockwise.
- Gravity keeps bodies moving, so equal sizes keep meeting: every seed tested (35/35) reaches a STAR, with no shaker.
- The cluster is a turning clump: median ~50°/s at the start, ~20°/s by 10 s. Median body speed 190 → 76 px/s, p90 ~340 → 280 px/s.
- Clip = the LAST 13 s before the STAR of one run from empty space (`--lead`, sim 77.4 → 90.4 s). No rewind, no re-seed. `--search a b` prints the STAR time, chain, bodies at frame 0, first reach of each size, merges/s and the STAR's lineage.

## Timeline (clip s; s17)
- Frame 0: 57 bodies, sizes 0-7 in 6 hues, turning. Counter 372, COMBO ×5. First merge at 0.19 s.
- 0.5 s: 379. 0.85 s: L8 (rose) is first made; its ladder dot pops. 1 s: 388. 2 s: 407.
- Merges per second: 15, 20, 10, 9, 23, 14, 18, 16, 18, 17, 23, 19, 22. Inflow 14 → 21 /s.
- Finale chain ×9, one lineage level by level: L1+L2 11.67 → L3 12.06 → L4/L5 12.07 → L6 12.26 → L7 12.61 → the second L8 → **STAR 13.00 s** (599 merges in).
- 13.0-14.3 s: 38 bodies sink in (32 in the first second). A few survivors orbit. Hold 2.9 s → 0.6 s dissolve to the pre-roll. **16.50 s, 990 frames.**

## Sound
- **Melody:** Chopin, Étude Op. 10 No. 5 "Black Key" (G-flat major), bars 1-8, both hands = 96 slots, read from the MIDI, −12 semitones.
  - Source: Mutopia "Mutopia-2007/02/11-926" (Peters/Scholtz 1900), Public Domain; `<SOUNDFONTS_DIR>\scores\chopin_black_key\` + `SOURCE_mutopia_926.txt`.
  - One slot per sampled merge, 5 → 10 notes/s. Bar 8's B-flat dominant resolves on the STAR into the G-flat chord of beat 16 + the étude's own final chord (bars 84-85, rolled). Strings, oohs, contrabass, timpani G♭ and a soft boom join there.
- SFX:
  - A tonal bloop per merge: a sine rising into its pitch, G♭ pentatonic by size, bigger = lower + longer. At least 12 ms apart, gain ÷ √(rate/8).
  - A soft bloop on a G♭-chord tone per swallowed body (at least 40 ms apart).
  - No hiss or whoosh; energy > 4.5 kHz 0.015%.
- Mastering: `audio.master(peak_db=None)`, `FIN_G` 3.1. −14.00 LUFS, peak −5.7 dBFS.
- RMS per second: −17.7, −17.3, −19.1, −19.1, −17.8, −17.8, −16.9, −17.0, −15.9, −16.3, −16.8, −16.4, −15.2, −13.3, −13.7, −18.8. Finale +2.6 dB over the late build. The last 0.5 s is digital silence.

## Checks (encoded Full HD)
- h264 yuv420p 1080x1920 60 fps, 990 frames. flash_check PASS (0 flashes).
- Seam: last→0 mean 1.83 vs the clip's 0→1 step 1.70 and median step 1.51; the dissolve lands on the predecessor of frame 0.
- Frames read from the mp4 at 0, 0.5, 1, 2, 11.7 s, the STAR, 14 s and last; 1:1 crop of the busiest region at 0.5 s. Key content inside x 0.10-0.84 w.

## Flags
- Run control: `--seed (17) --label --lead (13) --hold (2.9) --cap --still --frame a,b --simt t1,t2 --dry --search a b --sound 0 --sfx (0.30) --fin (3.1)`.
- Physics: `--r0 --g --rest --mu --ibase --ia --tau --imax --p1 --vt --vin --rsp --tmax`. Changing any physics flag changes the run: re-run the seed search.

## v1 (2026-10-21, superseded): jar + shaker, "until it becomes a SUN"
- Jar: one white line, inner x 136-880, mouth y 404, floor 1196, corners r 70. Dashed TOP line y 452. Shaker plate.
- 10 levels, r = 24 × 2^(k/3), SUN r 192. Hues violet 0.80 → red 0.02 (S .85).
- Physics: gravity 2000 px/s², sequential impulses, restitution 0.25, μ 0.05. Vertical shaker 4 px at 7.5 Hz (without it the pile locked and overflowed).
- Rain: 1.5 + 0.3·e^(t/15) /s, sizes L0/L1/L2 55/30/15%.
- Seed 58, lead 14.5 s. ×9 chain to the SUN at 14.49 s, 444 merges, 17.70 s. Same Black Key walk, `FIN_G` 3.1.
- Delivered 2026-10-21. Owner: drop the jar/shaker, and the SUN made no sense without a space theme.

Owner review 4 (2026-10-22): "no opinion, if research thinks ok lets try" -> Dopamine.exe schedule.
