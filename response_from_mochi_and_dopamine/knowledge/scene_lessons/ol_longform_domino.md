# ol_longform_domino (DopamineEXE long video 1)

- Brief: docs/BRIEF_dopa_long1.md (2026-11-03). Native 16:9, logical 1920x1080. Extends the 12.6K Short ol_domino_giant.
- Files: `scenes/ol_longform_domino.py` (timeline, chapters, camera, HUD, render, audio) + `scenes/ol_longform_domino_env.py` (3D camera, domino boxes, the 26 environments). The Short's file is untouched.
- Status: see "Delivered" below.

## The rule (honest numbers)
- Each domino knocks over one **1.5x** taller (the real limit; L. Whitehead, "Domino 'chain reaction'", Am. J. Phys. 51, 182, 1983). Domino 1 = 1.5 cm; domino n = 1.5 cm x 1.5^(n-1).
- **165 dominoes**: domino 165 = 1.135e27 m = **120 billion light-years**, the first one taller than the observable universe (93 billion ly; domino 164 = 80 billion ly).
- Geometry (as the Short): thickness 0.17 h, gap 0.50 h (contact at 30 deg), width 0.5 h; self-similar about x = 0, so every domino looks the same to a camera scaled with it.
- Kinematics: scripted, deterministic. Free phase 0.4u + 0.6u^2 to contact, then each leans on the next (corner solved on the next back face). The last domino falls 0 -> 90 deg over 16 beats.
- Timing is stylised (a 1.5 cm domino really falls in ~0.1 s, a planet-sized one would take hours); only sizes and distances are claims.

## Timeline (152 bpm, t = 0 = beat 0 of the music)
- Hit 0 on beat 5 (frame 0: the first domino already falling). Intervals between hits fall linearly 13 -> 5 beats (5.1 s -> 2.0 s), non-increasing, sum fixed so hit 163 lands on beat 1372; the last domino lands on beat 1388 (547.9 s) = the movement's last chord. End 556.5 s (9:16.5) after an 8.6 s hold with the count card and a 1.2 s fade to black.
- Hits per 30 s: 6, 7, 7, 7, 7, 8, 7, 8, 8, 9, 9, 9, 10, 10, 11, 12, 13, 15 (the rate only climbs).
- `--plan` prints the chapter table.

