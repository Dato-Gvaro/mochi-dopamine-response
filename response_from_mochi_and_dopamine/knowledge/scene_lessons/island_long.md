# island_long: STRANDED (Mochi & Bolt long video 1). Kit + chapter 1 FISH

- Brief: docs/BRIEF_island_long.md. Phase 1 (2026-11-07): the shared kit + the chapter 1 pilot, stills only. No full render has been done yet; it waits on the owner.
- Files:
  - `lib/island.py` is the kit.
  - `scenes/island_ch1_fish.py` is chapter 1.

## Kit (`lib/island.py`): every chapter draws through it
- **View:** world metres (x right, y UP, y = 0 = the sea surface) → px.
  - `View(tag, w, h, S, ox, oy)`.
  - `.safe` holds the 9:16 key-content box: x 0.10-0.84w, y ≤ 0.71h.
  - `.ui` is the label scale (16:9 1.0, 9:16 1.3).
  - Simulate once in metres; each layout is only a different View (camera).
- **Sky cycle:** `tod_state(tod, storm)`.
  - tod 0 dawn, 1 day, 2 dusk, 3 night (wraps); storm 0..1 mixes in grey.
  - `sky()` draws the gradient, sun/moon, stars and clouds; `sea_back()` the far sea band, far islands and sun glitter.
- **Water in cross-section, in draw order:**
  1. `water_back()`: the OPAQUE far water. Without it the previous frame shows through the translucent column (found on still 1).
  2. `bed()`: the receding bed band with numpy caustics (`caustic_field`, added in OPERATOR_ADD), ripples, far reef lumps, pebbles, and the sand cut face below it.
  3. `seaweed()`.
  4. `water_cut()`: the depth gradient, god rays and the meniscus line.
  5. `bubbles()`.
- **Sand:** `sand_face_source()` is ONE gradient anchored in world height, so the beach cut and the bed cut meet without a seam.
- **Land:**
  - `rock(poly_m, water_path="none")` draws seeded cobbles (cached), a lit-to-dark gradient and crack lines. Use `"none"` for a cut section; any other value adds a water tint and a tide band.
  - `beach()`, `palm()` (sways with `wind`), `ground_shadow()`.
- **Characters:**
  - `RB = 0.60/1.84` m: on the island, Bolt is 0.60 m (2 ft) tall.
  - `blob(..., rot, look, mood, mouth)` calls toon.draw_char with NO squash, the exact rest shape.
  - `blob_center(who, foot)` and `eye_world()` give the point between the eyes, the ray end for any sight-line physics.
- **Tools:** `float_tool(draw_fn)` adds a hover bob plus 3 faint motes under the tool ("by magic"; no hands, no limbs).
- **HUD:**
  - `hud(score, day, tod, storm, team, pulse)`: top-left MOCHI x · BOLT y · TEAM (dim "-" until earned), top-right DAY n with a sky icon and the time word.
  - `caption(segs)`: deadpan, top centre, on a soft pill.
  - `banner(chapter, name, age)`: rises from below the caption.
  - `title_card()` for between chapters; `stamp()` for MISS/HIT pops.
- **Transition:** `tide_wipe(surf_next, u)` sweeps the next chapter in with a foamy wave front.
- **Units:** `ft_in()`, `cm()`, `both()`: US first.
- **Music:**
  - `CHAPTER_MUSIC`: ch1 = Boccherini, Minuet from the String Quintet Op. 11 No. 5 (1771; Boccherini d. 1805, public domain).
    - No file in docs/scenes, scenes or lib names it (checked 2026-11-07).
    - Source: the cached MIDI (`<SOUNDFONTS_DIR>\scores\boccherini_minuet\Boccherini_Minuet_anacrusis.mid`) has an empty copyright field, no SOURCE file and no README entry, so it is NOT used. Mutopia has no copy; mfiles.co.uk's terms are unclear.
    - Instead the 1st-violin theme (bars 1-4: two turn figures + 12 notes) is re-sequenced by hand as data (`THEME` in the scene): pitches and rhythm of the 1771 work only.
  - Proposals, also unused: ch5 Liszt Liebestraum 3, ch7 Bach Passacaglia BWV 582, ch9 Chopin "Heroic" Polonaise.
  - `melody_top()` returns the top note per onset (one note per event).
- **Render:** `render_chunks(draw, canvas, nf, out, chunk_dir, resume_cmd)` uses the domino-long pattern: 900-frame chunks, tmp → fsync (r+b) → rename, the last 2 chunks probed on restart, PROGRESS.txt with the resume command, concat.

## Chapter 1: FISH (`scenes/island_ch1_fish.py`)

### The model (honest, fixed dt)
- **Sight line:**
  - The light ray fish → eye obeys Snell's law, sin a_air = n sin a_water, with n = 1.33, at a flat surface y = 0. The drawn ±1 cm wave is cosmetic.
  - The ray's surface point is found by bisection (48 iterations, vectorised).
  - The eye is the thrower's REAL eye point.
- **Where it looks:**
  - The binocular (sagittal) image: the air ray, extended under the water, meets the fish's vertical at depth d · tan(a_w)/tan(a_air). Straight down this is d/n (= 75%).
  - The ghost fish is the whole outline mapped point by point, so it is squashed and shallower, as the eye sees it.
- **Spear:**
  - 1.05 m, 0.40 kg, 2.2 cm shaft, stone tip; dt = 1/2400 s.
  - In air: gravity only (drag < 0.1 m/s², ignored).
  - In water:
    - nose drag (Cd 0.3);
    - turbulent skin friction (Cf = 0.074 Re^-0.2 ≈ 0.0029 at Re ~1e7) on the wetted length;
    - buoyancy of the wetted volume.
  - No deflection at entry (stated simplification).
- **Fair duel:** both throwers are PERFECT shots at their aim point.
  - The launch angle is solved by bisection over the full air + water sim.
  - Bolt aims at where the fish looks; Mochi aims at the real fish. The aim point is the only difference.
- **Hit test:** HIT = the tip enters the body ellipse (a = L/2, b = 0.135 L). MISS = the shaft never touches it (checked every step).

### Result (`--report`)
| throw | who | speed | fish depth | looks (from the rock) | air / water angle | spear at the fish | result |
|---|---|---|---|---|---|---|---|
| 1 | Bolt | 27 mph (12 m/s) | 2 ft (61 cm) | 1 ft (32 cm), 52% | 58° / 40° | 11.6 in over | MISS |
| 2 "harder" | Bolt | 40 mph (18 m/s) | 1 ft 11 in | 1 ft (29 cm) | 59° / 40° | 11.3 in over | MISS |
| 3 "bigger fish" | Bolt | 27 mph | 2 ft 8 in (82 cm) | 1 ft 5 in (43 cm) | 57° / 39° | 15.3 in over | MISS |
| 4 | Mochi | 27 mph | 2 ft 6 in (76 cm) | 1 ft 4 in (40 cm) | 57° / 39° | 0.0 in | HIT |

- The sim agrees with the brief: Bolt misses 3x (over the fish every time), Mochi hits first try.
- At these slants the fish looks about 47-52% of its real depth ("looks ~50% shallower"). The brief's "~25%" is the straight-down figure; the end card states both.
- Sanity check against fishermen's practice:
  - The bowfishing "10-4 rule": aim ~4 in low for a fish 10 ft away and 1 ft deep, and double it for double the depth or distance.
  - Our model, eye 6 ft up, fish 10 ft out, 1 ft deep: it looks 0.53 ft deep, so aim 5.7 in low (5 ft eye: 6.2 in; 7 ft: 5.2 in). Same order; the rule is a rough field heuristic.

