# ol_champagne_tower (Dopamine.exe)
- New scene, character-free (docs/BRIEF_channel2.md, docs/BRIEF_overnight_1023.md). Skeleton: ×2 (each full glass feeds 2 more) toward a named end state; concrete object, one obvious rule.
- Caption (baked, `--cap`; `--cap ''` = base): `Every glass that fills ^overflows^ into 2 more|until the whole tower is ~FULL~` (`^x^` = fill-front row hue, `~x~` = gold).
- Delivered: `<VIDEOS_DIR>\DopamineExe\review\ol_champagne_tower.mp4` (v2, Full HD, seed 8, label fhdv2, 16.67 s, 1000 frames). No 4K yet.

## World (logical 1080x1920)
- 12-row pyramid of coupe glasses = **78**: pitch 60 px (rims touch), row height 62, top rim y 470, tray line y 1214; bottom row x 148-868 (inside 0.10-0.84 w). Bowl: rounded profile, rim half-width 28.5, depth 19, rim ellipse half-height 3.6 (slight top-down view); stem, knob, foot standing on the two rims below. Thin white outlines (85 %), white gloss streak + specular dot per bowl.
- Liquid colour = ordered rainbow by row, HSV S 0.75 V 0.95, hue 0.02 (warm red, top) -> 0.80 (violet, bottom); surface ellipse lighter, depth darker; bubbles rise in glasses > 35 % full. Streams blend parent-row -> child-row hue, white gloss core line, width 1.7 + 1.05 ln(1+flow) px (cap 6.4); ripples where a stream lands; droplets hop on the tray.
- Bottle: dark green glass, gold foil neck, mouth (517, 406); tilts 15° -> 26° as the pour rate climbs, levels to 3° after the cadence.
- HUD: meter y 1286 (x 170-846, row-hue gradient, white marker, gold FULL goal from frame 0, breathes on every bar); counter y 1492 "N" + grey "/78" + "GLASSES FULL" (gold at the end); a small "×2" pill in the row hue at the right end of each row, popping in when that row first overflows (row 11 pill reaches x ~912, decoration); watermark "DOPAMINE.EXE" right-aligned 894 at y 1244, 35 %.

## Rule / model (exact, no integration)
- A full glass passes everything above its capacity over its 2 lips, split p / 1-p, p = 0.5 ± U(0.07) per glass (seeded imperfection: the two sides are not mirror twins, so ONE corner is last).
- Quasi-static Pascal flow gives every glass's cumulative inflow A_k(V) for pour volume V (table over ln V). Every stream falls TAU = 0.16 s, so row r sees the pour r·TAU later: level_k(t) = min(1, A_k(V(t − r·TAU))). Edge glasses only ever get half an edge glass's overflow, so the middle fills first and the edges need 2× the volume per row (bottom corner ≈ 3,700 glasses poured).
- Pour curve V(t): monotone PCHIP through knots solved by `--design --v0 14 --dtc 13.8 --r0 3.5 --r1 9` (Powell: fills at a 3.5 -> 9 /s ramp, monotone pour rate, last corner ≥ 0.29 s after the one before). Pour rate (glasses/s) per second: 5.1, 5.1, 5.1, 5.2, 5.3, 5.5, 6.4, 10, 26, 48, 124, 634, 4,650, 15,800, then the bottle stops (0.30 s before the cadence, 0.12 s ramp) and the stream tails fall out row by row (calm by ~1.8 s after).
- Each fill is moved onto the music's 16th-note grid by a local time warp of that glass only (max 61 ms, mean 28 ms); the last glass is the cadence itself.

## Timeline (clip s, seed 8)
- Frame 0 = design time 0.12: 9 full (rows 0-2 + row 3 middle), rows 3-4 filling, ~14 streams, 5 hues; first fill **0.03 s**.
- 0.5 s: 12 full, row 4 filling, ×2 pill row 4 popped. 1 s: 13. 2 s: 14-16, rows 5-6 filling. 6.5 s: 35 (front at rows 9-10 in the middle). 13.1-13.6 s: the last corners fill down both edges on eighth notes.
- Fills per second: 5, 2, 6, 4, 3, 3, 6, 6, 4, 5, 7, 7, 7, then 4 in the last 0.86 s (the 4 corners, one per eighth).
- **Last glass (row 11, left corner) at 13.86 s** = bar 41 downbeat. Finale: gold-white sparkle ×2.2 + 2 soft gold rings from that glass, counter turns gold 78/78, meter goal glows, a calm light sweep (top-left -> bottom-right, 1.15 s) brightens every glass + small sparkles; streams drain top-down.
- Hold 2.2 s → 0.6 s dissolve into the pre-roll (t −0.6..0). **16.67 s, 1000 frames.**

