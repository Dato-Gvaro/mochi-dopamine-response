# glass_tower
- New scene (batch39). **PURE MECHANIC, no characters.** It follows research/simple_viral_formula.md ("a container to fill"). A champagne-coupe pyramid is filled from the top until EVERY glass is full.
- Caption (baked, `--cap`; `--cap ''` = base): `Every glass must be ^FULL^|~Even the last corner~`.
- The only other text is the readout `GLASSES FULL n/21` at y 1432:
  - The number takes the hue of the latest row to fill and pops on each fill.
  - With 2 or fewer glasses left it adds a pulsing gold `2 LEFT` / `1 LEFT`.
  - It turns gold at 21/21.

## World (logical px)
- 21 coupes in rows 1-2-3-4-5-6.
  - Rim width 144, pitch 148, bowl a half-ellipse 54 deep, glass height 158. Each foot sits on the two rims below it.
  - The axis is x 470. The tower spans x 26-914, with the right corner rim at 912 ≤ 0.85 w. Top rim y 404, floor (feet) y 1352 = 0.704 h.
- **Row hues (rainbow from the top row down):** red, orange, yellow, green, sky, violet.
  - An empty glass is a crystal outline: white strokes, a row-tinted rim and edge, specular arcs and a twinkling rim glint.
  - It also carries a faint row-hue ghost of its full state. That ghost is the meter: the end state reads at frame 0.
- A full glass glows its row colour, with a pop and a rim star at the moment it fills. The liquid has a wavy surface, fizz bubbles, and an over-rim dome while spilling.
- Streams are drawn as ribbons. A stream that breaks below a flux of 0.30/s becomes discrete drops. Landings throw spray droplets.
- The pour enters from the dark under the caption, at x 475.

## Physics (one model; volume unit = 1 glass)
- **Spill:** above each rim half the glass spills as a weir, q = K·head^1.5 with K 3000. The two rim halves are seeded ±0.004 off level (`--dmax`). The low side spills first, and the split follows the two heads.
- **Transport:** the spill falls as ballistic parcels (G 2400 px/s²) through the gap between two glasses into the glass under that gap. The bottom row spills onto the floor. Volume moves only through the parcels, so every fall delay is real.
- **Pour (the escalation):** Q(t) = Q0·exp(L1·TQ/(PQ+1)·(t/TQ)^(PQ+1)). Q0 = 1.0/s, L1 = 0.5, TQ = 24, PQ = 4. That gives 1/s at the start and about 150/s at the last glass.
  - The quirk is emergent: a corner is fed only by the corner above it (1/2 of 1/2 …), so the two bottom corners are last.
  - The seed sets the tilts, and the tilts decide which corner goes first.
- **s14:** fills at 0.07 (top) · 2.2 / 2.7 · 5.1 … 21.3.
  - 19/21 at 25.25 s; **2 LEFT 1.53 s**, then **1 LEFT 1.07 s**; the last glass is the bottom-LEFT corner at **27.85 s**.
  - Fills per 5 s: 3/5/3/5/2/3. `--search N` lists the tension per seed (s3, s6, s17, s29 are also usable).
- **Pre-roll:** frame 0 has the top glass at 0.90 volume (brimming), calibrated by running the pre-roll. It is full at 0.07 s, and the first drops land in row 1 at about 0.45 s.
- **Finale:**
  - The pour stops 0.15-0.5 s after the last fill, and the cascade drains.
  - A light band rises bottom→top over 1.5 s: glow boost plus rising sparkles in row colours. A soft gold glow (alpha ≤ 0.10) sits behind it.
  - The camera zooms 1.0 → 0.93 and back to 1.0.
  - At last-fill + 3.0 s a 0.6 s dissolve runs into the pre-roll. The clip is **31.45 s (1887 frames)**.

## Sound
- **Melody:** Vivaldi, *Spring* RV 269, I. Allegro, bars 1-10: the ritornello, its echo and the cadence. It is violin I, transposed −12, 73 onsets, B3-C#5.
  - Source: Mutopia Project id 301, `spring-score.mid`, track "violinone" (engraving CC BY-SA 3.0; Vivaldi d. 1741, PD). Cached at `<SOUNDFONTS_DIR>\scores\vivaldi_spring\`.
  - `--verify` reports True.
  - **Note:** the bank's `audio.MELODIES['spring_vivaldi']` has 70 (A#) where the score has A (69). The scene uses the score. lib was not touched.
- **Note mapping:**
  - Every glass-full is an onset, and the LAST glass is onset 72, the cadence E4.
  - The onsets between fulls are arrivals (first liquid in a glass) and level eighths (the liquid passing k/8). They are spaced to a density that rises to the end: notes per 5 s are 9/11/12/15/13 + 13 in the last 2.85 s.
  - Kinds: 21 full, 8 arrive, 44 level. The minimum gap is 50 ms, where two fulls nearly coincide.
- **Instruments:**
  - The lead is the soundfont harp; velocity rises over the clip.
  - Under it are a strings_slow pad on the source harmony (E pedal; A-A#°-B walks; B-E cadence), changing on the onset that changes it, plus a pizz bass root on each full.
  - Cadence: a rolled E-major harp chord (E2-E5), a strings + oohs swell, a soft timpani E2, and a glass chime E5 + B5.
- **SFX (synth, no noise beds):**
  - A crystal **ting** per full glass, at the melody note +12 (top C#6, 1109 Hz). It has 3 glass partials with the upper ones quiet.
  - Liquid **plips:** a clean rising bubble blip at 560-900 Hz, and a 330 Hz tap for drops on the floor. 20% of drop landings are used, thinned to ≥ 60 ms and nudged ≥ 12 ms off notes, with density-aware gain. Plips per 5 s: 24/43/54/51/55/69.
- Energy above 3 kHz is 0.02%.

## Flags
`--seed --label --cap --still --frame N` (negative = pre-roll) `--dry --verify --search N --from S --sound 0 --sfx` (0.30) `--plip` (0.2) `--mel-rise` (1.4). Physics: `--k --dmax --q0 --l1 --tq --pq`.

## Checks (encoded Full HD, s14)
- h264 yuv420p 1080x1920, 60 fps, 1887 frames = 31.45 s.
- -14.00 LUFS, peak -8.27 dBFS. The last 1.0 s is digital silence. RMS/5 s: -17.9 → -15.3.
- flash_check PASS (0 flashes, mean lum 0.013).
- **Loop:** the last frame is identical to pre-roll frame -1. The pre-encode seam last→0 is 0.016 against a normal step of 0.027 (perfect). The encoded seam is 0.365.
- Encoded frames read at 0 / 0.5 / 1 / 2 / 3 / 14 / 27.85 / 29.5 s, plus Full HD stills at 21.7 s and 26 s (2 LEFT).
- Render takes about 8 min (Full HD).

## Doubts
- The pour reaches about 150 glasses/s at the end, which is unavoidable for a short last-corner wait: a bottom corner gets 1/32 of the flow. Stream width is ∝ flux^0.32 to stay readable, but the late cascade reads as glowing columns more than champagne.
- Fills are not accelerating (3-5 per 5 s): the corner rule makes the late fills sparse. The climbing rate comes from the streams, plips and level notes.
- 0-2.2 s has one fill. The first drops land at 0.45 s, and the row-1 levels rise.
- The ting's C#6 (4 notes) is 1 semitone above the "~C6" cap.

Delivered `<VIDEOS_DIR>\batch39\glass_tower.mp4`. Owner review: pending.

Owner review (2026-10-17): "booooring" -> rework glass_tower2: drop a large amount of small balls instead of water, overflow, catch attention in 2 s.