## Chapters (k = first domino taller; card fires when it is struck; chapter starts 2 dominoes earlier)
| # | start | card | world | camera | landmark / beat |
|---|---|---|---|---|---|
| 1 | 0:00 | 0:07 coin | dark walnut table, warm lamp, bokeh | macro low 3/4, slow orbit | US quarter (24.3 mm) lying beside the chain |
| 2 | 0:11.8 | mug | white marble counter, subway tiles, window light | side tele | mug with steam (9.5 cm) |
| 3 | 0:30.8 | cat | living room: oak floor, rug, sofa, lamp, dusk window | floor-level, looking up the chain | ginger cat watches, then leaps away, annoyed |
| 4 | 0:44.2 | person | backyard at golden hour, fence, tree line | 3/4 from ahead | a person walks in, looks up, steps back |
| 5 | 0:57.2 | car | night street seen from above: lanes, houses, lamps | top-down 66 deg | a red car drives past, headlights; "a house, 10 m" |
| 6 | 1:14.6 | blue whale | open ocean, sandbar, clouds | low over the water | the whale breaches (4.6 s) and splashes |
| 7 | 1:27.6 | Statue of Liberty | harbour at sunset, skyline, gulls | low hero looking up | back-lit dominoes (rim light) |
| 8 | 1:40.7 | Eiffel Tower | city at night (light grid, river) | orbit (+2.6 deg/s) | lit tower, sweeping beacon; Burj Khalifa callout; a plane |
| 9 | 2:15.4 | Everest | Himalaya: snow, ranges, mist | aerial 30 deg | an airliner + contrail at 11 km |
| 10 | 2:39.5 | the sky (100 km) | the curved Earth below, blue -> black sky, aurora | side tele | altitude lines 11 / 35 / 100 km |
| 11 | 2:55.3 | ISS orbit (408 km) | low orbit: Earth limb, night side lights | 3/4 above | the ISS crosses (drawn 40x, said on screen) |
| 12 | 3:15.0 | Moon | black space, the Earth under the chain's start | low hero | the Moon at true size in front |
| 13 | 3:26.8 | Earth | the Earth (where the chain began) + the Moon's orbit | orbit (-3.2 deg/s) | the Moon at its true 384,400 km |
| 14 | 3:50.5 | Jupiter | warm dust sky | ahead, looking back | the 4 Galilean moons at true orbits; light-second callout |
| 15 | 4:12.2 | Sun | red haze; dominoes back-lit silhouettes | low hero | prominences; light-minute and Sun-Mercury callouts |
| 16 | 4:58.4 | Earth's orbit | violet; orbits Mercury-Jupiter + asteroid belt | high oblique 40 deg | light-hour callout |
| 17 | 5:25.7 | Neptune's orbit | teal; outer planets, Kuiper belt, a comet | elevated side | light-day |
| 18 | 5:38.3 | heliosphere | indigo; the Sun's bubble, Voyager 1, Oort cloud | looking up the chain | light-month, light-year callouts |
| 19 | 6:32.0 | nearest star | dense stars, Milky Way band | side tele | bracket Sun -> Proxima (4.25 ly) |
| 20 | 6:43.4 | Orion Nebula | full-sky pink/teal gas | dutch angle 7 deg | the nebula in front |
| 21 | 6:57.2 | star cluster | inside the galactic disc: golden band, dust lanes | rising (pitch +0.9 deg/s) | Omega Centauri; Pleiades, disc thickness, galactic centre callouts |
| 22 | 7:41.1 | Milky Way | dark, distant galaxies | orbit (+2.6 deg/s) | the spiral in front ("the Sun is here"); Andromeda distance callout |
| 23 | 8:07.1 | Local Group | violet haze | from above, 50 deg | MW, Andromeda, Triangulum + dwarfs |
| 24 | 8:30.8 | Laniakea | gold flow lines | high oblique | the Great Attractor, "we are here" |
| 25 | 8:45.8 | cosmic web | violet filaments | dolly-in, dutch -5 deg | Hercules-Corona Borealis Great Wall (~10 bn ly) |
| 26 | 8:57.6 | observable universe | black | pull back for the finale | the CMB-skinned sphere; gold domino lands on the last chord, count card |

