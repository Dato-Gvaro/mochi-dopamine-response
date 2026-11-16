# shelter_cold: BLANKETS vs CANDLES at −10 °C, who gets to 18 °C? (shelter pilot B, 2026-11-15, NEW)

- Brief: docs/BRIEF_shelter_pilots.md (pilot B). New file `scenes/shelter_cold.py`; no lib changes.
- Gate (research/WINNING_FORMULA.md): 1 hook, 2 FILL (thermometer to 18 °C from frame 0), 3 ×2 per hour, 6 everyday
  question ("do candle heaters work?") settled by a thermal-camera view, 7 length, 8 finale = **6**; −1 if judged a
  race without a real lead change (Bolt leads only at frame 0) → 5.

## The situation
- Power out, −10 °C outside, two identical concrete shelter rooms at −2 °C. Thermal-camera look.
- Every sim hour (= 2.0 clip s) each DOUBLES their method:
  - Mochi: blankets over a small tent around her: 1, 2, 4, 8, 16 (land 0.09 s apart).
  - Bolt: tealights: 2, 4, 8, 16, 32 (lit 0.055 s apart), on the floor and 3 wall shelves.

## The model (lumped, SI; the meters read it)
| Quantity | Value | Source / status |
|---|---|---|
| Outside | −10 °C | scenario |
| Start | −2 °C both rooms (sim starts 0.25 h before frame 0) | scenario |
| Body heat | 100 W | 1 met = 58.2 W/m² × ~1.8 m² body area (ASHRAE 55 definition of the met) |
| Tealight | 30 W | Wikipedia "Tealight" (~32 W); measured 10-40 W (Galaxus test; NPL "candle power" method) |
| 18 °C | WHO minimum indoor temperature in the cold season | WHO Housing and Health Guidelines (2018), ch. 4 (NCBI NBK535294) |
| Room → outside | UA 40 W/K, C 150 kJ/K (τ ≈ 1 h) | ASSUMED: a small uninsulated concrete room (~30-40 m² envelope at U ≈ 1-1.3) with air + surface mass |
| Tent | 5 m², R = 0.17 (air films) + 0.10 per blanket m²K/W, C = 2 + 0.6 n kJ/K | ASSUMED: a ~4 mm fleece/wool blanket, k ≈ 0.04 W/mK |
| Physics | heat flow = A·ΔT/R (Fourier): doubling the blankets roughly halves the tent's loss | textbook |

- Honest outcome: 100 W kept under 16 blankets beats 960 W poured into a leaky room. Bolt's room does warm (32
  tealights ≈ a small heater) but slowly and mostly at the ceiling.
- Heat-map dressing (not in the meters): wall faces at Tr − 0.45 (Tr − Tsoil); a warm ceiling layer +0.006 K/W of
  candle power; narrow plumes (24 K, 70 px) and a white-hot flame core per candle; 33 °C halos at the bodies; the tent
  shell grades from Tf to the room.

## Captions, titles, comment
- Caption (baked; base `--cap ""`): "No power, −10°C: every hour they ~DOUBLE~ it" / "~BLANKETS~ or ~CANDLES~: who gets to ~18°C~?"
- Titles: see the brief. No "until", no kid words ("fort" avoided on purpose).

## Music
- Vivaldi, The Four Seasons, Winter RV 297, II. Largo ("by the fire"; PD; Mutopia #351 `winter-score-1.mid`), bars 1-2,
  re-timed (×~0.9) so bar 3's E-flat downbeat = 18 °C: solo violin, pizz violins, viola, cello.
- Note per hit: each candle lit = a celesta E-flat chord tone (+ a tiny ignite); each blanket landed = a pizz tone
  (+ a soft pok). E-flat tutti + timpani + harp on 18 °C. Last 0.5 s silent.

## Results / checks (label p1, Full HD)
- Tent / Bolt's room (°C): 0 s −3.2/−2.9 · 2 s −0.4/−4.8 · 4 s 0.6/−4.7 · 6 s 4.1/−2.8 · 8 s 11.0/1.3 · 10 s 19.4/9.2.
- **18 °C at clip 9.65 s** (16 blankets); Bolt 8 °C then, 13 °C at the end (32 candles).
- h264 yuv420p 1080x1920 60 fps, 730 f = 12.17 s; −14.01 LUFS, peak −5.37, last 0.5 s −65.2 dB; flash PASS; seam 0.39;
  hit events per 5 s 10 → 37.
- Delivered `<VIDEOS_DIR>/MochiAndBolt/review/shelter_cold.mp4` + `shelter_cold_files/`. Owner review: APPROVED 2026-11-15 with a colour fix (v2 below).

## Lessons
- A heat map can CONTRADICT the meter: Bolt's big room at 8-12 °C covers 10x the area of Mochi's 18-23 °C tent and
  looks "warmer". v1 plumes (55 K, 170 px) + ceiling layer (0.016 K/W) made it a blaze; cut to 24 K / 70 px /
  0.004 K/W, a bigger tent (r 100 + 4.3/blanket) and a live °C tag over each blob.
- v2 colour fix (owner, 2026-11-15; meters, timing, music, caption unchanged). The v1 scale put 10 °C at green and
  15 °C at yellow, so Bolt's 8-12 °C room out-glowed the 18 °C tent. Fixes:
  - New monotonic scale: blue to 9 °C, cyan to 13 °C, green only at 14.5 °C. The warm band starts at 15.5 °C:
    yellow, orange 17, red-orange 19, red 24, then magenta/white for flames.
  - Tent made bigger: r 118 + 3.2 per blanket (was 100 + 4.3), the same outer size at 16 blankets.
  - An additive ring glow hugs the tent arc. It uses the tent's own colour and fades in from 8 °C to 18 °C.
  - Dressing tamed: ceiling layer 0.004 → 0.0015 K/W; plume decay 70 → 34 px.
  - Rule: anchor a heat-map scale so the LOSER's final value is still cool-coloured. The area of colour reads as
    the amount of heat.
- Meter label v2: the live value with WARM! beside it (e.g. "18.3°C WARM!"). It now agrees with the floating tag.
  v1 froze at "18°C WARM!" while the tag climbed to 23.

## Doubts
- The visual read (above); no real lead change; the model constants are assumed.

## 4K (2026-11-15, approved owner)
- `<VIDEOS_DIR>/MochiAndBolt/reserve/shelter_cold_4k.mp4` + `_UPLOAD.md`; FHD review copy archived in `archive/reviewed_2026-11-15/`.
