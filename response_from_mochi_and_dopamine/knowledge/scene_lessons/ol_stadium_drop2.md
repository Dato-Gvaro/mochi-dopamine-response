# ol_stadium_drop2 (DopamineEXE, BRIEF_1113b C2; rebuild of ol_stadium_drop)
- Owner 2026-11-13: OK, but better execution (skips/cuts seen) and a better-looking stadium. v1 note: slow first 4 s. v1 file untouched.
- Facts = v1 (0.05 mL drop, 104,000,000 ft³, FULL at minute 45:45, minute 41 = 3.7%; see `ol_stadium_drop.md`). Volume model unchanged (bowl 180 ft + dome 121 ft), so the drawn level is still the true %.
- Status 2026-11-13: CODE ONLY (owner on the laptop). `--dry` smoke run passes; nothing rendered yet.

## Where v1 skipped (found in the code; measured on v1's camera)
| v1 source | effect on screen | v2 fix |
|---|---|---|
| `World.draw`: `far = cam.S < 30` gate for ground, exterior, bowl, dome, curtain, arches | the stands, the dome and two 13-ft arches POPPED in at 6.03 s (also v1's flash_check hit at 7.4 s) | structure drawn whenever it can be on screen (screen not inside the floor ellipse = nothing visible); dome, arches, floodlights fade over S 4 -> 1.5 px/ft |
| `r_equiv`: clipped-circle radius of the film (~255 ft) -> sqrt(a·b) of the level (170 ft) | a one-frame zoom jump ln S 0.133 (12.5%) at 8.82 s, plus a target slide | area-equivalent radius, continuous; the camera frames the floor once covered (no zoom during the climax) |
| `kcam_at`: piecewise-linear interp over the minute ticks | a slope kink at every minute | exact analytic inverse of the geometric schedule |
| `draw_water` puddle -> level style switch at V_FLOOR; level -> dome-fill switch at the rim | the water changed look in one frame (twice) | crossfade over 0.6-1.0 × V_FLOOR; one shared style, dome slices fade in over 15 ft |
| ripples/spray: different formula + centre in puddle vs level mode; spray scale `ax` -> 70 | ripple size and spray jumped at the switch | one formula, centred on the drop point at the water height, sized by the continuous radius |
| tag y followed the water (`y - ay - 70`, clamp 420, min 36 forced to 470) | tags jumped with the mode switch | fixed slot y 430 |
| field: `if S > 3000: return`, hashes `if S > 0.9`, numbers `3.5 < size < 2500` | lines/numbers/hashes popped | log-scale alpha ramps (hashes stay faint at the end instead of vanishing at 0.9) |
| seats `under = z0 < level` per row | a whole row turned blue in one frame | removed: the water body covers the submerged seats continuously |
| roof-opening outline alpha 0.45 -> 0.25 at FULL | one-frame dim | eased over 0.3 s |
| (not a skip) puddle held at a constant 120 px while the camera compensated | the slow, "frozen" first 4 s | puddle grows 80 -> 160 px, then eases to 105 px as the field arrives |

## Camera / clock continuity (asserted in `simulate()`, every drawn frame incl. the loop dissolve)
- Clock: minute durations strictly shrinking (0.19 -> 0.165 s, ≤2% per step); camera clock monotone; water level never goes down.
- Camera limits: |d ln S| <= 0.070/frame, |d2 ln S| <= 0.0040, target screen motion <= 20 px/frame, never zooms back in.
- Measured (`--dry`): max |d ln S| 0.0368 at 4.02 s, max |d2 ln S| 0.00089, target 5.1 px/frame. S 8157 -> 0.763 px/ft (settles at 5.85 s, then a still camera for the climax).
- Final framing: the stadium's outer wall spans x 108-908 px = the 0.10-0.84w side-safe zone (tight); arches and flood spill wider (decoration).

## Faster opening (v1 note)
- Drop lands 0.15 s (v1 0.25), minute 1 at 0.34 s (v1 0.59), minute 10 at 2.02 s (v1 3.48), FULL 8.26 s (v1 12.34).
- Minutes 1-12: the ADDED water falls in as a glossy drop (one per doubling, lands on the bloop), fading out over minutes 9-12.
- Minutes per second 5 -> 6 (v1 3 -> 5): Vivaldi's beat follows the clock, so the music is ~1.3x faster than v1 (risk below).

## Stadium look (stylised, generic, unbranded)
- Bowl: 3 decks (lower 0-52 ft, club 62-104, upper 116-180) split by dark fascias with multi-hue LED ribbons; section hue ramp per deck; alternate-row light/dark; the low row of each deck darker; far side brighter than near side; 0.006 rad aisles; seat-row lines; vomitory tunnels (lower + club deck, every 5th section).
- Roof edge: brushed-metal ring with 96 truss ticks, bright inner lip; 8 floodlight banks on masts (housing, 4×2 lamps, small glow) with very faint light cones onto the pitch.
- Facade: two warm lit window bands + a cool LED crown under the rim, broken by 48 ribs.
- Pitch: v1 stripes, end zones, yard lines, hashes, numbers + a midfield ring.
- Fill by tier: the waterline (with dashed foam on the near side) climbs the decks; a white glint runs along each fascia as it goes under (7.81 s lower/club fascia at 57 ft, 8.00 s club/upper at 110 ft).

## Rung table (clip second -> on screen -> counter)
| s | on screen | minute / milestone |
|---|---|---|
| 0 | a big glossy drop mid-fall onto turf fibres (macro), lands 0.15 s, splash | 1 drop |
| 0.3-1 | a second drop falls in (0.34), then 2, 4, 8-drop blobs: each doubling is a visible drop + ripple | min 1-4 |
| 1-2 | puddle grows on screen, fibres shrink to turf grain; "> A TEASPOON" 1.47 s | min 5-10 |
| 2-3 | mowing stripes; "> A SODA CAN" 2.57 s; first yard line 2.87 s | min 11-15 |
| 3-4 | yard lines + hashes; "> A 5-GAL BUCKET" 3.66 s | min 16-20 |
| 4-5 | numbers, the whole field; the bowl's seats enter 4.1 s; "> AN OIL BARREL" 4.20 s; roof, arches, floodlights fade in 4.6-5.1 s | min 21-26 |
| 5-6 | whole stadium settles (5.85 s); the film covers the floor (5.5-5.6 s), field turns blue | min 27-32 |
| 6-7 | numbers drown; "> AN OLYMPIC POOL" 6.63 s | min 33-38 |
| 7-8 | waterline climbs the decks: 1.9 -> 3.7 -> 7.5 -> 15 -> 30%; glints at 7.81 / 8.00 s | min 40-44 |
| 8-8.3 | 60% -> the dome fills -> FULL 8.26 s -> water erupts from the roof | min 45, 45:45 |
| 8.3-10 | overflow cascades down the dome and walls, flood spreads; recap at 9.16 s | counter stops at 58,899,040,911,360 |
| 10-11.6 | hold, 0.6 s dissolve to frame 0 | |
Length 11.57 s (694 frames). v1 was 15.63 s.

## READY TO RENDER (later, under the render lock; TEMP on D:)
```powershell
$env:TEMP='<REPO>\output\tmp'; $env:TMP=$env:TEMP
python scenes/ol_stadium_drop2.py --dry                                    # asserts + timeline, <1 s
$env:NF_FAST='1'; python scenes/ol_stadium_drop2.py --still --frame 0,20,60,90,170,250,280,300,330,351,420,470,480,496,520,560; Remove-Item Env:NF_FAST
$env:NF_FAST='1'; python scenes/ol_stadium_drop2.py --label fast; Remove-Item Env:NF_FAST     # full FAST clip
$env:NF_SCALE='1.0'; python scenes/ol_stadium_drop2.py --label fhd; Remove-Item Env:NF_SCALE  # FHD (v1 took 6 min)
python tools/flash_check.py output/ol_stadium_drop2_fhd_9x16.mp4
```
- Expected: 11.57 s, 694 frames, 1080x1920 @ 60 (FHD), -14 LUFS, last 0.5 s silent.
- Stills and what to look for:
  - 0 / 20 / 60 (0, 0.33, 1.0 s): the frame-0 drop is under the caption (y ≈ 516) and lands 0.15 s; the minute-1 drop falls into the puddle at 0.34 s; nothing static.
  - 90 (1.5 s): the TEASPOON tag in its fixed slot (y 430) does not cover the falling drop badly.
  - 170 (2.83 s): the first yard line arriving; turf grain/stripes crossfade clean.
  - 250 / 280 / 300 (4.17 / 4.67 / 5.0 s): the stands enter from the frame edges (no pop), roof/arches/floodlights half-faded at 280: check the arches are not fat bars at that zoom and the floodlight glows are not grey discs.
  - 330 / 351 (5.5 / 5.85 s): puddle -> level crossfade (no ghost double edge); whole stadium inside x 108-908.
  - 420 (7.0 s): the stadium LOOK at rest: decks, LED ribbons, vomitories, roof ring, floodlights, facade bands. This is the owner's "better-looking stadium" frame: judge at 1:1.
  - 470 / 480 (7.83 / 8.0 s): the waterline at each fascia + glint; foam dashes on the near waterline.
  - 496 (8.26 s, FULL) / 520 / 560: dome fill, gold pulse, geyser, curtain, flood (v1 finale).
- FAST clip: scrub 3.5-6 s frame by frame (the old pop zone) and listen to the music tempo.
- Copy to `<VIDEOS_DIR>\DopamineExe\review\ideas_1113\ol_stadium_drop2\` with a contact sheet.

## Open risks
- Music tempo: one Vivaldi beat per minute at 5-6 beats/s (v1 3-5): the presto may blur. Fallback flags: `--dt0 0.21 --dte 0.18` (slower, FULL ≈ 9 s) without touching code.
- Teaspoon (the first milestone tag) is at 1.47 s, not ~1 s; the first visible rungs are the minute drops from 0.34 s. Faster tags need `--dt0 ~0.13`, which pushes the clock to ~7/s.
- Untested visuals (code only): LED ribbon widths, floodlight sizes (tuned for S 0.76 via `k = S/0.76`), light-cone alpha, foam dashes. The first stills decide.
- The climax plays on a still camera (by design); if it reads static, a tiny push-in can be added to `raw_log_S` after minute 40 (the asserts guard it).
- Final framing is tight to the side-safe zone (108-908 px); `--sf` lowers it if a still shows the wall touching the Shorts buttons.
- `draw_ground`'s radial gradient is only drawn once the floor ellipse no longer fills the screen (S < ~12); the plaza simply fades in with the camera, not a pop, but check frame 250.

## Result 2026-11-13 (FHD, label fhd)
- No still fixes needed. 11.57 s, -14.00 LUFS, -5.3 dBTP, flash PASS (2, worst 2/s at 4.88 s), seam 2.96 = one ordinary macro step (median 2.72). Frame-step scan: ratios ≤9 are the per-minute water pulses on the still camera (Δ≈3); v1's switches are gone. FHD render ~5 min.
