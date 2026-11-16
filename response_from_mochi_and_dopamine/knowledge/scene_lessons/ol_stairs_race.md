# ol_stairs_race (DopamineEXE, channel 2)
- Batch 57 (docs/BRIEF_batch57.md); **v2 batch58** (docs/BRIEF_batch58.md). Five same-size balls (rubber, ping-pong, glass, steel, wood) roll off the top landing onto **45 deep stairs**; honest per-material bouncing; every impact nudges a ball sideways a little and past the stair's edge it falls off; glass cracks on hard landings and shatters. Seed 70: **rubber OFF THE EDGE at step 4 (1.69 s)**, **ping-pong OFF at step 21 (5.28 s)**, **glass leads alone 5.3-11.2 s and SHATTERS on landing at the bottom (11.25 s)**, **wood falls OFF the edge just past the last step (12.47 s)**, **steel (last for most of the race) WINS at 15.35 s**. Lead changes: wood, glass, ping-pong, glass, ping-pong, glass, wood, steel (8).
- Caption (baked, `--cap`; `--cap ''` = base): `5 balls race down ^45 STAIRS^…|only ~ONE~ makes it` (built from NB / NSTEP).
- Delivered: `<VIDEOS_DIR>\DopamineExe\review\ol_stairs_race.mp4` (**v3: picture-in-picture**, Full HD, seed 70, label fhdv3c, **17.55 s, 1053 frames**). v2 archived as `archive\ol_stairs_race_v2.mp4` (`--pip 0` reproduces it), v1 as `archive\ol_stairs_race_v1.mp4`; the v1 scene file is at scratchpad `bD58/ol_stairs_race_v1.py`. No 4K yet.

## v3 (2026-10-30, batch60): a picture-in-picture of 2nd and 3rd place
- Owner on v2: "while we watch glass lead, a small screen in the corner to watch the other two?"
- **Sim, main camera, HUD, sound unchanged** (audio wav bit-identical to v2). New: a framed inset (340 x 272, white 3 px frame, rounded) showing **the same world through a second camera**: same zoom, drawn at 0.42 scale (balls ~27 px), its own Gaussian follow (0.3 s) of the targets, a hard cut on a jump. Name tags at 18 px over the inset's balls (no overlaps), a header "● 2ND & 3RD PLACE" (red dot = a live camera).
- **When:** only while **2nd place is out of the main shot** (the main camera shows the leader alone); the targets = the chasers that are out of it (2nd, + 3rd if within 0.62 inset-widths of it). Dilated ±0.35 s, a 0.2 s fade, runs < 0.8 s dropped, blinks off ±0.15 s over its own cuts. The header names the targets' places at that frame (during the fade-in at 4.93 s steel and wood are still "3RD & 4TH PLACE"; at 5.28 s ping-pong goes off and they become 2nd & 3rd); no header while fading out.
- **Where:** bottom-left of the view (x 112-452, y 940-1212): under the treads, the stair body, where no ball ever is (checked over every frame: 0 balls under it). When the finish mat comes into the shot (it would cover "LAND HERE = FINISH"), it fades out (10.18 s) and comes back at the **top right** (x 563-903, y 352-624, empty sky at the bottom of the stairs) once nothing races there: 11.42-12.65 s (steel, 2nd behind wood). A crash note that would overlap the top-right inset is drawn under its crash instead.
- **Timeline seed 70:** inset on 4.93-10.18 s (steel + wood, from 8.8 s wood + steel) and 11.42-12.65 s (steel, "2ND PLACE"; wood falls off at 12.47, the inset fades). So while glass leads alone (5.3-11.2 s) the inset shows the other two for 4.9 s of 5.9.
- Proof-read on screen: "2ND & 3RD PLACE", "3RD & 4TH PLACE" (fade-in only), "2ND PLACE", tags "WOOD" / "STEEL": the places are computed live from the race order (step, then distance), so they are literally true at each frame.

