# ol_domino_giant (Dopamine.exe)
- New character-free scene (docs/BRIEF_channel2.md): the famous geometric domino chain, taken from a 1.5 cm domino to one as big as the Milky Way. Concrete objects plus an obvious rule.
- Caption (baked, `--cap`; `--cap ''` = base): `Every domino knocks over one ^2× BIGGER^|until one is as big as a ~GALAXY~` (`^x^` = current domino hue, `~x~` = gold).
- Delivered: `<VIDEOS_DIR>\DopamineExe\review\ol_domino_giant.mp4` (**v3.1**, Full HD, label fhd31, 17.80 s, 1,068 frames). No 4K yet.
- History:
  - **v1:** ×1.5 to a skyscraper, stretching hit gaps, Mendelssohn Wedding March, 16.07 s. Rejected by the coordinator: slowdown, wedding vibe.
  - **v2:** ×1.5, 1.5 cm → 253 m → a 379 m skyscraper; one hit per beat then 8 on eighths; Ride of the Valkyries bars 64-71; 13.80 s.
  - **v3.1 (coordinator, 2026-10-24):** v3's landmarks were specks ("the viewer never SEES the rocket/Everest/Moon/Earth/Jupiter/Sun"). Six labelled MOMENTS replace them (see below), and the camera dwells on each. The mug, nebula, cluster and Earth's orbit were dropped. Everything else is unchanged.
  - **v3:** after the owner's v2 review ("interesting, but it can get to bigger objects — I was waiting for a spaceship and a planet and maybe a galaxy"). The ratio is now 2× (a fixed 1.5× would need ~130 dominoes for 23 orders of magnitude), with eighths then sixteenths so the rate only climbs. The chain runs on to planets, the Sun and a galaxy-sized final domino.

## World (logical 1080x1920, side view)
- 77 dominoes: d0..d75 (1.5 cm → 59,899 ly) + the final gold domino d76 = 119,797 light-years (the Milky Way is ~100,000 ly). Thickness 0.17 h, gap 0.50 h (contact angle 30°). The chain is self-similar about its vanishing point (back face of domino k at 0.67 h_k).
- Ground: one white line at y 1130. Black background. A black fade above y 330-470 keeps the incoming giants off the caption.
- Dominoes: lacquered wood with gradient, sheen, grain, a thin white edge highlight and a dark outline. Hue 0.52 + 0.030 k (an ordered rainbow, ~2.3 cycles over the chain), S 0.74, V 0.90, with V lowered around yellow-green. The final domino is gold.
- Landmarks (true scale, each in the gap of a domino slightly bigger than itself):
  - everyday: coin (k 1), mug (3), bottle (5), person (7), car (8), house (10);
  - big: rocket 110 m (13), skyscraper 380 m (15), Everest (20);
  - space: Moon (28), Earth (30), Jupiter (34), Sun (37), Earth's orbit (45), solar system (50), Orion Nebula (64), a star cluster (67), and the Milky Way behind the final domino.
  - Everyday ones are dim slate silhouettes. Rocket upward get a small label under the ground line ("Moon", "Earth"…). Space ones are calm coloured discs: grey cratered Moon, blue Earth with green continents, banded Jupiter, an orange Sun disc with a hugging glow (no white), and orbit ellipses.
  - The galaxy is a tilted static spiral: ~1,100 dots in ordered hues (gold core → rose → violet → blue).
  - Big landmarks fade in as they shrink below ~1350 px on screen (no large-area pop).
- HUD:
  - Log meter at y 1252 with ticks 1 m / 1 km / Earth / Sun / 1 light-year, "1.5 cm" at the start, and a gold spiral glyph + "GALAXY" goal from frame 0.
  - Counter at y 1478: the size in real units (cm, m, km with commas, "million km", "billion km", "light-years"), a "×2" pill in the current hue that pops on each hit, and "DOMINO n" ("DOMINO 77 · GALAXY-SIZED" in gold at the end). Auto-fits to 800 px.
  - Watermark "DOPAMINE.EXE".

## Landmark moments (v3.1)
- Each moment is drawn at true scale, behind the dominoes, centred near x 500-600. It starts ~400-470 px tall: about 4× the struck domino and the size of the next-but-one domino.
- The camera DWELLS ~0.55 s on it: the zoom-out slows to 0.7 doublings while the hits continue at full rate, so the dominoes visibly overtake the landmark (struck 90 → ~650 px).
- Between moments it eases out (Hermite keyframes, forced non-decreasing: 0 zoom-in frames; peak ~16 doublings/s in the rushes).
- Labels are 38-40 px (companions 26-28 px), drawn above each part and over the dominoes, inside x 112-902 and below y 505. They show while the main part is 110-1150 px.

| moment (dwell centre) | parts | main size on screen |
|---|---|---|
| street 3.05 s | house (+ car, person) | 360 px tall |
| tower 5.55 s | skyscraper (+ rocket) | 470 px |
| Everest 7.3 s | Mount Everest | 200 px tall × 640 wide |
| Earth 8.83 s | Earth (+ Moon) | 400 px |
| Sun 9.9 s | the Sun (+ Jupiter, Earth at true scale) | 430 px |
| solar system 11.88 s | orbits + planets | 560 px wide |
| Milky Way 14.5-17.8 s | the finale | ~480 px |

- Early small landmarks: coin (frame 0) and bottle only.
- Camera (v3.1): a camera index c (the domino of index c is HPX = 150 px tall), with the vanishing point at x 229.5.
  - c follows the chain until 0.6 s, then runs through the dwells, then to the finale: the final domino 643 px tall when struck and ~550 px when landed.
  - The vanishing point glides to x −239 around the strike, so the lying gold domino spans ~x 245-800 under the Milky Way.
  - This replaces the v3 camera notes below.