### Timeline (55.0 s, 3300 frames)
- **0.0-1.8 s:** frame 0 is mid-wind-up, with the ray, the ghost and the meter already up. Throw 1 launches at 0.5 s, plays at x0.25 slow-mo (labelled with its speed in mph), passes over the fish at 1.07 s, and the MISS stamp reads "1 ft over it".
- **1.6 s:** the CHAPTER 1 · FISH banner.
- **4.8-10.3 s:** the explanation: the normal at the surface point, 58° / 40° arcs, "light bends here · n = 1.33".
- **13.0 s:** throw 2, "Bolt's fix: throw it harder" (40 mph). The same miss: the speed does not move the aim point.
- **18-21 s:** the small fish leaves and the big one comes in.
- **23.0 s:** throw 3, "Bolt's fix: a bigger fish". The miss is bigger (the error grows with depth).
- **27.5 s:** the swap. Bolt slides back; Mochi passes in front of him with a small hop. A hop OVER him left the 16:9 frame.
- **32.5 s:** Mochi throws. The "aims 1 ft 4 in lower" bracket shows; HIT at 33.17 s; MOCHI 1.
- **The fish:** it rides her floating spear home, then floats over to above Bolt at 40.4-42.6 s ("She shares. He blames the fish.").
- **47.6 s:** the "WHY BOLT MISSED" card (n = 1.33; Bolt's last view: looked 1 ft 5 in, was 2 ft 8 in; 25% straight down). Caption: "Day 1. Bolt still blames the fish."
- **Sky:** tod 0.62 → 0.87 (late dawn → morning).

### Cameras v2 (2026-11-07, coordinator (a)+(b); supersedes the layout numbers below)
- **16:9 (v3, coordinator round 2): the same push-in idea as 9:16, on the same `zoom_and_throw(c)` clock.**
  - WIDE = S 300, origin (450, 565): both blobs fully in frame (Mochi's left edge ~40 px in) + the meter at the top-right.
  - TIGHT per throw = S 850 (the fish 2.5x its px at the old static S 340, 2.8x the wide shot). The left edge is 0.25 m before that throw's surface point P; the bottom edge is 0.30 m below the fish. The sight line, the ghost, the fish and the spear passing over it fill the frame; the sand bed is below it.
  - While tight: the meter fades, SLOW-MO sits at (960, 250) under the caption, and the stamps are fixed at (1500, 330).
  - Rays and angle labels scale x(1 + 0.5 zoom).
- **Fish darts:** after a miss they go LEFT and DOWN, away from the spear's path. A dart to the right crossed the shaft and read like a hit in the tight shot. The small fish leaves only once throw 2's spear is out of the water (T_LEAVE = c_end + RET + 0.9 = 17.4 s); the big fish enters at T_LEAVE + 0.6.
  - Check: a missed spear (fly / stuck / return) never overlaps a fish body in any of the 3300 frames.
- **9:16:** `make_view(orient, c)` is a time-dependent View.
  - WIDE = S 230 with x 0.34 m at the safe-box centre (507, 1035). TIGHT = S 400 framing x 0.30-2.30 m, bed at 0.70h.
  - Interpolation: log S, plus linear world anchor.
  - `zoom_amount(c)`: in over 0.5 s from launch -0.15 s; hold to pass +1.9 s (hit +1.6 s); out over 0.65 s.
  - While zoomed: the meter fades (1 - zoom) and the SLOW-MO tag takes its slot (shown only at zoom > 0.6); the MISS/HIT stamps sit at a fixed spot (0.84w - 150, 718).
  - Mid-zoom, Bolt crosses the 0.10w line for about 0.25 s (the camera passing). Wide and tight both hold the safe box.
- **ALL decoration ranges are world-fixed** (`WORLD_X0, WORLD_X1` = -3, 5). Seeded placement from view.x_min/x_max would swim under a moving camera.
- The audio's pan map is pinned to the old 16:9 view, so the accepted a1 mix rebuilds bit-for-bit.

### Layouts (one sim)
- **16:9:** S = 300 px/m, origin (600, 565).
  - Full width: shore + rock at the left third, the water cut over the rest.
  - The meter is bottom-right on the sand; the HUD is in the corners; the caption is top centre.
- **9:16:** S = 230, origin (428, 1035).
  - The blobs, rays and fish sit in x 0.10-0.84w; the bed ends at ~0.70h.
  - The meter is in the sky under the caption; below 0.71h is plain sand (the UI zone).
  - Stuck spears can reach past 0.84w (decoration).

### Stills (FAST, `--label final`)
- 16:9: `output/island_ch1_fish_final_16x9_f{0,100,1995,3200}.png`
- 9:16: `output/island_ch1_fish_final_9x16_f{0,1995}.png`

### Gotchas
- `throw_at(c)` keeps the last throw's window; the explanation beat needs its own window (EXPLAIN) or the rays hide 3 s after the pass.
- The impaled fish must be drawn in BOTH spear branches (flying/stuck and floating home), or it vanishes when the spear arrives.
- The 16:9 frame top is world y ≈ 1.88 m: keep hops and floating props under ~1.7 m.

### Audio (done 2026-11-07, `--audio --label a1`; no video rendered)
- **Melody:** one cell of the Boccherini theme per event, in time order (22 events): launch, splash, pass, hit, the swap landing, the share, each caption change (unless a note is within 0.6 s) and the end card.
  - A cell is a single note or a 16th-note turn (B-A-G#-A-B → A, E-D-C#-D-E → D) that runs INTO its event; Mochi's launch gets the opening turn.
  - The hit lands on A5 and the end card on A4 (the tonic).
  - Instruments: violin + pizz an octave down.
- **Bed:** a quiet strings_slow pad + cello roots that follow the theme's harmony (A or E7 per cell). The hit adds horns, a strings chord and a timpani A2; the end card holds an A-major chord; the last 0.5 s fades to silence (-38.5 dBFS).
- **SFX (all synthesised, `lib/island.py` sfx_*):**
  - launch: a whoosh;
  - splash: `audio.synth_splash` (0.9) + spray;
  - pass: a small bubble;
  - stuck: a sand thud (70 Hz);
  - hit: a thock (x0.85, timpani under it);
  - swap landing: a soft thud;
  - a tool floating up: a celesta A6-C#7-E7 shimmer.
  - Every SFX that shares an onset with a note is nudged +12 ms.
- **Measured on the MUXED proxy** (`output/island_ch1_fish_a1_proxy.mp4`, black 320x180 + AAC 192k):
  - -14.05 LUFS, true peak -2.3 dBFS.
  - 15/22 events show a > 3 dB onset within 30 ms; the hit is +5.0 dB.
  - The weak ones are the launches (the turn runs into them), the 40 mph throw's splash/pass (90 ms apart) and two captions under sustained chords.
- Files: `output/island_ch1_fish_a1_audio.wav`, `_events.json`, `_preview.mp3`. The timeline is unchanged, so the wav fits the eventual render as is.

### Still to do (after the owner's OK)
- Planned visual changes (coordinator, 2026-11-07):
  - (a) 16:9: frame tighter on the water. Raise S and/or move ox left, so the rock and blobs shrink toward the left edge and the fish and spear paths get more of the frame. The camera is only the View; the sim and timings stay.
  - (b) 9:16: a per-throw camera zoom. View(t) eases S/ox/oy from the wide framing to a tight one on thrower → fish over each wind-up, and back after the stamp; the safe box is checked at both ends.
- Full 16:9 and 9:16 renders via `render_chunks`, then flash_check and check_clip on the real files.

## Sources
- Snell's law and apparent depth d/n: any optics text (e.g. Hecht, *Optics*).
- n of fresh water 1.333 (20 °C, 589 nm): Hale & Querry, Applied Optics 12, 555 (1973).
- Seawater ~1.34, an empirical function of temperature, salinity and wavelength: Quan & Fry, Applied Optics 34(18), 3477 (1995), doi:10.1364/AO.34.003477.
  - We use the brief's 1.33. With 1.34, straight-down apparent depth changes by < 1%.
- The bowfishing "10-4 rule" and similar depth rules: [Realtree](https://realtree.com/fishing/articles/bowfishing-shooting-tips-hit-more-fish-in-fewer-shots), [MeatEater](https://themeateater.com/fish/general/how-to-bowhunt-for-small-game-in-the-water), [OffGridWeb](https://www.offgridweb.com/preparation/tip-how-to-aim-when-spearfishing-bowfishing/), [Outdoor Troop](https://outdoortroop.com/how-to-aim-properly-when-bowfishing/).
- Turbulent flat-plate skin friction Cf = 0.074 Re^-1/5: the Prandtl one-fifth-power law (standard fluid-mechanics texts).

### Delivered (2026-11-07): ch1 Full HD, waits on the owner
- `<VIDEOS_DIR>\MochiAndBolt\review\island_ch1\` holds ch1_fish_16x9.mp4 (label ch1fhd3), ch1_fish_9x16.mp4 (label ch1fhd) and README.md.
- Render: 4 chunks x ~54 s each orientation (one process, ffmpeg 2 threads), muxed with the accepted `island_ch1_fish_a1_audio.wav` without -shortest.
- **flash_check lesson:** the first 16:9 FAILED (worst 1 s = 3 at each push-out). `horizon_y` tied to the water line dragged the bright horizon band 2-3 grid rows on every camera move; each crossed cell rose then fell over > 25% of the screen.
  - 1.5 s push-outs alone did not fix it.
  - The fix: `View.hz_px` pins the horizon on screen (a dolly keeps the horizon still). 16:9 PASS, worst = 2.
  - The 9:16 passed as rendered (worst = 1) and is unchanged.
  - For any future camera move: pin the horizon.
- Encoded checks for both: h264 yuv420p 60 fps, 3300 frames, PTS step 256; -14.01 LUFS, TP -3.7 dBFS; the 1:1 miss/hit frames are clean.

## Revision b (2026-11-07, docs/BRIEF_island_ch1b.md): pacing, life, mirage, sound. delivered
- v1 source kept: `scenes/_versions/island_ch1_fish_v1.py`. Sim numbers unchanged (`--report`).
- **Pacing:** per-throw `wind` / `slow` / `ret` (THROWS) + derived camera keys (`zin0`, `zin`, `hold`, `zout16`, `mirage`).
  - Throw 1 = the teach beat: x0.25, 1.3 s wind-up, mirage 1.45-2.85, explanation 2.9-5.9 (tight), push-out 1.5 s.
  - Throws 2-3 = the repeats: x0.5, 0.8 s wind-up, push-in 0.4 s from launch -0.4, hold pass +1.3, push-out 1.2 s (9:16 0.65). Their "fix" caption lands BEFORE the wind-up.
  - Mochi: x0.25, 1.6 s wind-up (bracket reads), hold hit +1.6, push-out 1.5 s.
  - Tail: share 22.4-23.8, the card at 23.9 with "Day 1. Bolt still blames the fish.", end 29.4 (16:9 = 1764 frames).
- **9:16 = a separate EDIT** of the same clock (`EDL`, `c_of`, `t_of`): [0-5.4] [6.75-10.0] [16.4-22.4] [23.8-29.4] = 20.25 s (1215 frames): throw 1 -> "harder" -> Mochi -> card. Audio is built per edit in output time.
- **Mirage:** throw 1's fish holds still through the explanation (rays are drawn from it); for 2-3 the image freezes at the pass while the fish darts. The ghost ripples (travelling sine on the mapped outline + 3 rings) and fades; "REALLY HERE" stays. Caption "Bolt speared the fish's MIRAGE." (true: the spear goes through the image refraction lifts).
- **Card:** straw-in-a-glass inset (prop, floats), "The fish was 1.9x deeper than it looked" = throw 3 as Bolt saw it (0.82 / 0.431 m), looked 1 ft 5 in · was 2 ft 8 in (82 cm), n = 1.33. The depth meter fades at the card (it would show Mochi's view).
- **Background life:** 11-fish school (x 2.9, y -0.5 m) + 2 lone fish, world-fixed on a FAR plane (`far_xy`: screen offset from the frame centre x0.82), drawn under `water_cut` (tinted), scatter from each splash. `--check` tests every frame of both edits: 0 overlaps with spears, each tight shot's spear path, or the fish.
- **Sound:** Boccherini Minuet bars 1-4 + anacrusis + its accompaniment from the Commons MIDI (PD Mark; SOURCE.txt in the score cache), played through at 84 bpm with a bar-1 downbeat ON the hit (the phrase grid is anchored there; the music is already playing at t = 0). Leads: violin / flute / violin / strings on the hit phrase; pizz accompaniment, strings_slow harmony. Ducks -6 dB under each throw, +3.8 dB swell decaying from the hit (+ horns, strings, timpani).
  - Ambience: `I.amb_surf` (slow wave swells, ~-30 LUFS) + `I.amb_breeze`; tight camera -> 72% crossfade to a 1.1 kHz zero-phase low-pass + `I.amb_underwater` hum/bubbles.
  - SFX (`lib/island.py`): `sfx_whoosh_v` (pitch from speed and slow-mo), `sfx_plunk` + `sfx_fizz` at entry, `sfx_sand_thud` + `sfx_deflate` (Bolt's face) on a miss, `sfx_thock` + `sfx_sparkle` on the HIT, soft bell shimmers for the mirage and floating tools.
  - Measured (black proxy, AAC 384k): 16:9 -14.0 LUFS, TP -3.5 dBFS; 9:16 -14.0 LUFS, TP -4.2; last 0.5 s <= -61 dBFS; HIT onset +10.8 dB (the loudest).
- **Gotchas:**
  - `audio.mix_events` pads +2 s: v1's muxed files had a 57 s audio track on 55 s of video. Rev b cuts the wav to the edit length.
  - The far-plane map pulls everything toward the frame centre, so a "world y" there is not a screen depth: test overlaps in SCREEN space.
  - A stamp from a throw the 9:16 edit cuts can leak into the next segment: keep stamp life < the gap (repeats: 2.2 s).
- **Delivered (2026-11-07, label b1, coordinator holds applied):** Mochi's hold = hit + 2.1 s; the card is 24.4-30.9 (6.5 s). 16:9 30.9 s (1854 f), 9:16 21.75 s (1305 f; EDL [0-5.4] [6.75-10.0] [16.4-22.9] [24.3-30.9]).
  - Encoded: -14.0 LUFS, TP -3.5 / -4.1 dBFS, flash_check worst 2 / 1 (PASS), audio = video length. Full HD renders took ~2 min (16:9) and ~1.5 min (9:16).
  - Files: `<VIDEOS_DIR>\MochiAndBolt\review\island_ch1\`; v1 is in `<VIDEOS_DIR>\MochiAndBolt\archive\island_ch1_v1\` (its README corrected: the bracket reads 1 ft 2 in).

## Revision c (2026-11-07, docs/BRIEF_island_ch1c.md): the approaches as PLAN cards, a crab. Step 1 (stills) only
- rev b source kept: `scenes/_versions/island_ch1_fish_v2b.py`. Pace, sound, mirage, card, cameras and sim unchanged; 16:9 30.9 s, 9:16 21.75 s.
- **PLAN cards + ATTEMPTS strip = `lib/island.py` helpers** (`plan()`, `draw_plans()`, `plan_rects()`, `plan_layout()`, `verdict_mark()`, `ease_out_back()`, `sfx_pop()`), reusable by every chapter.
  - Motion: pop at the head 0.2 → 1.12 → 1.0 (ease-out-back s = 2.2, 0.25 s) with a speech tail, a 0.2 s hold, a 0.35 s arc into the slot under the caption, a 0.15 s punch stamp (drawn cross/check, no font glyphs), a 0.3 s ease-in dock into the strip. No loops, no blur.
  - Slots: 16:9 card at (960, cap_y + 92), strip top-left under the score (x 22, y 80, wraps at 600 px so it never reaches the caption pill at x ~640). 9:16 card at cap_y + 84, strip between the HUD and the caption, inside the safe box.
  - A head off-screen (a push-in) pops the card just inside the edge, without a tail; `pop_top` keeps it under the HUD.
- **Ch1 plans:** PLAN 1 "aim where it LOOKS" (born -0.1: already popping at frame 0), PLAN 2 "throw it HARDER" (6.5), PLAN 3 "aim for a BIGGER fish" (10.85, after throw 2's push-out; true to the sim: the bigger, deeper fish, aimed where it looks), MOCHI "aim BELOW it" (16.0). Crosses at each pass, dock +0.9 s; the check at the HIT.
  - 16:9: Mochi's winning card stays in its slot to the end (a 4th item would wrap the strip onto the fish she shares). 9:16: no PLAN 3 (the Short skips throw 3), and Mochi's card docks at 20.3 (its slot is where the end card goes).
  - The "Bolt's fix" / "Mochi aims BELOW it" captions are gone; the caption is empty 6.5-20.3. The banner moved to 2.3-5.3 (it shared the slot with plan 1); the 16:9 SLOW-MO tag moved to y 270; the shared fish floats 0.06 m lower (clear of the strip).
- **Sea bed:** `I.crab()` (pauses + scuttles in little steps; a dash away from throw 3's stuck spear, a hop after Mochi's lands), `I.sea_star()` x2, `I.shell()` x5, world-fixed on the bed band, drawn under the water tint. The bed is below the 16:9 tight frame for throws 1-2 (camera unchanged), so there the crab shows only in the wide shots and in the tight shots of throw 3 / Mochi / 9:16.
  - `--check` adds the crab vs spears, fish and HUD boxes (plan cards, strip, meter, end card): 0 / 0. The closest spear passes at 2.4x the crab's size (throw 3).
- **Sound:** + a soft `sfx_pop` per card (gain 0.26). Measured (black proxy, AAC): -14.0 LUFS both, TP -4.0 / -3.3 dBFS; the HIT is still the loudest onset (+9.2 / +11.3 dB).
- **Rev c, round 2 (coordinator):** 16:9 card size 38 (title ~45 px, h = 1.85 size), strip 30 px (9:16 26 px) with bold marks (r 0.47 sz, x1.35 stroke) and wrap at x 632; no room above the head (pop_top) -> the card pops BESIDE the head. Crab x1.6 (shell ~7 in), warm, white eyes + pupils, a small mouth; stars x1.5 (orange / soft purple) and 7 shells, all drawn ABOVE `water_cut` (15-18 % toward the water colour). A third lone fish crosses throw 1's tight shot (0-6 s, then exits right). Fish B's dart is 5 cm shallower (it touched the bigger crab).
  - Delivered: label c1, 16:9 30.9 s / 9:16 21.75 s; -14.0 LUFS, TP -4.0 / -3.3; flash worst 1 / 1; `--check` 0 / 0. rev b archived in `<VIDEOS_DIR>\MochiAndBolt\archive\island_ch1_v2\`.

## The STRANDED theme (`lib/island_music.py`, 2026-11-07): the whole long video's own music
- **Why:** the owner on ch1: Boccherini "associates with aristocrats and some old-style town with rich people, not an island". The long video gets ONE original theme with variations.
- **Provenance:** an ORIGINAL composition, written note by note in code for this channel (CLAUDE.md rule 4: our own music). No existing song, arrangement, MIDI or recording is used or imitated. It is a chill adult tropical bed; deliberately no calypso band figure (nothing like Disney's "Under the Sea": IP + made-for-kids risk with a crab on screen). Rendered with FluidSynth + MuseScore_General.sf2 (GM programs) through lib/orchestra.
- **Leitmotif:** 8 bars in D, 4/4, major-pentatonic flavour (D E F# A B; C# only on the V bar).
  - Melody per bar: A D F# E D | E F# A F# E | D E B A F# | E D E | F# A B A F# | B D E G F# | D E F# B D | E D C#.
  - Chords: Dmaj7 | F#m7 | Gmaj7 | A6 | Bm7 | Em7 | Gmaj7 | A7sus4-A7 (loops back to Dmaj7).
  - Minor variants (storm, temple): Dm7 | Bbmaj7 | Gm7 | A7 | Dm7 | Bbmaj7 | Gm7 | A7sus4-A7, with the melody mapped F# → F, B → Bb, C# → C (C# kept on the A7 bar).
- **Variants** (`M.VARIANTS`):
  - `beach_day` (ch1-2), 94 bpm: nylon-guitar offbeat skank, fretless bass (root, pickup, fifth, approach), shaker 8ths + congas, kalimba lead. The pass that carries the payoff switches to steel pan (a colour, not wall to wall).
  - `campfire` (ch3), 76 bpm: fingerpicked nylon guitar, flute / kalimba, warm pad, shaker only.
  - `storm` (ch4), 100 bpm, minor: cello / strings lead, pizz ostinato, low toms, strings pad. The theme returns after the storm with `beach_day`.
  - `jungle` (ch5-6), 98 bpm: marimba lead + marimba arpeggios, bongo / conga / claves, acoustic bass.
  - `temple` (ch7-8), 84 bpm, minor: kalimba / vibes, contrabass, strings pad, a soft low tom.
  - `raft_finale` (ch9), 100 bpm: the full band. Skank, fretless, a light kit, strings pad, steel-pan / strings lead, marimba counter-line.
- **API:**
  - `M.grid(variant, dur, anchor=(t, bar))` returns the tempo / bar / beat grid. `anchor` puts that bar's downbeat on t, and the music is already playing at t = 0.
  - `M.render(variant, dur, anchor, duck=[(t0, t1)], swell=[t], silent_from, final_chord=t)` returns the bed at -20 LUFS (pre-master).
    - Ducks are -6 dB.
    - A swell is +0.55 decaying over 2.2 s, with a soft strings lift and a reverse-cymbal swell; that pass gets the payoff colour.
    - `final_chord` holds a tonic chord.
  - `M.preview(mp3)` renders a short tour.
- **ch1 (rev d, audio only):** `beach_day` with a downbeat ON the hit and ducks under every throw. All SFX + ambience unchanged.
  - The frames were re-muxed (video stream bit-identical) from the ch1c files, now archived in `<VIDEOS_DIR>\MochiAndBolt\archive\island_ch1_v3_boccherini\`.
  - Measured on the muxed files: -14.0 LUFS, TP -4.0 / -3.1 dBFS, last 0.5 s ≤ -62 dBFS; the hit is still the loudest onset (+7.5 / +9.5 dB).
  - The Minuet version of the scene is kept as `scenes/_versions/island_ch1_fish_v3c.py`.

## Chapter 2: WATER (`scenes/island_ch2_water.py`, builder B, phase 2). Step 1 (FAST stills + audio) only
- **Brief change (flagged):** the brief had Bolt dig in the MIDDLE of the island and hit salt. A real lens is THICKEST in the middle (40x the highest water table): on our island the centre's water table is 2.2 in above sea level, so fresh water runs 7 ft 5 in below it, far below a hand-dug hole. So Bolt digs (1) in the WET swash sand and (2) DEEPER a yard up the beach, where the lens is thin. Winner unchanged: Mochi.
- **Model (sharp interface, Dupuit + Ghyben-Herzberg, strip island):** h(d)^2 = W (2 L d - d^2) / (K (1 + G)), interface at -G h, G = rho_f / (rho_s - rho_f) = 1.000 / 0.025 = 40. W 0.6 m/yr recharge, K 20 m/day (medium sand), L = 40 m (an 80 m / 262 ft island); d = distance inland of the swash zone's top (x = -1.1 m). The swash zone (wet from the waves) holds sea water.
- **A hole's water:** it flows in from the wall below the water table (uniform sand), so salt = layer salts weighted by how far the hole cuts into each. Sea 3.5 %, lens 0.02 % (200 mg/L, assumed), drinkable <= 0.05 % (500 mg/L TDS, US EPA secondary standard).
- **Result (`--report`):**

| dig | who | spot | water table | salt line | hole | salt | verdict |
|---|---|---|---|---|---|---|---|
| 1 | Bolt | wet swash sand (x -0.55) | sea level | - | 1 ft 7 in | 3.5 % (70x) | SALTY |
| 2 | Bolt | 0.95 m up the beach (x -2.05) | 0.48 in above sea | 1 ft 7 in below sea | 4 ft | 1.35 % (27x) | SALTY |
| 3 | Mochi | swale behind the dune (x -5.35) | 1.00 in above sea | 3 ft 4 in below sea (= 40 in) | 2 ft 1 in (8 in into the water) | 0.02 % | FRESH |

- **Timeline (16:9, 30.7 s, 1842 f):** 0 Bolt mid-dig in the wet sand, PLAN 1 popping, meter already 3.5 % · 3.35 SALTY · 3.9-8.3 teach (x-ray up, rain soaks in, FRESH / SALT labels) · 8.4 PLAN 2, 8.9 he glides up the beach · 9.6-13.0 dig: water 10.52 (0.02 %, he smiles and keeps digging), SALT LINE 12.02 · 14.85 SALTY · 15.8 MOCHI card, 16.25 she slides off the dune, 17.0-18.5 digs · 20.35 FRESH, MOCHI 2, "One hole.", the 3 ft 4 in brace · 21.25-23.5 she floats the cup over the dune to Bolt · 24.2-30.7 why card.
- **9:16 (24.7 s, 1482 f):** EDL [0-7.6] [11.6-22.2] [24.2-30.7]; S 250, a pan (V_KEYS) per beat, horizon pinned.
- **Card:** "Fresh water floats on the sea, like ice in a glass." + "Her spot: 1 in above sea level = 40 in of fresh below." + "fresh 1.000 vs sea 1.025 g/cm3: 1 / 0.025 = 40 (Ghyben-Herzberg)" + "Bolt dug 4 ft deep: right through it, into the salt."
- **Life:** a ghost crab (x1.3) on the dune that burrows when Bolt arrives and while the cup flies over; gulls (one circling over the sea, one out over the swale and back in the teach beat). `--check` both edits: 0 overlaps (blobs, shovels, holes, heaps, cups, stamps, meter, plan cards, caption, card).
- **Sound:** the STRANDED theme `beach_day` (lib/island_music.py), a pass's bar 0 on the FRESH result, ducked under each dig and taste. Surf + breeze. Foley (own synthesis, in-scene): scoop (dry / wet), toss, seep gurgle, cup plunk, two glugs, deflate on SALTY, rain ticks in the teach, the FRESH chime (bells + sparkle + low thud) = the loudest onset (+6.4 dB 16:9, +7.0 dB 9:16). Proxies (black + AAC 384k): -14.0 LUFS both, TP -4.0 / -2.5 dBFS, tail <= -64 dBFS, audio = edit length.
- **Sources:** Ghyben (1888), Herzberg (1901), "1 ft above = ~40 ft below": [USGS Long Island fresh/saltwater](https://www.usgs.gov/centers/ny-water/science/long-island-fresh-and-saltwater-relationsinteractions). Strip-island lens: Fetter, Water Resources Research 8(5), 1307 (1972). Small-island recharge/lenses: Falkland (ed.), *Hydrology and Water Resources of Small Islands*, UNESCO (1991). Sand K ranges: Freeze & Cherry, *Groundwater* (1979). Drinkable: US EPA secondary standard, TDS 500 mg/L. Field practice (dig behind the first dune, stop when water seeps in; deeper/closer = brackish): SAS Survival Handbook (Wiseman); [HowStuffWorks](https://adventure.howstuffworks.com/survival/wilderness/how-to-find-water3.htm).

## Chapter 6: ROPE BRIDGE (`scenes/island_ch6_bridge.py`, builder A, 2026-11-07). FAST stills + audio preview; waits on the coordinator
- **Duel:** each strings one rope over a 16 ft (4.88 m) ravine and rides it in a floating sling (a clamp that grips the rope; no limbs).
  - MOCHI "pull it TIGHT": she cranks hers to 300 lb with a floating windlass.
  - BOLT "leave it SAGGY": his is 3 % longer than the span.
  - Two PLAN cards live at once, side by side (new kit keys `slot_dx`, `size_k_v`).
- **The model (honest, solved exactly):**
  - Cord: 2 mm 12-strand Dyneema (SK78), 410 daN break (922 lb), 3.8 % stretch at break (extremtextil), so EA = 108 kN, linear.
  - Knots: bowlines; a bowline in Dyneema keeps ~47 % (yacht.de tear test), so the knot fails at 1,927 N = 433 lb.
  - Cord weight (~2.6 g/m) is negligible.
  - Rider: a point load clamped at arc position s. Each segment is elastic with its own tension; horizontal balance + vertical balance = weight; `fsolve` along the crossing (continuation from mid-span).
  - Weights: `I.BLOB_MASS_KG`, Mochi 50 kg + 1 kg sling = 112 lb, Bolt 124 lb.
- **Result (`--report`):**
  - Bolt: max pull 227 lb = 1.84x his weight at mid-span (sag 2 ft 3 in, angle 17°). That is 52 % of what the knot holds: it HOLDS.
  - Mochi: the near segment reaches 433 lb 2.8 ft out (angle 12°, 3.85x her weight), so the near knot fails: SNAP. The brief's winner (Bolt) is confirmed.
  - Sensitivity: the snap needs a pre-tension of about 240 lb or more. At 200 lb her mid-span pull is 421 lb and the rope would hold. Stated in the notes; 300 lb is the assumption.
  - The near segment always carries more on the near half, so it is her start knot that fails and she swings to the FAR wall, where Bolt is.
- **The fall:** a pendulum about the far anchor (r 4.06 m, from -81°), with quadratic air drag (Cd 1, 0.3 m²) and dt 1/2400.
  - She meets the vines on the far wall 1.12 s after the snap at 8.1 m/s (18 mph); restitution 0.22.
  - Then she dangles, and Bolt's floating reel hauls her up (help 3).
- **Clock (16:9, 26.75 s):**
  - Frame 0: Mochi mid-crank, with her card popping. Bolt's card pops at 1.4.
  - Bolt rides 2.95-8.35; HOLDS at 8.6.
  - Mochi rides from 9.8, slow-mo x0.25 at c 11.8-14.0; SNAP at 12.6 (BOLT 2).
  - The camera dollies to the deep view (horizon pinned). Into the vines at 14.77; haul 16.55-19.15.
  - The why card 20.25-26.75: "Same reason power lines hang with a sag. Tight rope: 3.9x her weight. Saggy: 1.8x." plus "2 mm cord: the knot gave at 433 lb (196 kg)".
  - 9:16: EDL [0-3.4] + [7.4-end] = 22.75 s, a tracking camera at S 150 (keys `V_KEYS`), all characters inside x 0.10-0.84w.
- **Life:** two butterflies low in the ravine (they flutter out of the falling blob's way) and a frog on the far wall. `--check`: 0 / 0 overlaps with ropes, slings, riders and HUD boxes.
- **Sound:**
  - The STRANDED theme `jungle`, its pass downbeat + swell on Mochi reaching the top. It ducks under both rides; a held breath 0.3 s before the snap, then the band drops out.
  - `I.amb_jungle`; windlass / reel `sfx_ratchet`, `sfx_creak` (the cord taking load), `sfx_snap`, a whoosh, `sfx_leafy_thump`, card pops.
  - Measured (black proxy, AAC): -14.0 LUFS, TP -4.0 / -3.7 dBFS; the SNAP is the strongest onset (+16.6 / +17.0 dB).
- **Score/day:** start MOCHI 3 · BOLT 1 (assumed from ch2-5's intended winners), DAY 4 (assumed; builder B sets ch5). End MOCHI 3 · BOLT 2.
- **Sources:**
  - [extremtextil 2 mm Dyneema cord](https://www.extremtextil.de/en/dyneema-cord-extra-strong-2mm-100-dyneema.html) (410 daN, 3.8 % at break);
  - [yacht.de knot tear test](https://www.yacht.de/en/equipment/cordage/tear-test-this-is-how-much-knots-in-ropes-reduce-the-breaking-load/) (bowline on Dyneema ~47 % retained);
  - also [Practical Sailor](https://www.practical-sailor.com/sails-rigging-deckgear/lashing-for-strength/) (knots cost 30-50 %).

- **Rev (coordinator OK + one visual fix):**
  - The lens is an opaque light-cyan SHAPE with a convex bottom and a lit edge, on a dark teal/navy SALT layer.
  - A crisp interface line is visible in every shot.
  - FRESH / SALT labels are ~2x (66 px) and on from frame 0; in 9:16 they ride with the pan.
  - The teach beat has a "THE WHOLE ISLAND" sketch (true widths, depths x6 in 16:9 / x3 in 9:16, a "HERE" box). In 9:16 it takes the meter's slot.
  - The hole water takes the layer's tint (fresh above the salt line, salt below), and a dashed salt line crosses Bolt's hole.
  - Gull B moved to 9.6-15.0 s.
- **Delivered Full HD (label ch2fhd, audio p2):** `<VIDEOS_DIR>\MochiAndBolt\review\island_ch2\` (ch2_water_16x9.mp4, ch2_water_9x16.mp4, README).
  - h264 yuv420p 60 fps, 1842 / 1482 f.
  - -14.0 LUFS, TP -4.0 / -2.5 dBFS.
  - flash worst 0 / 1 (PASS); `--check` 0 / 0; the audio is exactly the video length.
  - ~1.3 min per 900-frame chunk.

## Chapter 7: TEMPLE GOLD (`scenes/island_ch7_gold.py`, builder A, 2026-11-07). FAST stills + audio preview; waits on the coordinator
- **Duel:** two gold BLOCKS (not an idol: no iconic idol staging) on two spring-loaded pressure plates.
  - BOLT "same-SIZE bag": one 3 L pouch of sand.
  - MOCHI "same-WEIGHT bag": 12 pouch-fulls of sand (36 L).
  - The two PLAN cards sit side by side.
- **The model:**
  - Gold 19.32 g/cm³, dry sand 1.60 g/cm³ bulk (loose-dense range 1.43-1.86): the ratio is 12.1x.
  - A 3 L block = 57.96 kg (127.8 lb). Bolt's same-size pouch = 4.8 kg (10.6 lb). Mochi's 36 L sack = 57.6 kg (127.0 lb): 0.6 % light, because 12 is the nearest whole scoop.
  - Each plate: a 4 kg slab on a spring (2.5 cm travel under the gold, k 24.3 kN/m), ζ 0.15, dt 1/4800. The latch trips beyond ±8 mm (load off by ~32 %).
  - A swap is a load profile on the slab.
- **Result:**
  - Bolt's plate trips 67 ms after he lifts the gold, before his pouch even lands. The slab rises up to 31.5 mm. Even a perfect same-size swap trips: the pouch is 8 % of the gold.
  - Mochi's plate moves 0.15 mm: LEVEL. Winner Mochi (as the brief says).
- **Clock (18.3 s, both edits play the whole chapter):**
  - 0: both scooping sand; Bolt's card is already popping. Mochi's card pops at 1.1.
  - They walk 2.45-3.4. Bolt's swap at 3.83, in slow-mo x0.25 over c 3.55-5.15: TRAP at 4.10, the rumble and dust start. Caption "The plate only counts pounds."
  - Mochi's smooth swap 8.5-9.3: LEVEL at 9.4 (MOCHI 4).
  - Bolt drops his gold back at 10.35: "Too late, Bolt."
  - The stone ball rolls out of the arch at 10.9 (leads into ch8).
  - The why card 11.8-18.3: "A milk carton of gold weighs 43 lb: as much as a 5-gallon water jug. Gold is 12x heavier than sand, so same size ≠ same weight." Caption "Day 5. Bolt blames the sand."
  - 9:16: a tracking camera at S 220 (x 1.0 → 3.1).
- **Life:** two moths at the right torch, a gecko on the right column, dust motes in the roof's light shaft, torch flames. `--check`: 0 / 0 overlaps with the blobs, gold, bags, pedestals and HUD boxes.
- **Sound:**
  - The STRANDED theme `temple` (minor, kalimba / vibes), with its downbeat + swell on LEVEL. It ducks under both swaps, holds its breath before the clack, then drops out.
  - Temple ambience (soft air, torch crackle, far drips). Sand pours, the latch CLACK (the loudest onset, +18.6 dB), a stone rumble, a bell on LEVEL, the ball's rumble.
  - -14.0 LUFS, TP -4.6 dBFS.
- **Assumed:** start score MOCHI 3 · BOLT 2 (after ch6), DAY 5.
- **Sources:**
  - gold density 19.32 g/cm³ (CRC Handbook);
  - [dry sand bulk density ~1.6 t/m³ (vCalc)](https://vcalc.com/wiki/Density-of-Sand);
  - [Coastal Engineering Manual, sand dry bulk densities](https://coastalengineeringmanual.tpub.com/Part_III-Chap_1/Part_III-Chap_10036.htm).
  - 5 US gal = 18.9 L.

## Chapter 3: FIRE (`scenes/island_ch3_fire.py`, builder B). Step 1 (FAST stills + audio) only
- **Duel:** Bolt's clear ICE lens (from the cooler) on char cloth vs Mochi's bow drill, both racing in real time. Winner: Bolt (as the brief guessed). He then lights her nest too, and the fish (from the cooler) cooks over his fire.
- **Lens model:** biconvex, 4 in (10.2 cm) across, R 12.4 cm.
  - Focus f = R / 2(n-1): ice n 1.31 -> 7.9 in (20.0 cm); the SAME shape in glass, n 1.50 -> 4.9 in. Ice focuses 1.6x farther.
  - Spot = sqrt(defocus D|z-f|/f, sun image z x 9.3 mrad, aberration 3 mm).
  - Irradiance = 1000 W/m2 x 0.85 (Fresnel 2 x 1.8 % + bubbles / melt film) x (D/d)^2.
- **Char cloth:** a lumped 0.3 mm sheet (250 kg/m3, 1300 J/kg K, absorbs 95 %). Losses: convection 20 W/m2K + radiation, x1.5. It glows at 349 C / 660 F (Char cloth working range 349-455 C).
- **Bow drill:** P = (2/3) mu N v = 12 W (mu 0.40, N 90 N = 20 lb, v 0.5 m/s, tip r 1 cm).
  - Half of P goes into the hearth: 19.1 kW/m2.
  - The contact heats like a semi-infinite block, dT = 2q sqrt(t/(pi k rho c)) (wood k 0.12, rho 450, c 1700).
  - The dust embers at 800 F / 427 C (Baugh, primitiveways: char must reach ~800 F to glow), after 30.9 s of bowing (practitioners: "well under a minute" with good wood).
- **Result (`--report`):**
  - PLAN 1 "hold it 5 in up, like glass": 1.5 in spot, 7 suns, the cloth tops out at 306 F -> TOO LOW.
  - PLAN 2 "lift it to its FOCUS: 8 in": it glows 1.1 s after he starts lifting, at 7.3 in (177 suns; 835 suns at the focus).
  - Her nest: 0.05 s once the lens sits at its focus over it. She had bowed 10.9 s (513 F of the 800 F she needed).
- **Timeline (16:9, 26.0 s):**
  - 0: mid-race.
  - 1.3-4.4: teach, in the tight shot: the rays run on into the sand to a focus 3 in under the cloth.
  - 4.4: TOO LOW. 5.35: PLAN 2. 6.5: IT GLOWS (BOLT 1).
  - 7.6: banner.
  - 8.7-9.9: the lens floats to her nest. 9.95: hers lights, 10.45: HE LIT HERS.
  - 12.3: the fish rises from the cooler over his fire.
  - 19.5-26: the why card.
  - Cameras: WIDE S 480 <-> TIGHT S 1400 on each nest. The horizon is pinned. The far gull is placed with the wide camera and fades out while tight (a narrow shot).
- **9:16 (20.5 s):** EDL [0-14.0] [19.5-26.0].
- **Mochi's card:** her approach runs ALONGSIDE Bolt's (a race), so it has its own slot under the meter (scene-drawn with `I.draw_plan_card`). Its verdict is ✗ when he lights hers. The strip lists Bolt's two plans.
- **Card:**
  - "Ice bends light less than glass, like a weaker magnifier: its focus is 1.6x farther."
  - "8 in, not 5 in, for the same 4 in lens."
  - "ice n = 1.31 · glass 1.50 · f = R / 2(n - 1)"
  - "At the focus: 835 suns on the char cloth."
- **Life:** a crab right of Mochi; one far gull. `--check` 0 / 0.
- **Sound:** the STRANDED theme `campfire`, with bar 0 on IT GLOWS (ducked before it).
  - Surf + breeze; a rasp per bow stroke; sizzle as the cloth heats; the catch whump + sparkle + bells (the loudest onset, +6.9 dB); fire crackle once lit.
  - Proxies: -14.0 LUFS, TP -4.5 / -4.2 dBFS, tail <= -66 dBFS.
- **Sources:**
  - Ice n 1.31: Warren & Brandt, J. Geophys. Res. 113, D14220 (2008).
  - Glass 1.50: crown glass ~1.52.
  - Sun's angular diameter 0.53 deg.
  - 1000 W/m2 clear-sky: ASTM G173 AM1.5.
  - Char cloth: Wikipedia "Char cloth" (349-455 C).
  - Bow-drill char ~800 F: [primitiveways (Baugh)](https://primitiveways.com/fire_Baugh.html).
  - Ice-lens practice: [primitiveways](https://primitiveways.com/fire_from_ice.html).
  - Wood friction 0.25-0.5 and thermal properties: USDA FPL Wood Handbook.
  - Flash temperature of a semi-infinite solid under constant flux: Carslaw & Jaeger.

## Chapter 7 (delivered) + Chapter 8: THE STONE BALL (`scenes/island_ch8_ball.py`, builder A, 2026-11-07)
- **ch7, coordinator tweaks before Full HD:**
  - A bevelled 3 L ingot: bright top, dark side, a sweeping glint, 3 twinkles, a warm light pool clipped to its slab, and the label "3 L of GOLD · 128 lb".
  - Lifted, the gold floats low and slow beside its lifter, with a strain (sweat) face.
  - Mochi's fill is a counted time-lapse: ×1 … ×12, a pour tick per scoop (+2 s). The coordinator asked for the counter; it conflicts with the CLAUDE.md "never teach counting" rule, framed as a data readout and flagged in the README.
  - Delivered to `review\island_ch7\` (20.3 s both edits; -14.0 LUFS, TP -4.5, flash 0, `--check` 0/0).
- **ch8 duel:** both chutes drop 6.6 ft (2.0 m) over 9.8 ft (3.0 m).
  - MOCHI "the SHORT straight chute" (to the right exit).
  - BOLT "the CURVED chute": a cycloid through the same two points, the brachistochrone, mirrored to the left exit.
  - Side by side from a central platform; the ball rolls out of the back arch and down Mochi's chute after her.
- **The model (honest):**
  - The blobs SLIDE on floating sled-boards (Bolt is square and cannot roll), Coulomb μ = 0.15 (assumed), with the normal force including the centripetal v²κ term; dt 1/4800 along the arc length.
  - The ball ROLLS without slipping (solid sphere, 5/7 g sin a).
  - At the straight chute's foot, the along-floor component carries on (the kink).
  - Mass cancels, so Mochi's 128 lb of gold changes nothing.
  - Frictionless check: 1.151 s straight / 0.980 s cycloid = the closed forms √(2L/g sin θ) and φ√(r/g).
- **Result (μ 0.15):**
  - Straight 11.8 ft in 1.308 s; curve 12.7 ft in 1.083 s. The curve is 7 % longer and 17 % faster (0.225 s). Winner Bolt (as the brief says).
  - Ball: 4.5 mph out of the arch, at the top edge at T 0.80 s, down her chute in 0.94 s (12.7 mph). It wedges under her tunnel's 2 ft 11 in lintel (the ball is 3 ft 7 in) 0.26 s after she is through. Closest gap 0.50 m.
  - "By a hair" = 0.26 s real (1.0 s on screen at x0.25).
- **Clock (19.42 s, both edits):**
  - 0: "Day 5. The ball wants the gold back." The cards pop (Mochi -0.1, Bolt 0.9). 1.4: the banner.
  - 2.4: push-off; the race runs in slow-mo x0.25 to 10.5, with per-lane timers and lengths.
  - Bolt down at 6.73 (✓, BOLT 3); Mochi at 7.63 (✗); SEALED at 9.52.
  - Caption "Bolt by 0.22 s. Mochi by a hair."
  - Why card 12.9-19.4: "Same reason skate ramps curve: drop steep first. The curve is 7% longer but 17% faster." Caption "Day 5. Bolt brags. Mochi has the gold."
  - 9:16: S 170, the camera follows Mochi's side (the chase). Bolt leaves the frame on the pan; his timer, card and the caption carry his win.
- **Life:** a moth at the left torch, a gecko on the wall, torches, daylight at both tunnel mouths. `--check` 0 / 0.
- **Sound:**
  - `temple` theme: ducked through the race, a held breath before the slam, a swell after.
  - `I.amb_temple` (moved to the kit).
  - The ball's rolling rumble, sled slides, the bell on Bolt's finish, and the SLAM (the loudest onset, +12.7 dB). -14.0 LUFS, TP -4.2 dBFS.
- **Assumed:** μ 0.15 (wood sled on smooth stone); the ball's corridor speed and start; MOCHI 4 · BOLT 2 → 3; DAY 5.

## Chapter 4: SHELTER vs HURRICANE (`scenes/island_ch4_storm.py`, builder B). Step 1 (FAST stills + audio) only
- **Ladder (NHC Saffir-Simpson):** Cat 1 74 -> Cat 2 96 -> Cat 3 111 -> Cat 4 130 -> Cat 5 157 mph.
  - The wind is monotone, with small upward-only gusts, so each Cat stamp is honest.
  - q = 1/2 rho v^2, rho 1.225: 14 -> 24 -> 31 -> 43 -> 63 lb/ft2. Cat 5 pushes 4.5x harder than Cat 1.
- **Bolt's flat roof:** 1.5 x 1.6 m.
  - Net uplift 1.08 q A: ASCE 7 MWFRS flat roof Cp -0.9 outside + GCpi +0.18 inside (enclosed).
  - Held by 4 vine lashings of 1.1 kN (250 lb, ASSUMED) + its 40 kg.
  - The roof goes at **122.9 mph (Cat 3)**.
  - Flight: the attached-flow suction for ~0.1 s, then a flat plate (lift 0.5 sin 2a, drag 1.2), shown at SLOW-MO x0.1 for 2.4 s (the whole world slows: `anim_t`).
  - Then the walls fold (no bracing).
- **Mochi's A-frame:** 2.0 m base, 1.1 m ridge, 48 deg.
  - Panels: windward +0.4, leeward -0.6 (ASCE 7 steep roof), inside +0.18.
  - The panel resultant minus her 60 kg is held by **6 lashings** (the same 1.1 kN vines, to two palm trunks).
  - Demand at 157 mph: 5.72 kN of 6.6 = **87 %**. It would fail at 168 mph (stated in the docs, not on screen).
  - Six vs four ties is part of her plan ("tied to palms"), not a hidden advantage. Same vine, same strength.
- **Help 1:** Bolt glides over, she swings the leeward flap out, he squeezes in. Caption: "Mochi lets him in."
- **Timeline (60.0 s):**
  - 0: Cat 1, mid-storm; the BOLT card pops; MOCHI's card is in her slot.
  - 3.0: banner. 7.5: Cat 2. 8-13: teach (suction arrows, labels in the sand).
  - 14.6: Cat 3. 22.03: ROOF OFF ✗ (slow-mo to 24.4). 24.7: the walls fold.
  - 25.1-26.7: he runs. 26.0-28.4: the flap.
  - 36.6: Cat 4. 47.0: Cat 5. 49.0: STILL STANDING ✓ (MOCHI 3).
  - 53.5-60: the why card, top-left sky.
- **9:16 (25.5 s):** EDL [0-3.5] [19.0-29.0] [44.5-50.0] [53.5-60.0]; S 380 pans hut -> A-frame.
- **Card:**
  - "Wind pushes with speed SQUARED, like a hand out a car window: twice as fast, 4x the push."
  - "Cat 5 (157 mph) pushes 4.5x harder than Cat 1: 63 lb on every ft2."
- **Score:** MOCHI 3 · BOLT 1 after ch4 (matches builder A's ch5 assumption).
- **Life:** storm debris (leaves, twigs) high in the frame, kept clear of the flying roof. `--check` 0 / 0.
- **Sound:** the STRANDED theme `storm` (bar 0 on the roof), a wind bed whose level and brightness follow the mph, creaks quickening with the roof's load, rain.
  - Before the tear the bed dips 70 % for 0.3 s. The TEAR (cracks + rip + whump + 55 Hz boom) is the loudest onset (+11.3 dB 16:9, +7.0 dB 9:16).
  - Proxies: -14.0 LUFS, TP -3.8 / -3.8 dBFS, tail <= -66 dBFS.
- **Sources:**
  - NHC Saffir-Simpson scale.
  - ASCE 7-16 Ch. 27 (MWFRS Cp; GCpi +-0.18 enclosed).
  - Air density 1.225 kg/m3 (ISA).
  - The 1.1 kN lashing is an assumption (natural-fibre cordage + knots); the docs say so.

- **ch4 rev (coordinator OK + 2 fixes):**
  - "6 ties" is on her card and the meter ("BOLT's 4 ties" / "MOCHI's 6 ties").
  - The why card adds: "Same vine: with 4 ties, hers would still outlast his by 16 mph (138 vs 123)."
  - The A-frame's near poles are drawn behind the blobs (+ a 25 % ghost on top).
- **Delivered Full HD** to `review/island_ch4/`: -14.0 LUFS, TP -3.8 / -3.8 dBFS, flash 0 / 0, `--check` 0 / 0.

## Chapter 5: QUICKSAND (`scenes/island_ch5_quicksand.py`, builder B). Step 1 (FAST stills + audio) only
- **The jungle starts:** DAY 4, morning. Unscored (MOCHI 3 · BOLT 1 stays). Help 2: Mochi talks him out.
- **Physics (Khaldoun, Eiser, Wegdam & Bonn, "Liquefaction of quicksand under stress", Nature 437, 635 (2005), doi:10.1038/437635a; Bonn's numbers as quoted by National Geographic 2005):**
  - Quicksand ~2 g/mL vs a person ~1: you float, about waist-deep.
  - Pulling a foot out at 1 cm/s takes about the force that lifts a medium car.
  - Escape by wriggling slowly to let water in.
- **Model:**
  - Bolt 55 kg (`I.BLOB_MASS_KG`), density 1.0, on his true cross-section: his bottom floats 0.30 m (1 ft) under = 50 % of his height.
  - Thrashing liquefies the sand: an overdamped sink to that line, no further.
  - The pull force scales with speed: F = F_car x v / (1 cm/s). F_car = 1,500 kg x g = 14.7 kN (3,308 lb). The water must flow into the gap he leaves (Darcy), so the drag grows with the speed. This linear law is OUR model; the paper gives only the 1 cm/s point.
  - The vine holds 1.1 kN (247 lb), the same vine as ch4.
  - Yank at 4 in/s: 147 kN (33,081 lb) needed -> SNAP.
  - Mochi's slow pull at 0.67 mm/s (1.6 in/min, 223 lb): 0.30 m takes 7.9 min, shown TIME-LAPSE x79.
- **Timeline (16:9, 36.0 s):**
  - 0: Bolt mid-thrash, PLAN 1 "THRASH his way out" popping.
  - 3.0: STUCK AT HALF. 4.2: banner.
  - 4.4-9.4: the myth-bust, "You can't actually SINK in quicksand." (the float line + "2x his density: it holds him UP").
  - 9.8: PLAN 2 "YANK out FAST with a vine". 11.45: SNAP (the frog hops).
  - 14.3: "Mochi talks him out.", MOCHI card "wiggle SLOWLY, let water in".
  - 17-20: slow wiggles, water seeps into the gap. 20-26: the slow pull (TIME-LAPSE x79 · 8 min).
  - 26.0: OUT. 29.5-36: the card.
- **9:16 (27.0 s):** EDL [0-6] [10.9-13.3] [14.4-27] [30-36]; S 315 keeps both blobs in the safe box.
- **Card:**
  - "Myth: you can't actually sink in quicksand."
  - "It's 2x denser than you, so you float half in, like a ball in a pool."
  - "Pulling out at 1 cm/s takes about a medium car's weight (Bonn et al., Nature 2005)."
  - "Slow wiggles let water in: that is the way out."
- **Life:** a frog right of the pit (blinks, hops at the snap); butterflies and falling leaves in the band under the HUD (the left ones leave before the card). `--check` 0 / 0.
- **Sound:** the STRANDED theme `jungle` (bar 0 + swell on OUT), a soft insect hum + sparse two-note bird calls, squelches per thrash, a deflate on STUCK, the vine SNAP, slow squelches, OUT (squelch + sparkle + bells) = the loudest onset.
  - Proxies: -14.0 LUFS, TP -4.5 / -3.2 dBFS, tail <= -69 dBFS.

- **ch5 rev (coordinator OK + honesty tweak):** the modelled forces show rounded: "PULL at 4 in/s: ~33,000 lb (≈ 10 cars)" and "~220 lb", with "(model: force grows with pull speed)". The exact figures (33,081 / 222.6 lb) are in the README. The snapped vine end and the tie point were moved to his side, clear of his face.
- **Phase 3 prep:** `tools/build_island_long.py` (chapters -> one video, tide-wipe + DAY badge transitions, bridge music, YouTube chapter list, end-card hook). The continuity table is in `review/island_phase2_B/ASSEMBLY.md`.

## ch9 RAFT HOME (`scenes/island_ch9_raft.py`, builder A)
- **Sim (VPP):**
  - Hull: C_D·A 0.10 m² ×1.3 (leeboard), seawater 1025 kg/m³; a wind-driven current of 3 % of the wind speed.
  - Sail: 3 m² (CL = 2π·0.6·α up to 1.2, CD = 0.05 + 0.2·CL²), 0.5 m² windage, best-VMG heading, tacks every 300 m sailed at 20 s each (half first leg, so she zig-zags either side of the line).
  - Paddle: 30 W useful power (thrust = P/v) against hull drag + headwind on 0.8 m².
- **Results:**
  - Wind 10 → 20 kn over 50 min, 1.8 km (1.1 mi) straight upwind.
  - The sail beats the paddle above ~15.4 kn (27.2 min, 34 % of her trip); she passes him at 54.0 min.
  - Harbour mouth at 79.1 min with Bolt 416 m behind; tow VMG 0.52 kn; home at 109.4 min.
  - At 20 kn: VMG 0.98 kn at 48° vs the paddle's 0.31 kn. Bolt only loses ground below ~18 W.
  - The gold (3 L, 128 lb) sinks one raft 0.66 in, 0.33 in each after the split.
- **Look (hero view, coordinator 2026-11-07):**
  - A side-on sea: Mochi on the far lane, Bolt on the near one.
  - The real gap is tanh-squeezed on screen; an "ahead by N m" readout carries the honest metres.
  - Map inset at true scale, with compact wind / gain strips.
  - The skyline grows on the horizon and the island shrinks.
  - The lanes are spaced so Mochi's boards and Bolt's head stay ≥ one raft height apart, including waves and tilt (`lane_clearance` in `--check`).
- **Lib:** `hud(word=...)`, `team="✓"` drawn as a check, and `plan_layout` honours `view.plan_over`.
- **Sound:** `raft_finale` + surf + a breeze that grows with the wind; holds before the crossover / pass / finish. The finish is the loudest onset (+10 dB).

## Series spine (`lib/island_spine.py`, builder A)
- One table: chapter -> score in / out, day, HUD word, TEAM, winner. V2 (12 chapters) is the default; `NF_SPINE=v1` = the delivered 9-chapter cut (proved pixel-identical: 56 / 56 stills).
- ch9's final card reads `SP.final()`: score, TEAM, days, duels. New chapters pass `SP.score(key, won)`, `SP.row(key)["day"]` and `SP.word(key)` to `I.hud`.
- **4K-pass scene changes (`SP.FOURK_PASS`):** ch6's sky goes from tod 0.95-1.0 to ~1.35-1.45 (afternoon), to match DAY 4 AFTERNOON.

## ch3b COCONUT + ch8b SIGNAL (builder A)
- **ch3b:**
  - Palm: a 49 ft cantilever with a 400 kg crown, swaying at 0.41 Hz (zeta 0.03).
  - Mochi's pumped vine tug (250 N, in phase): ±13 in of crown sway, 10x a steady pull; the nut feels 1.2x its weight -> HOLDS.
  - Bolt: rocks at 11 % a throw; the hit lands on #8 (seed 295) and jerks the stalk 6.4x -> BOLT.
  - The ripe-stalk ~3x threshold is an estimate (no data found) and is labelled "est.".
  - On screen: the palm's middle is cut out (break marks + a stated height); ghost crowns + a "±N in" arc show the rhythm build.
- **ch8b:**
  - The ship is 6 mi out; line of sight to its bridge is 12.7 mi.
  - Mochi: 0.21 arcmin (5x below acuity); her shout arrives at -28 dB.
  - The 3x5 in mirror: 0.05 lux through haze = ~290x Venus. The ship answers in Morse "CITY UPWIND" -> BOLT, which sets up ch9.
  - Every flash is a small spot (flash_check PASS).

## ch5c MONKEYS (`scenes/island_ch5c_monkey.py`, builder B). FAST stills + audio only
- Mechanic: a monkey on a branch 11 ft 10 in (3.6 m) up throws mangoes at 20 mph (9 m/s) on the low arc, aimed by bisection, led on a walking target.
  Throw noise: elevation sd 2.5 deg, azimuth sd 1.2 deg. Gravity turns an elevation error into RANGE, so a miss is long or short
  (landing sd 14 in along the line, 6 in across: 2.4x). Hit radius 0.35 m.
- Roles (v3): MOCHI backs straight away along the line at a walk (1.2 m/s) = bonked; BOLT steps 2 ft SIDEWAYS as it throws = clear.
  Monte Carlo, 4000 throws each: back away 69 % hit, side-step 0.9 %. Seeded run (SEED 11): Mochi 3/3, Bolt 0/3. Winner BOLT.
- 27.13 s both edits (1628 f); first throw at SLOW-MO x0.5; teach beat (2-sd landing ellipses) c 2.8-8.4; OUT OF MANGOES c 18.63; card 20.63.
- Layout: OView (K 0.42, skew 0.30). 16:9 S 175; 9:16 S 115, ox 112: monkey at 0.10w, Mochi's last step at 0.84w (--check gates it).
- Lessons: Mochi's BONK sits beside her toward the monkey (above her is Bolt, read as "Bolt bonked"); 9:16 teach labels stack
  above-left of Mochi (below 0.71h is the Shorts UI; above Bolt is his MISS stamp); the parrot stands on the far floor.

## ch8c TREE FELLING (`scenes/island_ch8c_felling.py`, builder B). FAST stills + audio only
- Day 6 MORNING, before ch9; spine 6·7 -> 7·7, winner MOCHI. Two palms, one raft spot (dashed on the sand from frame 0).
- Sim: a rigid trunk about its pivot, theta'' = g (m_t L/2 + m_c L_c) / (m_t L^2/3 + m_c L_c^2) sin theta, dt 1/240.
  Palm 4.2 m trunk + 0.30 m stump (15 ft), 8 in, 750 kg/m^3 -> 99 kg + 35 kg crown, COM 8 ft 7 in up; lean 4 deg (COM 7 in past the base).
- Bolt, flat cut (70 % at frame 0): falls along the lean, meets her ridge (1.1 m) at 77 deg after 2.05 s, the A-frame collapses.
- Mochi: notch 70 deg open face, 1/5 deep; back cut leaves a hinge 0.8 in (10 %) x 6.3 in (80 %); aimed 35 deg off the lean
  (plane lean 3.3 deg, side 2.3 held by the hinge); hinge tears at 70 deg (2.09 s), down at 2.28 s (shown at SLOW-MO x0.5).
  Aim error one seeded draw, sd 1.5 deg: -1.0 deg (2.8 in at the top).
- Sources: Husqvarna directional felling (hinge 10 % thick, 80 % long; open-face notch 70 deg+), OSHA logging eTool (hinge),
  US Forest Service felling guide (aim within ~45 deg of the combined lean); palm hinges are fibrous and steer less (arborist forums).
- Layout: mirrored oblique view (world +x runs LEFT: her palm left, the A-frame right), K 0.75 so ground angles read (35 deg);
  16:9 S 140; 9:16 S 105 with a camera pan (his palm + A-frame -> her palm + spot). The close-up inset shows the kerf / notch /
  hinge in the fall plane and the top block turning on the hinge during the fall.
- 26.57 s both edits (1594 f). --check 0/0 (HUD vs blobs + crowns, 9:16 safe box + UI zone, nobody under a trunk).

## ch5d CLIFF JUMP + ch7b TRAP FLOOR (builder A, v3)
- **5d:**
  - 35 ft; both hit at 32 mph.
  - Von Karman water entry: Bolt's flat face gets ~420 g in ~1.5 ms (air cushion ~3 ms, est.); Mochi's round bottom ~63 g over ~12 ms. Same final speed.
  - Slow motion ×1/100 with a live force graph + a wetted-width bar. The Short ends on the result.
- **7b:**
  - 6×10 floor, p = 1/4 a tile (a fired trap is spent).
  - Switching adds tiles: 1,000 floors give straight 2.59 / 10, switching 3.21 / 13.2 (per tile ~0.25 both).
  - Seed 5 is the one run shown, matching the averages.
- **Spine v3 (16 chapters):** 1 2 3 3b 4 5 5b 5c 6 5d 7b 7 8 8b 8c 9. MOCHI 8 · BOLT 7 · TEAM ✓, 15 duels. The day is asserted never to run backwards.
- **ch3b v3:** one continuous cantilever trunk (sway drawn ×4) + magnifiers.
- **ch9 v3:** a fixed skyline; the gold split on the pier.