### Checks v3 (encoded Full HD, fhdv3c)
- h264 High yuv420p 1080x1920, 60 fps, 1053 frames, 17.55 s. **flash_check PASS** (0 flashes, mean lum 0.0197).
- **-14.00 LUFS**, peak -4.52 dBFS, last 0.5 s digital silence (= v2, wav bit-identical). Seam (check_clip) 1.575 = v2 (the camera's own motion).
- Frames read from the mp4 at 0.05, 5.0 (fade-in "3RD & 4TH PLACE"), 6.5, 7.0, 8.0, 9.0, 10.1, 11.3, 11.9 (top-right inset, steel "2ND PLACE"), 12.55 (fade-out), 15.4, 17.5 s; stills at 3.6, 5.0, 5.3, 5.5, 7.0, 9.3, 10.4, 10.7, 11.5, 11.8, 12.3, 12.5 s. A scan of every frame: 0 racing balls under the inset at either position.
- Side safe zone: inset x 112-452 (bottom left) / 563-903 (top right), inside 108-907.

### Flags v3
`--pip (1; 0 = v2) --pipw (340) --piph (272) --pips (0.42) --pipx (112) --pipy (940)`.

### Doubts v3
- 10.18-11.42 s (the last steps before glass shatters, and the shatter itself): no inset, the finish mat is where it lives; 2nd/3rd show as the left-edge markers there (as v2).
- At ~5-6 s and ~8.8 s steel and wood are side by side in the inset (their tags stack above/below).
- The inset briefly covers the step numbers on the stair body (decoration).

## v2 (2026-10-29, batch58)
- Owner on v1: "so fast I can't even figure out what was happening and what kind of balls there were; better to watch up close, wider steps, more kinds of balls."
- **Close camera:** fixed zoom 1.0, balls r 32 = **64 px across** (v1 ~23 px at zoom 0.55). It follows the leader (at most ~70% across) and frames any ball racing within 0.6 view-widths behind it. A crash it is watching (all 4 in seed 70) holds the shot 0.9 s (`--ehold`); a jump wider than 0.85 x the view is a **hard cut**, not a pan (cuts at 12.15 s to wood, 13.38 s to steel). Balls behind the shot: an arrow + icon + step at the left edge.
- **Wider, deeper steps:** W 150 x H 60 (v1 64 x 40; 2.3 ball diameters deep), 45 steps (v1 100), stair 460 wide, oblique depth KX 0.45 / KY 0.50 (treads read as deep blocks; risers drawn darker). g 3000 px/s^2 (the motion reads like ~20 cm balls on a grand outdoor staircase). Push off the landing 600 px/s.
- **5 labelled balls:** a name tag on every ball (greedy, no overlaps), HUD chips with a ball icon, name and step (OFF / BROKE + red X), the track with mini-ball icons, a glass crack bar + %. Looks: rubber coral + spin seam, ping-pong off-white + moulding seam, glass translucent cyan + cracks, steel chrome, wood tan + turning grain rings.
- **Slower:** 17.55 s (v1 9.42); the winner rolls ~3 steps/s.
- **Finish = landing at the bottom intact:** the gold line is the stair foot; the run-out mat glows gold with "LAND HERE = FINISH". A ball in the air past the last step still counts 44 (the counter shows 45 only on landing). Glass flies over the line and shatters on touchdown; wood drifts off the edge while in the air over the mat.

## World / physics v2 (scenes/ol_stairs_race.py `simulate`, seeded)
- Contacts as v1 (tread / riser / nose segments, restitution, friction coupling spin, 1% tangential loss per impact, slow contacts roll), dt 1/480.
- Materials (e, mu, sideways kick per unit impact speed, relative density): rubber 0.85 / 0.90 / 0.030 / 1.1; ping-pong 0.88 / 0.35 / 0.030 / 0.08 + **air drag** (terminal speed 2600 px/s, a = g (v / vt)^2: it floats); glass 0.70 / 0.30 / 0.012 / 2.5; steel 0.45 / 0.25 / 0.010 / 7.9; wood 0.55 / 0.50 / 0.016 / 0.7.
- Ball-ball hits: 3D spheres, impulses by mass, the pair's lower restitution (none in seed 70: the start lanes are 90 apart and the race spreads).
- Glass cracks by (vn^2 - 650^2) / 2e7 per impact harder than 650 px/s; shatters at 100%.
- Off the edge: |z| > 230 (the stair half-width). Start lanes back -> front: rubber, ping-pong, glass, steel, wood.
- Honest-physics note: on flat treads a low-bounce ball keeps its horizontal speed (it plops one step at a time: steel ~3 steps/s); bouncy balls gain speed off the step noses and run away, so the race spreads.
- **Seed choice:** 400 seeds x 2 configs scanned (scratchpad `bD58/search3.py`) for exactly one finisher with all 4 others out before it, all 4 crashes inside the camera's shot, the widest gap between events, 13-16.5 s. Seed 70 = the only one with all 4 crashes watched, 8 lead changes and glass shattering (not just falling off). Seed 313 (12.5 s, 2+ balls in view 67% of the time, but glass falls off instead of shattering) is the shorter alternative.

## Timeline v2 (clip s, seed 70)
- Steps at s: rubber 0, 2, OFF at 4 (1.69 s); ping-pong 0, 2, 6, 10, 14, 19, OFF 21 (5.28 s); glass 0, 2, 6, 10, 14, 18, 22, 25, 30, 36, 42, SHATTERS at the bottom (11.25 s); wood 0, 2, 5, 8, 10, 13, 15, 18, 21, 26, 30, 36, OFF over the mat (12.47 s); steel 0, 2, 5, 8, 11, 14, 17, 20, 23, 26, 29, 32, 35, 38, 41, 44, **45 at 15.35 s**.
- Glass crack at s 0, 0, 2, 11, 19, 26, 43, 51, 58, 68, 80, 96%, 100%.
- Hold 1.6 s on the winner at the line, 0.6 s dissolve into frame 0 (the five balls dropping onto the landing).

## Sound v2
- Music: the same Rossini overture, now the Allegro from its first bar: **score beats 98-132** (the strings' E pedal, the violins' theme from ~beat 106, the E chord played major = STEEL WINS) at **133.3 bpm** (v1 beats 110.5-132 at 180 bpm): calmer, to match the slower race.
- SFX per landing (>= 110 px/s, >= 30 ms apart per ball), pitched to the score: rubber "bop", steel clink, glass tink, **wood: a dull hollow tok**, **ping-pong: the light "pik"**; crack ticks; the shatter's 10-note tinkle; 3 falling notes in the ball's own voice when it goes off the edge; a bell at the finish. A ball far off screen sounds at 45%. After the last crash the winner's landings **walk up the chord** (louder each step) into the finish.

## Checks v2 (encoded Full HD, fhdv2)
- h264 High yuv420p 1080x1920, 60 fps, 1053 frames, 17.55 s. **flash_check PASS** (0 flashes, mean lum 0.019).
- **-14.00 LUFS**, peak -4.52 dBFS, last 0.5 s digital silence. RMS/s (audio test) -17.1, -16.5, -17.7, -17.1, -17.9, -18.9, -18.8, -19.7, -18.9, -19.1, -17.8, -17.0, -18.4, -18.6, -17.6, -16.1 (finish), -18.1, silence. SFX events/s 16, 15, 12, 11, 9, 14, 9, 8, 8, 8, 7, 17 (shatter), 7, 3, 3, 2; 149 events.
- Seam (check_clip) mean |delta| 1.575 = the clip's own motion (frame-to-frame 1.18-1.49 at the start and end: the camera moves over high-contrast step edges); last frame = frame 0 (read).
- Side safe zone: the camera keeps the racing balls inside x 108-907 (VIEW_X0/X1); tags clamp to it; the HUD spans 170-846. Balls 64 px across at every frame.
- Frames read from the mp4 at 0.05, 1.7, 1.75 (full res), 4.2, 5.3, 9, 11.25, 11.3, 11.6, 12.5, 13.5, 15.4, 17.5 s; full-res stills at 0 (start: 5 tagged balls), 3.0 (HUD + tags), 5.0 (HUD crop).
- At 12.5 s the wood ball is still drawn (fading over 1 s) as it falls just past the mat's side edge, so for a moment it looks like it is on the mat; its chip already says OFF and "OFF THE EDGE! WOOD" is up.

## Doubts v2
- **5.3-11.2 s shows only glass** (its crack meter climbing), with steel and wood as left-edge markers 10-20 steps back: honest physics spreads the race (the bouncy balls run away). The camera follows the leader, so every crash is in shot, but a close view cannot hold all five after ~3 s.
- **SFX/s fall** (16, 15, 12, 11, 9, 14, 9, 8, 8, 8, 7, 17, 7, 3, 3, 2): balls drop out and steel lands once per step; the drama climbs instead (shatter 11.25, wood 12.47, win 15.35) and the winner's notes climb.
- Glass passes over the gold line in the air and shatters on landing: the rule ("LAND HERE = FINISH") is on the mat, but a viewer may argue glass "crossed first" (comment bait).
- The winner is steel again (as v1); here it comes from last to first.
- 17.55 s is long for the channel's 9-13 s rewatch data; the brief asked ~14-18 s.

## Flags v2
`--seed (70) --label --cap --still --frame a,b --dry --audio --sound 0 --sfx (0.55) --fin (2.0) --hold (1.6) --search a b`. World `--w (150) --h (60) --nstep (45) --g (3000) --rb (32) --zw (230) --lane (90) --v0 (600) --vtpp (2600) --order (rubber,pingpong,glass,steel,wood) --tmax (26)`. Materials `--er/--ep/--eg/--es/--ew --kr/--kp/--kg/--ks/--kw --crackv (650) --crackk (2e7)`. Camera `--zoom (1.0) --kx (0.45) --ky (0.50) --ehold (0.9) --cutx (0.85) --camsig (0.40)`. Music `--sb0 (98)`.

## Upload draft v2
- Titles: "5 balls race down 45 stairs… only ONE makes it 🏁 #satisfying #physics #shorts" (77 chars) · "Rubber, glass, steel, wood, ping-pong: who survives 45 stairs? 🏁 #satisfying #physics #shorts" (93) · "The glass ball was winning… then it hit the bottom 💥 #satisfying #physics #shorts" (81).
- Pinned comment: "glass led for 6 seconds and smashed on the very last landing, then wood fell off the edge… which one were you betting on?"

# v1 notes (batch57: 3 balls, 100 steps, 9.42 s; superseded by v2; flags/physics below are v1's)
- Batch 57 (docs/BRIEF_batch57.md). A rubber, a steel and a glass ball are dropped onto the top of 100 stairs (side view, the camera follows). Honest bouncing per material; **rubber** bounces high and drifts sideways until it flies **OFF THE EDGE** (step 31), **glass** cracks at every hard landing and **SHATTERS at step 76 while leading**, **steel** (low, steady) wins at 7.21 s. Lead changes: rubber -> steel -> rubber -> steel -> glass -> steel.
- Caption (baked, `--cap`; `--cap ''` = base): `3 balls race down ^100 STAIRS^…|only ~ONE~ makes it`.
- Delivered: `<VIDEOS_DIR>\DopamineExe\review\ol_stairs_race.mp4` (Full HD, seed 39, label fhd3, **9.42 s, 565 frames**). No 4K yet. Scratch: `output/ol_stairs_race_fhd*_v0_9x16.mp4` (an earlier camera that lost the airborne leader).

## World (y up; a step = 64 x 40 px; logical 1080x1920)
- Oblique side view: the front face of the staircase (dark body) + every tread as a coloured parallelogram receding up-right (depth 2 x 100 px); tread colour runs teal -> blue -> violet -> rose down the 100 steps (S 0.42), every 10th brighter with its number on the riser; white edge lines. The floor after step 100 is a dark run-out mat with a gold "100 · FINISH" line.
- Balls r 18 (drawn x1.15): rubber coral with a spin seam, steel chrome, glass translucent cyan with white crack lines that grow with its crack level. Name tags (rubber below, steel above, glass right).
- Camera: frames every ball still racing (x and y, + the stairs under them) and, for 0.9 s, where one broke or fell off; zoom 0.55-1.0; if they don't fit, the leader first (kept in frame even high in the air); Gaussian-smoothed 0.55 s. After the finish it frames the finish line + steel on the mat.
- Events on screen: "OFF THE EDGE!" (coral, rises and fades) where rubber leaves the stairs; "SHATTERED!" + 26 glass shards + a thin ring where glass breaks. Finale: gold sparkles at the finish line, steel gets a gold ring.
- HUD: y 1286 a race track 0-100 (ticks every 10) with the 3 coloured dots (grey X when out) and the gold finish from frame 0; y 1348 three chips "RUBBER n / STEEL n / GLASS n" (OFF / BROKE) + glass CRACK % bar; counter y 1500 = the leader's step "n/100" + "<NAME> LEADS" -> "STEEL WINS!" (gold). Watermark DOPAMINE.EXE 35%.

## Physics (scenes/ol_stairs_race.py `simulate`, seeded)
- g = 5333 px/s² (= 9.8 m/s² at 1.84 mm/px: a model staircase, steps 11.8 x 7.4 cm). Fixed dt 1/960. Each ball: position, velocity, spin. Contacts with the tread / riser / nose segments: normal impulse with the material's restitution, tangential impulse up to mu x normal (solid sphere, spin couples to the slip: m_t = 2/7 m), a small tangential loss per impact (beta 0.99), slow contacts (< 60 px/s) roll.
- Materials: rubber e 0.86 mu 0.90; steel e 0.42 mu 0.25; glass e 0.70 mu 0.30. Sideways: every impact adds a random sideways kick ∝ impact speed (rubber 0.025, glass 0.008, steel 0.008) and damps the old one; |z| > 100 px (the stair half-width) = off the edge. Lanes start at z ±40 / 0 (symmetric; the render mirrors depth so rubber falls off the FRONT).
- Glass cracks by (vn² - 700²) / 2.5e7 per impact harder than 700 px/s; shatters at 100%.
- All three start at rest-ish over the top landing (vx 600 ± 3%, 70 px up). First impact at 0.15 s.
- Seed choice: 400 seeds scanned for steel wins + rubber off the edge (step >= 30) + glass shatters (step 40-98) + finish 7-11 s; sorted by the widest gap between the running balls (camera can frame them all); seed 39 = gap <= 10.9 steps, 7 lead changes, glass leads 5-6 s and breaks in front.

## Timeline (clip s, seed 39)
- Steps at s: rubber 0, 6, 15, 29, **off at 31 (3.11 s)**; steel 0, 7, 16, 25, 34, 48, 66, 97, **100 (7.21 s)**; glass 0, 6, 12, 19, 27, 51, **shatters at 76 (6.02 s)**. Glass crack 10, 24, 39, 53, 89% (4.6-6 s), 100%.
- Leader at s: r, s, s, r, s, g, g, s.
- **7.21 s** steel crosses the finish = the cadence; hold 1.6 s on the mat, 0.6 s dissolve into frame 0.

## Sound
- **Music played as music:** G. Rossini, "The Barber of Seville" overture (1816; d. 1868, PD), the Allegro: score beats 110.5-132 (the E-minor violin theme over the strings' driving pulse) to the E chord at beat 132, played E major (Picardy third) = STEEL WINS. Steady **180 bpm** (the MIDI's own 175). Source: midiworld.com `barbero.mid`, saved at `<SOUNDFONTS_DIR>\scores\rossini_barber_overture\` + SOURCE.txt. Not on any used list; not kid-coded; not banned.
- Arrangement: violins (+ strings), 2nd violins, viola, cello, bass, flute, oboe, clarinet, bassoon, horns from the score; timpani roll into the finish. Finish = E-major strings tutti + brass, trumpets, harp roll, falling celesta, timpani E, a bell.
- SFX per bounce (>= 120 px/s, >= 30 ms apart per ball), pitched to the score: rubber a round low "bop" (E3-D4 register), steel a bright metal clink (G5-G6), glass a glassy tink (C6-C7); a dry tick on every crack; a 10-note falling glass tinkle on the shatter; three falling bops as rubber drops off; a bell at the finish. Gain 0.10-0.32 by impact speed.
- `level_bed` (+4 dB crescendo, cadence +6 dB), `audio.master(peak_db=None, reverb=0.5)`, last 0.6 s digital silence.

## Checks (encoded Full HD)
- h264 yuv420p 1080x1920, 60 fps, 565 frames, 9.42 s. **flash_check PASS** (0 flashes).
- **-14.00 LUFS**, peak -4.26 dBFS, last 0.5 s digital silence. RMS/s (audio test): -17.3, -17.2, -18.1, -17.9, -17.9, -20.0, -17.9, -16.1 (finish), -21.3, silence. SFX events/s 12, 9, 8, 10, 8, 2, 15 (shatter), 1.
- Seam (check_clip): mean |Δ| **1.41** = the clip's own frame-to-frame delta (1.27-1.75: the camera moves over high-contrast step edges), so the dissolve seam is as smooth as any frame step; last frame = frame 0 (read).
- Frames read from the mp4 at 0, 1, 3.1, 5.3, 5.98, 6.1, 7.3, 9.3 s (+ 0.5, 2, 3.15, 3.5, 5.5, 6.05, 7.25, 8.5 s on the previous camera); fast stills at 5.0-5.7 s for the airborne leader.

## Doubts
- **Bounces thin out late** (9, 7, 6, 5, 6, 2, 4, 0 per s): fast balls fly 5-15 steps per bounce (real stair physics at speed), so the last second before the finish is steel in one long flight + the music. The step counter still climbs fastest at the end (steel 66 -> 97 in 1 s).
- Balls are small when the camera zooms out (zoom 0.55: ~23 px across); the HUD chips/track carry the race.
- "Off the edge" comes from random sideways kicks per impact (surface roughness), the one non-deterministic-looking ingredient; seeded.
- Scale: g is set for a ~12 cm-deep model staircase (so 100 steps take ~7 s); with full-size stairs the same race would take ~13 s.
- At frame 0 all three are level; the tie shows "RUBBER LEADS".

## Flags
`--seed (39) --label --cap --still --frame a,b --dry --audio --sound 0 --sfx (0.55) --fin (2.0) --hold (1.6) --search a b`. Physics `--g (5333) --v0 (600) --rb (18) --zw (100) --er (0.86) --eg (0.70) --kr (0.025) --ks (0.008) --kg (0.008) --br/--bs/--bg (0.99) --crackv (700) --crackk (2.5e7)`. Camera `--zmin (0.55)`.

## Upload draft
- Titles: "3 balls race down 100 stairs… only ONE makes it 🏁 #satisfying #physics #shorts" · "Rubber vs steel vs glass down 100 stairs: who survives? 🏁 #satisfying #physics #shorts" · "The glass ball was winning… then step 76 happened 💥 #satisfying #physics #shorts".
- Pinned comment: "glass was literally winning at step 75 lol… which one were you betting on?"

## Ship (batch61, 2026-10-30): approved
- 4K `NF_SCALE=2.0 python scenes/ol_stairs_race.py --label ship` (defaults): h264 High yuv420p 2160x3840 @ 60, 1053 frames 17.55 s; -14.00 LUFS, peak -4.52 dBFS, last 0.5 s silent; flash PASS; events json bit-identical to the reviewed fhdv3c. Frames read at 4 timestamps.
- Staged `<VIDEOS_DIR>\DopamineExe\schedule\2026-11-10\1_ol_stairs_race.mp4`, 04:00 local Nov 11 (= 19:00 US East Nov 10). FHD review copy → `DopamineExe\archive\ol_stairs_race_fhd.mp4`.