## Kinematics / camera (v3)
- Free phase θ = θc·(0.4u + 0.6u²) to contact. Then each domino leans on the next (corner solved onto its back face every frame). The final domino falls 0 → 90° over 3 beats.
- Hits (b = dotted-quarter beats from the bar-60 downbeat; 76 hits):
  - one per beat at b −1 (pre-roll) to 13 (2.07/s);
  - 36 on eighths at b 14-25.67 (6.2/s);
  - 25 on sixteenths at b 26-30 (12.4/s); the b 30 hit strikes the final domino;
  - landing at b 33 = the bar-71 cadence.
- Camera: anchored on the struck domino's back face, which stays 150 px tall at x 330. The zoom rate follows the hit rate (smoothed σ 0.25 s), so the zoom-out speeds up with the music but is never stepped.
  - From chain index 70 the struck domino grows ×4.1 (the zoom-out slows, never reverses: 0 zoom-in frames measured) and the anchor glides to x 150.
  - End framing: the gold domino ~560 px tall, lying x 245-801 under the Milky Way (465 px wide, centre 0.40 D above the ground).
- Perf note: an upright domino is culled by its back face (px − w > 1100), not its height; upright giants over 2400 px are drawn clipped (cairo stroking 10^5-px paths cost 3-13 s/frame).

## Timeline (clip s)
- 0 s: mid-action, 3 cm striking 6 cm, coin.
- 0.5 s: 12 cm, bottle ahead.
- 1 s: 24 cm.
- 2 s: 96 cm, person + car.
- 5.3 s: rocket.
- 6.3 s: skyscraper.
- 7.4 s: Everest.
- 8.7 s: Moon.
- 9.0 s: Earth.
- 9.7 s: Jupiter.
- 10.2 s: Sun.
- 11.4 s: Earth's orbit.
- 12.2 s: solar system.
- 12.9 s: first light-year.
- 13.5 s: Orion Nebula.
- 13.8 s: star cluster.
- 14.5 s: the final domino is struck, the Milky Way appears.
- 15.95 s: it lands on the cadence.
- 17.2 s: 0.6 s dissolve into the pre-roll.
- Hits per second: 3, 2, 2, 2, 2, 2, 3, 6, 6, 7, 6, 6, 9, 12, 7. Then the 1.45 s final fall and the landing (3 low clacks).

## Sound
- **Music:** Wagner, "Ride of the Valkyries" (Die Walküre, Act III prelude, 1856; Wagner d. 1883, PD).
  - Source: the orchestral MIDI transcription rvalkyri.mid (midiworld.com, "Rearranged L. Roberts"), saved at `<SOUNDFONTS_DIR>\scores\wagner_valkyries\` + `SOURCE_midiworld.txt`. No Mutopia/Commons score exists, and IMSLP is captcha-gated.
  - Excerpt: bars 60-70 (the first, second and third brass statements of the theme over the string swirls), then our held B-major chord on the bar-71 downbeat. No looping needed.
  - Tempo: one steady tempo, bar = 1.45 s (dotted quarter = 124).
- Arrangement (lib/orchestra): Strings I/II, horns + trombones + brass section on the theme, contrabass + cello 8va, timpani track, a soft choir doubling the horns. Cadence: a B-major chord on strings, choir, horns, trombones and cello/contrabass, timpani B2 and a soft boom. `level_bed` crescendo 5 dB; the finale sits +3 dB.
- SFX (×0.45): one tonal wood clack per hit.
  - Pitch class = the contrabass note at the hit; the octave walks E5 → E2 with size.
  - Gain (0.62-1.0 by size) ÷ √(rate/2), and each clack is cut to 2.5× its interval, so the sixteenths stay crisp instead of rumbling.
  - Landing: 3 low clacks (B1/F#2/B2).
- `audio.master(peak_db=None, reverb=0.5)`; last 0.6 s digital silence.

## Checks (encoded Full HD v3.1)
- flash_check PASS (0 flashes, mean lum 0.020).
- −14.01 LUFS, peak −6.22 dBFS, last 0.5 s digital silence; RMS per second identical to v3 (audio unchanged).
- Seam 1067→0 2.70 vs normal steps of 1.9-2.9.
- Frames read from the mp4 at 0, 2, 2.8, 3.05, 3.3, 5.55, 7.3, 8.6, 8.83, 9.08, 9.65, 9.9, 10.15, 11.88, 15.2 and 17.78 s: every moment is big and labelled for ≥ 0.5 s.

## Checks (encoded Full HD v3)
- h264 yuv420p 1080x1920, 60 fps, 1,068 frames, 17.80 s.
- **flash_check PASS**: 0 flashes, mean lum 0.019.
- **−14.01 LUFS**, peak −6.22 dBFS, last 0.5 s digital silence; energy > 5 kHz 0.12%.
- RMS per second: −18.9, −19.2, −17.4, −18.1, −18.4, −17.4, −17.3, −16.9, −16.4, −16.0, −15.7, −16.2, −15.4, −15.1, −15.9, −15.7, −14.9 (landing), −58.8.
- Seam: the last frame = the pre-roll frame before frame 0. Encoded 1067→0 delta 3.22 vs normal steps of 1.8-2.6 (frame 0 is also a hit).
- Frames read from the mp4 at 0, 0.5, 1, 2, 6.3, 7.45, 8.75, 9.1, 9.7, 10.2, 12.3, 13.6, 14.6, 15.2, 16.2 and 17.78 s.

## Flags
`--label --cap --still --frame a,b --dry --sound 0 --sfx (0.45) --fin (2.0) --bar (1.45) --hpx (150) --hold (1.25) --fink (4.1)`.
