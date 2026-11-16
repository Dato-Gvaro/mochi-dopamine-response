# ol_gear_train (Dopamine.exe)
- New scene, character-free (docs/BRIEF_channel2.md, docs/BRIEF_overnight_1023.md). Skeleton: ×3 per generation (every gear drives 2 gears that turn 3× faster) toward a named end state; concrete objects (brass/copper/steel clockwork), one obvious rule.
- Caption (baked, `--cap`; `--cap ''` = base): `Every gear spins 2 gears ^3× FASTER^|until the last gear hits ~10,000 RPM~` (`^x^` = the fastest running generation's hue, `~x~` = gold).
- Delivered: `<VIDEOS_DIR>\DopamineExe\review\ol_gear_train.mp4` (**v2**, Full HD, label fhd2, 17.00 s, 1020 frames; overwrote v1). No 4K yet.
- **v1 → v2 (owner review 2026-10-24: "kinda interesting kinda boring — maybe each kind of gear having little numbers next to it, so we watch how the speed progresses"):**
  - A live RPM tag on ONE gear of every generation (pill in the generation's metal colour, dark ink, 36 px number + 22 px "rpm", 50 px tall, centred on the axle): 15 (root) and 45 (top gen-1 gear) from frame 0; 135, 405, 1,215, 3,645 pop in (0.22 s overshoot) on the clack of the first gear of their generation; 10,935 on the cadence. Each generation's engagement sweep now starts a quarter turn further round (12, 3, 6, 9 o'clock; `SWEEP0`), so the tagged first gears are spread over the machine: (665,549), (665,883), (429,1105), (272,716); gen-6 tag on the gear nearest (232,383).
  - Main counter is now **TEETH MESHED** (cumulative, live every frame): each running child's pinion takes its parent wheel's teeth at rpm_parent / 60 × 24 per second; the machine has run since t = −8 s. It never sits still and accelerates with every gear that joins: 96 (frame 0), 133, 209, 330, 562, 905, 1,418, 2,362, 3,931, 6,172, 9,068, 13,332, 20,905, 32,110, 46,929 at each second up to the cadence, then 111,972 teeth/s → 212,965 at 15.92 s (×2,200). The ×3 pill under the counter was removed (the tags carry the ×3 steps). Meter unchanged (TOP SPEED, log scale to the 10,000 RPM goal).
  - Unchanged: layout, colours, gear schedule (only the sweep start moved), music, sound, cadence, loop.

## Mechanism (honest, logical 1080x1920, static camera)
- 127 compound gears, generations 0-6. Each gear = a 24-tooth wheel + an 8-leaf steel pinion on the same axle. A wheel drives the pinions of 2 children, so each child turns 24/8 = **3× faster, the other way round**. Root 15 RPM (90°/s) → 45, 135, 405, 1,215, 3,645, **10,935 RPM** (gen 6).
- Teeth mesh exactly: θ_child = −3(θ_parent − φ) + φ + π − π/8 (φ = mesh direction), so a parent tooth always sits in a pinion gap (checked 1:1 at frames 20/300).
- Layout = H-tree: gen 1 vertical, each generation turns 90°, each wheel 0.707× its parent (pitch radii 166.6, 117.8, 83.3, 58.9, 41.7, 29.5, 20.8 px; d1 = 222 px solved to fit x 146-870, y 332-1212 incl. waiting offsets). No two gears of one layer touch. Layer = generation: a child wheel tucks BEHIND its parent, its pinion meshes in the parent's layer (clock movement); spoke windows show the layers behind.
- Waiting gear: dim (S×0.72, V×0.46 of its metal), 1.9 modules out of mesh along the mesh line. Engage = slides in over 0.075 s (ease-in, contact at full speed) → small gold glint at the mesh point (0.16 s) → lights up over 0.14 s and runs. In an H-tree the parent's slide is perpendicular to the child's mesh line, so a waiting child never collides.
- Colour (one per generation, calm and ordered): copper 0.045 → bronze 0.08 → brass 0.10 → gold 0.125, then teal 0.465 → 0.505 → steel blue 0.545 (no yellow-green); S 0.66-0.70, V 0.74-0.80; screen-fixed brushed-metal gradient (highlight top-left, stays put while the gear turns). Pinions steel tinted 28 % toward their own wheel.
- Motion blur (no strobing): 0.5-frame shutter. Teeth sharp (multi-sample, OPERATOR_ADD + clip/paint_with_alpha) only while < 0.35 pitch/frame (gens 0-1); faster teeth average into a translucent ring. Spokes sampled while < 18°/frame (gens 0-2); faster webs average into a translucent disc + stationary turned-metal rings and a fixed sheen arc. Gen 3 turns 40.5°/frame, gen 6 1,093°/frame: neither is ever drawn with a periodic pattern → no wagon-wheel.
- HUD (v1; v2 changes above): tachometer meter y 1290 (log scale 15 → 10,000 RPM, a notch per ×3 step, generation-colour fill, white marker, gold "10,000 RPM" goal from frame 0, "TOP SPEED" left); counter y 1488 = top RPM (rolls up log-wise over 0.2 s at each jump) + "×3" pill (current generation colour, pops on each jump) + "RPM"; thin white rounded frame 128-888 × 318-1226; watermark "DOPAMINE.EXE" right-aligned at 888, y 1254, 35 %.

## Schedule (clip beats, 124 bpm; beat 0 = score beat 12)
- Frame 0: root + gen 1 turning (45 RPM), the first gen-2 gear already sliding; whole machine visible (end state readable).
- Gen 2: beats 0.25, 1, 2, 3 · gen 3: 8ths in 5-11.5 · gen 4: 16ths in 12-20 · gen 5: 16ths in 21-29.75 · **gen 6 (64 gears) all on the cadence (beat 30)**. Order within a generation = clockwise sweep from 12 o'clock. Each generation starts on a beat: top-speed jumps at **0.12, 2.42, 5.81, 10.16, 14.52 s**.
- Top RPM per second: 45 (frame 0), 135 ×2, 405 ×3, 1,215 ×5, 3,645 ×4, 10,935. **Growth ×243.**
- Gears spinning per second: 3, 6, 7, 9, 11, 13, 16, 19, 24, 28, 31, 36, 44, 51, 59, 127.
- Clacks per second: 3, 1, 2, 2, 2, 3, 3, 5, 4, 3, 5, 8, 7, 8, then 68 at the cadence.
- **Cadence 14.516 s** (score bar 11, the ritornello's cadence on E): 64 tiny gears clack in, counter rolls to 10,935 and turns gold, meter full + goal glow, frame warms to gold, a calm diagonal light glint sweeps the metal (ATOP the gear layer only, peak α 0.46, 1.45 s). Hold → 0.6 s dissolve into the pre-roll (t −0.6..0). **17.00 s, 1020 frames.**
- Loop: root 90°/s and every gear has 90° symmetry (24 teeth, 8 leaves, 4 spokes, 4 root bolts) → after a whole number of seconds every running gear is pixel-identical; the clip is exactly 17 s, so the dissolve only fades the late generations back out of mesh (no ghosting on the running ones).

## Sound
- **Music played as music:** J. S. Bach, Violin Concerto in E major, BWV 1042, I. Allegro (c. 1717-23; Bach d. 1750, PD). Source: Mutopia `BachJS/BWV1042/concerto-in-e-major` (Bach-Gesellschaft 1874), listed **Public Domain**; saved at `<SOUNDFONTS_DIR>\scores\bach_violin_concerto_e_bwv1042\` + `SOURCE_mutopia.txt` (downloaded 2026-10-24). Not on the used/banned lists, not kid-coded, no earlier scene uses it.
- Score beats 12-42 (bars 4-11 of the opening ritornello: the ringing repeated 16ths over the climbing bass scales, the falling sequence, the cadence on E). One steady tempo, **124 bpm**. All five parts from the score: solo violin, violin I + II (strings), viola, continuo (cello + contrabass 8vb + a quiet harp 8va). Cadence: violin E5 held, full E-major chord (strings, horns), rolled harp, celesta glint, cello/contrabass E, soft timpani E.
- SFX (×0.60): a tonal "clack" per gear that slides into mesh (sine with a 25 ms ring, an inharmonic 2.76× partial that dies in 5 ms, a 1 ms tonal click at 2.9 kHz; no noise), pitched to a note the score is sounding at that instant, smaller generations higher (E4-ish → A6). Ticks on the grid, denser as the train speeds up: quarters → 8ths (gens 2-3) → 16ths (gens 4-5), tonal 7 ms blips C6-B6. Cadence: a 6-note rolled clack cluster + bell tink E6 + a rising E-major chime run on the glint. SFX events per second: 7, 5, 6, 6, 6, 8, 11, 14, 12, 11, 13, 17, 15, 16, 18, 5.
- `level_bed` (+3 dB crescendo, cadence +4 dB), `audio.master(peak_db=None, reverb=0.5)`, last 0.6 s digital silence. Own mux without `-shortest`.

## Checks (encoded Full HD, v2)
- h264 yuv420p 1080x1920, 60 fps, 1020 frames, 17.00 s. **flash_check PASS** (0 flashes, mean lum 0.029).
- **−14.01 LUFS**, peak −4.18 dBFS, last 0.5 s digital silence; energy > 5 kHz 0.23 %. RMS per second (muxed): −18.7, −19.1, −18.3, −18.2, −18.1, −17.7, −17.5, −17.4, −17.2, −17.0, −17.1, −16.5, −16.5, −16.2, −14.8 (cadence), −14.2, −36.8 (tail).
- Mean relative luminance (encoded v2): frame 0 0.039; **finished machine (15.92 s) 0.069**; last frame 0.038 (= pre-roll). v1: 0.038 / 0.063 / 0.037.
- Seam (encoded mean |Δ|, last → 0): **2.52** v2 (check_clip 2.38) — the same as an ordinary step in this file (500→501 2.53, 1018→1019 2.26; 0→1 1.45). v1: 2.22. Fine teeth turning every frame make every step ~1.4-2.3; pre-encode the seam is 1.47 vs a normal step 1.36. check_clip's 0.12-0.72 band does not fit a frame full of moving teeth.
- v2 frames read from the mp4 at 0, 0.2 (135 tag popping), 2, 2.5 (405), 5.92 (1,215), 10.27 (3,645), 14.67 (10,935, finale), 15.92 and the last frame. v1: 0, 0.5, 1, 2, 6.5, 14.52, 15.0, 15.92, last; FHD stills 1:1: the first gen-2 slide (frames 3/6/7/9/14: out of mesh → contact + glint → lit, teeth ring blurred), meshes root/gen-1 pinion and gen-1/gen-2 pinion (frames 20/300: teeth interleave).

## Flags
`--label --cap --still --frame a,b --dry --audio --sound 0 --sfx (0.60) --fin (2.0) --bpm (124) --secs (17, must stay an integer) --jy (772) --theta0 (0.13)`. No cache; a still renders in ~0.2 s, the full FHD clip in ~3 min.

## Doubts
- Root is in the CENTRE, not at the top: an H-tree is the only layout I found where 7 generations (64 gears of 21 px radius at the end) fit without same-layer collisions; top-down fractal trees collided from gen 4 (layout search in scratch). The cascade reads centre → edges.
- v1 doubt (counter static between ×3 jumps) addressed in v2: the counter is the live TEETH MESHED count; the ×3 steps live on the per-generation RPM tags and the meter.
- The tags sit on top of the machine and cover a few neighbouring small gears (the 10,935 tag reaches x 140: inside the frame and the safe zone).
- Clacks are sparse in the first 2 s (1-3/s; only 4 gen-2 gears exist); ticks and the music fill it.
- Small fast gears are drawn as blurred discs with stationary sheen (no visible rotation direction past gen 3) — that is the anti-strobing choice.
- Score file is Mutopia Public Domain; the Mutopia track names (SoloViolin, ViolinI…) are read by name.

## Upload draft
- Titles: "Every gear spins 2 gears 3x faster… until the last gear hits 10,000 RPM ⚙️ #satisfying #physics #shorts" · "One slow gear became 10,935 RPM in 7 steps ⚙️🔥 #satisfying #physics #shorts" · "127 gears, each 3x faster than the last… how fast does the last one spin? ⚙️ #satisfying #physics #shorts".
- Pinned comment: "the big copper one only does 15 rpm and the tiny blue ones end up at almost 11 thousand… which row did you think would break first?"