## Engine notes
- Real 3D (pinhole camera, near-plane clipping, painter's sort by depth): domino = box with lacquer gradient per face, outline, top-edge highlight, optional rim light; ground shadows projected along the light (ground chapters only).
- The camera index c follows the smoothed chain index (sigma 0.7 s): the struck domino keeps about the same screen size, so the zoom-out is continuous. At each chapter start the camera rig (yaw, pitch, dist, f, anchor, roll, orbit rates) blends FIRST, inside the old world (2.8 s), THEN the world cross-fades with the camera settled (1.8 s); both shrink to 0.38 / 0.25 of the start-to-card time in the fast late chapters.
- **Learned (flash_check):** the first full render FAILED at 0:14, 1:16, 2:41 (worst 1 s = 4). A camera swing that runs while a dark world cross-fades into a bright one (table -> white kitchen, night street -> day ocean, snow -> sky) makes >25 % of the cells rise and fall alternately (horizon and giant dominoes sweep over the changing background). A slower swing (4.5 s) did not fix it; moving the camera first and cross-fading after did (worst 1 s = 2, 1, 2 on the three windows).
- **Learned (audio):** at sfx x0.42 the clacks sat 3.6 dB UNDER the full orchestra (400 Hz-4 kHz, 60 ms after each hit), and the big late clacks pitched down to E2 vanished. Now x1.4 and the pitch walk stops at E3: median +11 dB.
- Precision: the chain is self-similar about x = 0, so camera-relative coordinates stay well-conditioned from 1.5 cm to 1e27 m (doubles).
- The Earth sits under the chain's start (its centre at y = -R_E): from chapter 10 the straight chain visibly leaves the curved Earth (honest geometry).
- Landmarks sit beside the chain at true size, mostly just in front of it (behind, the giant dominoes hid them); small objects stay close to the chain and the lens is longer there, so perspective barely changes the comparison. Distances between the landmarks are NOT to scale (a line-up), except the Earth (the chain's start), the Moon's orbit and Jupiter's moons.
- Space chapters each get a full-sky panorama (`_PANOS` in the env file), drawn at 1/4 resolution and scaled up (large gradient fills are the slowest thing in a frame).

## Sound
- **Music: Dvorak, Symphony No. 9 "From the New World", 4th movement (Allegro con fuoco), complete.** Composition PD (1893; Dvorak d. 1904). Note data: Mutopia #1793 (N. Simrock 1894 edition, typeset 2011, CC BY-SA 3.0 engraving; the notes are PD), `<SOUNDFONTS_DIR>\scores\dvorak_newworld\mids\Mvt4_conFuoco.mid`, constant 152 bpm in the file, 549.5 s. Our orchestration via lib/orchestra (MuseScore_General, MIT): every MIDI track mapped to its instrument (flute, oboe, clarinet, bassoon, trombone, strings x3, cello, contrabass, 2 horn sections, trumpet, timpani, the one cymbal); the last chord is held 6 s under the count card with a fading expression; a soft boom on it.
- Why this piece: it builds by itself (the opening semitone crawl, the horn/trumpet theme at 0:11, a quiet clarinet second theme, the big coda), so the score changes character per section the way the chapters do; it is not kid-coded; not used by the atom video. Its 4th-movement theme was in the Short paper_fold (acceptable for a long video, as Mountain King was).
- SFX: one tonal wood clack per hit (pitch class = the bass note sounding at the hit, octave walks E5 -> E2 with size; bigger = longer ring + a body thump), a soft whoosh into each chapter card, the whale's two splashes, 3 low clacks + boom on the landing. Mastered to -14 LUFS (`audio.master`, reverb 0.4).
- The bed is cached (`output/ol_longform_domino_bed.npy`, pass `--bed-cache`).

## Commands
```
NF_SCALE=1.0 python scenes/ol_longform_domino.py --plan
NF_SCALE=1.0 python scenes/ol_longform_domino.py --still --frame 12.5s,100s --label x
NF_SCALE=1.0 python scenes/ol_longform_domino.py --cut "0,9;38.8,46.3" --label test --bed-cache
NF_SCALE=1.0 python scenes/ol_longform_domino.py --render --label full --bed-cache   # 30 s chunks, resumable
```

## Delivered (2026-11-03): FULL video, Full HD, waits on the owner
- `<VIDEOS_DIR>\DopamineExe\review\longform1\ol_longform_domino_full_fhd.mp4` + README.md, UPLOAD_notes.md (4 titles, description with chapters, pin), `thumbnails\` (4 x 1280x720 from `--still --nohud` frames).
- Built as label `full3`: `full2` (all chunks with the camera-then-fade order) + the 4 chunks around 1:28 and 2:55 re-rendered with `fade_first` (ocean -> harbour, atmosphere -> orbit). Render 28 min at ~20 fps (FHD), one process, ffmpeg 2 threads.
- Checks on the encoded file: h264 yuv420p 1920x1080 60 fps, 33,390 frames, 556.500 s; aac 556.495 s (both start 0); PTS all 256/15360; -14.0 LUFS, true peak -1.4 dBFS; flash_check PASS (61 flashes, worst 1 s = 2 at 17.5 s); blackdetect only 556.38-556.48 (the fade-out end); chunk seams 3600/5400/7200/9000/10800/12600: seam step = neighbours (e.g. 2.57 vs 2.69/2.60); hit clacks +8.5 dB median over the 60 ms before (400 Hz-4 kHz); landing +24.5 dB; 30 s RMS -20.3 -> -13.1.
- ~60 s test cut (8 windows, `--cut`) checked first: frames of any two chapters differ in world, palette and camera (the owner's "same thing" lesson).
- Mastering: the orchestra is mastered alone and the clacks added after at the same gain, then a soft ceiling at ~-3 dBFS (mastered together, the limiter flattened the clacks to +2 dB).
- Weak spots (told the owner): slow first minute (~5 s per domino, forced by 165 hits rising in rate over 9:08 of music); 6:00+ space chapters share a composition; Sun partly hidden (silhouettes), Milky Way / Local Group small at true scale; flat cartoon props; the whale's mid-jump pose; a calm finale.
- Next (after the OK): `NF_SCALE=2.0 ... --render --label full4k --bed-cache` (chunks go to a `_x2` dir); ~2-3 h.