## Sound
- **Music played as music:** Verdi, "Libiamo ne' lieti calici" (Brindisi), La Traviata (1853; Verdi d. 1901, PD). Source: Mutopia "Mutopia-2008/01/13-1215" (piano transcription by N. Toledo, 1857-69, Public Domain), `<SOUNDFONTS_DIR>\scores\verdi_brindisi\Traviata_02.mid` + `SOURCE_mutopia_1215.txt` (downloaded 2026-10-23). Not on the used/banned lists, not kid-coded, no earlier scene uses it. Theme fit: it is THE drinking song ("let's drink from the joyful cups").
- Quarter-beats 34.0-61.5: the pickup "Li-" (bar 22) through Alfredo's verse to the Bb cadence on the bar 41 downbeat. One steady tempo, **79.5 bars/min** (dotted quarter), solved so the cadence = last glass.
- Arrangement (lib/orchestra): melody on strings + clarinet, flute 8va from bar 32; waltz "oom" on pizz + contrabass 8vb, "pah-pah" chords on harp + pizz; horns sustain the harmony from bar 32 (build). Cadence: held Bb chord (strings, horns, flute, clarinet, cello/contrabass), rolled harp Bb2-Bb5, celesta Bb5-Bb6, soft timpani Bb2.
- SFX (×0.42): a glass tink per fill (sine + quiet 2.76× wineglass partial, chord tone of the score's harmony in C6-B6, rising through the chord), a richer Bb5 tink on the last glass; tonal liquid bloops (rising sine) from every filling glass, 3-9 /s each, pitched Bb4 -> G6 by its level (the filling-bottle rise); soft plips where streams land on full glasses / the tray (up to 24 /s); a rising Bb chime run along the finale sweep. Non-tink density-scaled ÷ √(rate/12). No noise anywhere. SFX events per second: 31, 32, 38, 35, 38, 39, 40, 39, 39, 36, 41, 42, 40, 30 (last 0.86 s), 29 (finale).
- `level_bed` gain ride (+3 dB crescendo, cadence +3 dB), `audio.master(peak_db=None, reverb=0.5)`, last 0.6 s digital silence.

## Checks (encoded Full HD v2)
- h264 yuv420p 1080x1920, 60 fps, 1000 frames, 16.67 s. **flash_check PASS** (0 flashes, mean lum 0.012).
- **−14.00 LUFS**, peak −6.82 dBFS, last 0.5 s digital silence; energy > 5 kHz 0.02 %. RMS per second: −17.9, −18.5, −17.6, −17.4, −17.6, −17.8, −16.8, −16.6, −17.2, −16.8, −16.4, −16.5, −16.1, −16.7, −15.6 (cadence), −19.4, −95.6.
- Seam: pre-encode last→0 0.082 vs a normal step 0.072; encoded (check_clip) 0.439.
- Frames read from the mp4 at 0, 0.5, 1, 2, 6.5, 7, 13.0, 13.87, 13.9, 13.95, 14.3, 14.45, 14.6, 15.5 s and the last frame; 1:1 crops of the 7 s mid-tower cascade, the last corner at 13.9 s and the finale rings.
- v1 -> v2 (self-review): bigger last-glass sparkle + gold rings, stronger finale sweep, rounded falling stream tails, faster pop-in of the row pills (frame 0 showed a dark half-faded pill).

## Flags
`--seed (8) --label --cap --still --frame a,b --dry --design --sound 0 --sfx (0.42) --fin (2.0) --shift (0.12) --amp (0.07) --v0 (14)`; design-only: `--dtc (14.6) --r0 (3.0) --r1 (8.0)`. Changing `--seed/--amp/--v0` needs a new `--design` and pasting KNOT_S/KNOT_C.

## Doubts
- The physics is honest Pascal flow, so the last 3 s are the edge glasses filling while the middle just overflows; the fill count/s dips in the final 0.86 s (4 corners on eighths) although the SFX density and stream thickness keep climbing.
- The late pour rate is physically absurd (×3,000) — streams are width-capped so it only reads as "faster, thicker".
- Empty glass outlines fill the lower half for the first ~4 s (5 hues on top at frame 0).
