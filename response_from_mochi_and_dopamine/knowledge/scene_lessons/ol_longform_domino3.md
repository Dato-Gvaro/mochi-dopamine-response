# ol_longform_domino3 (DopamineEXE long video 1, FINAL style)

- Brief: docs/BRIEF_dopa_long1d.md (owner picked variants 1 + 4). v1, v2 and the style tests stay untouched (imported read-only).
- Files: `scenes/ol_longform_domino3.py` (Journey style, sky journey, lanes, labels, HUD, finale, render, audio) + `scenes/ol_domino3_objects.py` (FX parts, 116 new drawings + space generators, the roster `R3`).
- Timeline = v2 (1.12x, 586 dominoes, hit grid 50 -> 80/min, last domino lands 9:07.9). END_HOLD 8.6 s (= v1's cached bed length) -> 9:16.5, 33,390 frames. Fade to black over the last 1.25 s.

## Look
- Base: variant 1 (Aurora glass: glass rainbow dominoes, cel-shaded layered parts, reflections, bloom).
- One continuous sky driven by time (`phase(t)`): golden (variant 4 lighting: low sun x 1500, gold rims, long shadows toward camera) -> dusk by 1:45 (sun set) -> night + stars by 2:18 -> aurora peak 2:39 (two cached curtain layers cross-fading, period 15 s) -> space palette by 3:20. Hills fade after Everest. Object lighting params (shade/light hue, rim colour, grade map, haze) interpolate warm -> cool with the same weight.
- Golden-phase fixes of variant 4: labels get a dark soft backing (fades with night), objects keep their natural fill (no silhouette multiply), bloom threshold 0.82 (night 0.55).
- Rim light capped at 3 + 0.006 x size px (big objects got 20 px mint bands). Reflections paint flat base fills (speed).

## Objects
- 182 FINAL -> 180: dropped `unity` (TALLEST STATUE: featureless bronze figure read as creepy) and `redspot` (GREAT RED SPOT: banded slab read as a cake).
- Space set from generators: planet, rock, star, black_hole, far_beam, orbit_map, nebula, ring_nebula, spiral, elliptical, cluster, galcluster, shell, web, jets, cmb_universe.
- Line facts (cars, ants, blood vessels, Great Wall) are drawn thicker than true so they read; Olympus Mons is compressed to 4.4x wide (true ~27x); Lion's mane tentacles spread wider than true. Size labels are true.
- Lanes: default front (z just in front of the chain). BACK = olympus, asteroid, universe: just behind the chain, scaled by depth ratio so the on-screen comparison stays true.
- The next object ("ahead") fades in over 2.7 -> 1.3 dominoes of camera index (before: Everest popped in 7 dominoes early as a grey wall).
- Labels: newest 7, own placement search (up/down/sideways), never above y 300 or below 960; hidden under the end card.

## Checks / tools
- `--gallery` (all objects on sheets), `--passes` (every object at its pass moment +0.55 s, 4x4 sheets: the composition check that found the ahead-wall, Everest and finale problems).
- Frame cost FHD 0.25-0.6 s (fills dominate). Full render ~3 h, one process, ffmpeg 2 threads.

## Gotchas
- Bash heredoc + apostrophes breaks: write edit scripts to files.
- At a banner's first frames the text shadow outweighs the fill (looks dark): shadow alpha now scales with a.
- Self-similar camera: horizon y and sky layers are constant -> sky layers are cached once.

## Delivered (2026-11-05): FULL video, Full HD, waits on the owner
- `<VIDEOS_DIR>\DopamineExe\review\domino_v3\domino_full_fhd.mp4` + README.md, UPLOAD_notes.md, `thumbnails\` (4 x 1280x720, frames rendered without HUD/labels + title). `review\domino_style_v2\` moved to `archive\`.
- Built as label `full`: 19 chunks in 101 min (one process, ~5.5 fps, ffmpeg 2 threads). Restarted once ~1 min in for the label-gap fix (PX 18 / PY 16 px, vertical moves before sideways).
- Encoded-file checks: h264 yuv420p 60 fps, 33,390 frames, PTS step 256 throughout; -14.0 LUFS, TP -2.4 dBFS; flash_check PASS (12 flashes, worst 1 s = 2 at 273 s); clacks +10.7 dB median (p10 +0.7); chunk seams = neighbours.
- Audio: v1's cached bed `output/ol_longform_domino_bed.npy` (same score/clock/hold) + v2 clacks + 3 low landing clacks, mastered like v1.

## Fix pass 2 (2026-11-05, owner review of 2:19-2:27): label `fix2`
- DROPPED2 = asteroid (hidden behind Everest/trench, only its label showed), borehole (read as a building). Roster index "i" keeps the old numbering so EARTHLY etc. don't shift outside the span.
- BACK += trench, halley, neutron (the newest object must never cover the active fall); the back lane is drawn biggest first (Olympus had covered the neutron star). XO = trench +0.5, halley +1.1 domino heights (clear Everest's flank and each other).
- Re-rendered chunks 4-6 only (frames 7200-12600; the changed objects can be on screen from 2:00 to 3:30). The other 16 chunks were copied byte for byte; the frames at the span edges decode identically; the audio is identical.
- Lesson: check the moments AFTER a hero banner on the pass sheets too. A dense run of objects (one per domino) needs lanes or drops, not just label placement.

## v4 (2026-11-05, docs/BRIEF_dopa_long1e.md): `scenes/ol_longform_domino4.py` (imports v3; v3 untouched)
- Owner on v3: "objects appear from nowhere" + "avoid objects overlapping, give them space".
- **No fades:** every object is drawn whenever it can be on screen (camera index -46 .. +9.5 dominoes); the self-similar zoom carries it in from the right edge about 3 dominoes before its pass. Only the NEXT object's label fades in (x 1800 -> 1500).
- **Layout solver** (`--solve`, cached in `scenes/ol_longform_domino4_layout.json`): per object a lane (front z=-0.06H, back z=D+0.03H, near z=-1.0H; back/near scaled by the depth ratio at the pass so the on-screen size stays true) and an x offset a in [-1.2, +1.0] domino heights (-2.6 .. +1.7 dominoes). Test = screen occupancy masks (10x10 paint cells over the local bbox, rasterised at 8 px) at 15 camera positions per object (u = +3.4 .. -14); max 5% overlap of the smaller mask, objects under 44 px ignored; front/near objects may cover at most 18% of the falling dominoes' box.
- Order: KEEP (heroes + anchors) at their most natural free spot, then the rest in chain order at the LEFTMOST free spot (interval packing), then a repair pass (one blocker may move). Flat objects (h/w < 0.5) prefer the near row; Everest prefers the leftmost anchor (its slope enters late).
- Result of the first (fit-based) drop rule: 156 kept, 22 dropped. Superseded by the FAME rule below.
- Lessons: one row along the chain fits about 2.3 x (width/size) dominoes per object; it is the capacity limit. The flat-card projection must not be used near the camera plane (`valid`). Masks, not summed cell boxes (sheared cells double count). Orbit/shell/galaxy objects need their full disc in the mask.
- Weak: entering objects are big (the camera zooms); near-row objects loom at the bottom right for 2-3 s.

### v4 CHECKPOINT 2 (2026-11-05, owner pause; NO render running, the full render NOT started)
Done since checkpoint 1:
- **Olympus Mons is drawn 3x wider than tall** (v3: 4.4x; true ~27x; the size label stays true). It is patched in the v4 process only (`o_olympus3`); v3's objects file is untouched.
- **Strip projection** (`strip_mats`): objects are drawn as vertical strips, each with its own affine map fitted to the projected world corners. One strip while the perspective is mild; up to 32 near the camera plane. Strips with a corner near or behind the camera are skipped. Used by the renderer (`draw_obj` + `reflections`, a clip per strip; shadows and contact ellipses only from 2.5 dominoes ahead, the shadow faded) AND the solver (`cell_boxes`, `screen_box`). AHEAD raised to 16 (strips cull).
- **Pop-in check** (scratch `popcheck.py`: no object may first appear inside the frame, every 3 frames over the whole timeline): 43 → 0 real pop-ins. 10 flags remain, all 1-5 px slivers at the bottom edge (near-row objects rising in from below) or at the right edge (the farthest-galaxy beam).
- **Re-solved with the fame rule:** 163 kept, 15 dropped; the first 2:40 has 60 objects (one per 2.7 s); no must-keep fails. Mariana Trench and Halley's Comet are restored; the neutron star stays dropped (Halley's Comet fills its slot; both tier 2).
- **Contact sheets** (pre-render frames, 3x3, scene time in yellow):
  - `output/v4s_a_0005-0058.png`: 0:05, 0:20, 0:27, 0:30.5, 0:44, 0:47, 0:50, 0:54.6, 0:58
  - `output/v4s_b_0218-0230.png`: 2:16, 2:18.4, 2:20.3, 2:21.5, 2:22.4, 2:24, 2:26.2, 2:28, 2:30
  - `output/v4s_c_crowded.png`: 1:03, 1:33.6, 1:45.6, 2:03.3, 2:39.4, 3:42.6, 5:01.7, 7:35.4, 9:06.5

Drop list (15):
- Tier 2: neutron star (Halley's Comet), Titan (Moon, Mercury), Antares (UY Scuti), VY Canis Majoris (Betelgeuse, UY Scuti).
- Tier 1, each blocked by the neighbours in brackets:
  - biggest diamond (hummingbird, credit card)
  - coconut crab (money stack, nugget)
  - capybara (hydrant, penguin)
  - rubber-duck comet (Everest)
  - Sirius B (Mars)
  - geostationary orbit (Saturn)
  - Aldebaran (Arcturus, Polaris)
  - Oort cloud (Helix Nebula)
  - Whirlpool (Sombrero, Triangulum)
  - Pinwheel (Milky Way, Andromeda)
  - Porphyrion (Alcyoneus, Coma)

Still weak (look, not a bug):
- Objects entering from the right are big, because the camera zooms out.
- Near-row objects loom at the bottom right for 2-3 s (car 0:54, tanker 1:45, oarfish 1:03).
- The watch enters big at the top right at 0:03-0:05, right of the fading rule text.

### v4 CHECKPOINT 3 (2026-11-05; NO render running, the full render NOT started)
- **Looming fix:** a new solver rule. Before its pass, an object may cover at most 12% of the frame's lower third (`LOOM_THR`), and a near-row object may not streak more than 22% of the frame width along the bottom. With this rule the car, cruise ship, crocodile and blue whale move to the back row; the near row drops from 19 to 10 objects (salamander, oarfish, tanker, airship and other flat ones, which now enter low but small).
- **Overlap tolerance:** tightened from 5% to 2% of the smaller mask. The shoebill (tier 1) now yields to the penguin and is dropped (they had touched at 0:44-0:47).
- **Re-solved:** 161 kept, 17 dropped; first 2:40 = 58 objects (one per 2.8 s); longest gap 7.3 s; no must-keep fails. Pop-in check: 1 flag, a 2 px sliver of the farthest-galaxy beam at the right edge.
- **Sheet:** `output/v4L_check2.png` (0:44, 0:47, 0:54.6, 0:58, 1:03, 1:36, 1:45.6, 2:20.3, 5:01.7). The car enters mid-height at 0:54.6; 2:20 and 5:01 are unchanged.
- **Drops (17):**
  - Tier 2: neutron star, Titan, Antares, VY Canis Majoris.
  - Tier 1: credit card, elephant-bird egg, capybara, shoebill, pizza, tallest waterfall, Sirius B, geostationary orbit, Arcturus, Oort cloud, Whirlpool, Pinwheel, Porphyrion.
  - Biggest diamond, coconut crab, the rubber-duck comet and Aldebaran are now back.
- UPLOAD_notes count: 161.

Next commands (on the owner's go):
    NF_SCALE=1.0 OMP_NUM_THREADS=1 OPENBLAS_NUM_THREADS=1 MKL_NUM_THREADS=1 python scenes/ol_longform_domino4.py --render --label v4c
    (layout is cached in scenes/ol_longform_domino4_layout.json; re-solve only after changes: --solve)
    then verify (ffprobe, PTS, -14 LUFS, flash_check, seams, 1:1 frames at the crowded moments), deliver to
    <VIDEOS_DIR>\DopamineExe\review\domino_v4\ with README, UPLOAD_notes (count 161), 3-4 thumbnails.

### v4 DELIVERED (2026-11-05): label `v4c`
- `<VIDEOS_DIR>\DopamineExe\review\domino_v4\domino_full_fhd.mp4` + README, UPLOAD_notes (161 objects), thumbnails (4).
- Render 103.5 min (3.8 fps with a Mochi job alongside), 19 chunks in `output/ol_longform_domino4_chunks_v4c`.
- Encoded-file checks: h264 yuv420p 60 fps, 33,390 frames, PTS step 256; -14.0 LUFS, TP -2.4; flash_check PASS (24 flashes, worst 1 s = 2 at 37 s); seams = neighbours, no duplicates; 1:1 frames at 0:44/0:47/0:54.6/0:58/1:03/1:45/2:20/2:26/5:01 clean.

## v5 (2026-11-05 night, docs/BRIEF_dopa_long1f.md): `scenes/ol_longform_domino5.py` (imports v4; v4 untouched)
- **One rigid card per object** (`card_mat`): weak perspective at the base anchor (local axes rotated into the camera, scale f/depth); sphere = similarity at its centre. It replaces v4's strip_mats in the renderer AND the solver checks. The plain tangent of the projection explodes as 1/d^2 near the camera plane (whole-screen smears); weak perspective goes off screen to the right instead.
- **Layout re-checked under the card projection** (`repair_layout`, `--relayout`, cached in `scenes/ol_longform_domino5_layout.json`; overlap tolerance 6%): 39 objects moved; 3 dropped (highest skydive, the rubber-duck comet, Halley's Comet) → 158 kept. 16 pairs still overlap 6-20% of the smaller object.
- **Labels:** one fixed offset per label, chosen offline in pass order (`solve_offsets`: 10 candidates, dx in label widths, lift in label heights, checked at pass +0.3 s and +2 s against already-fixed labels and the HUD zones). Rigid with the object, no clamp. Newest first, and a label overlapping a newer one or the HUD fades by the overlap (continuous, deterministic per frame). No 7-label cap.
- **Joke ending:**
  - J0 = T_LAND + 5.0 (the card fades out over 0.6 s), then the camera pans on (+4.0 s, smoothstep, 2.8 s).
  - Domino 587 is appended to the chain lists at x = 6.5 H586, out of reach of the fallen gold tip (4.9 H). It wobbles about its front edge (7.5 deg, decaying) and never falls.
  - The silhouette: dark dome, violet rim, x = 13 H, size 4.2 H. Label "YOUR MOM" / "∞ (sorry)" on its left flank; banner "DOMINO 587 vs YOUR MOM" then "...nope.".
  - Sound: 3 soft low wood knocks; the bed's tail fades naturally. T_END = J0 + 6.6 → 9:19.5 (33,570 frames).
- v5a was stopped (16 residual 6-20% overlaps from the 6% repair). **v5b layout**: a full fame-tier re-solve under the card projection with v4's rule (`--resolve`, OV_THR 0.02), then a symmetric repair (each object re-checked from its OWN samples too; the less famous of a pair moves first; tier 1 yields) → 149 kept, 29 dropped. 3 residual contacts of <=7% (person/tallest man while entering at 0:46.3, tallest man/corpse flower when tiny far left, phone/beetle). Lesson: the solver only checks a new object against earlier ones at the NEW object's sample times, so the post-hoc symmetric check finds more.
- Render: `--render --label v5b`.
- **v5 DELIVERED (2026-11-06), label v5b:** `<VIDEOS_DIR>\DopamineExe\review\domino_v5\` (video 9:19.5, README, UPLOAD_notes with 149 objects, 4 thumbnails); v4 moved to `archive\domino_v4\`. Render 97 min, 19 chunks. Checks on the encoded file: h264 yuv420p 60 fps, 33,570 frames, PTS step 256; -14.0 LUFS, TP -2.3; flash_check PASS (worst 1 s = 2); seams = neighbours, no duplicates.

## v6 (2026-11-06, docs/BRIEF_dopa_long1g.md): `scenes/ol_longform_domino6.py` (imports v5; v3-v5 untouched)
- **Units:** `imperial()` / `size_label6` patched over S.size_label in-process. Imperial first, " / " then metric; miles for >= 1 mile (3 s.f. from 10,000 miles; million/billion/trillion miles mirror size_parts); light-years only. The HUD (big imperial, small metric), the meter ticks (1 ft, 1 mile, ...), the meter start "0.6 in", START "0.6 in / 1.5 cm", the caption and the finale card are all overridden in Journey6.
- **Late names (cause):** v5 labelled only passed objects + the single next one, which faded in by its anchor x (1800 → 1500); giant objects also had their top anchor off screen while entering. **Fix:** every drawn object gets a label whose alpha follows its own clearness (visible bbox / min(bbox, a quarter of the frame)), and each object has a fixed anchor (height fraction x left-flank fraction) + offset solved offline (`solve_offsets6`, 4 moments: visible, +1 s, pass +0.3 s, pass +2 s; penalties for off-screen, HUD, fixed labels, low anchors). RELAX giants may anchor on their left flank (`GIANT_ANCHORS`). Priority: passed + up to 2 ahead (newest first), then entering ones (nearest first); the lower-priority label fades on a collision.
- `--labelcheck`: late (> 1 s after >= 30% visible and >= 70 px) v5 132/149 → v6 0. Collision fades: v5 110 objects / 379 s, v6 88 / 431 s.
- **Voyager:** S = 2.59e13 m (one light-day, NOV 2026); still domino 311; custom sub-line + an extra line ("one light-day from Earth").
- **Watch 0:04:** the caption sits on a stronger soft dark panel (layout unchanged).
- **4K:** S.dev_path patched to set the device base matrix (v3 called identity_matrix, which assumed a 1920x1080 device); sky layers are built at device resolution and painted under the identity matrix; bloom sigma x SC. A 4K frame takes 0.7-1.1 s to draw.
- **Shutdown-safe render:** CHUNK_F 900; tmp → fsync → rename; stale tmp_* deleted on start; the last 2 chunks are ffprobe-checked (frame count + size) on a restart; `PROGRESS.txt` in the chunk dir has the resume command (cmd.exe) on top. Audio = v5's wav (same timeline).
- **v6 DELIVERED (2026-11-06), label v6a:** `<VIDEOS_DIR>\DopamineExe\review\domino_v6\domino_full_4k.mp4` (3840x2160, 9:19.5) + README, UPLOAD_notes (imperial-first title/description, Voyager light-day line), thumbnails (thumb 1 "0.6 in TO THE UNIVERSE"); v5 moved to `archive\domino_v5\`. Render 271.9 min (38 x 900-frame chunks, about 7 min each; one crash: fsync on a read-only handle under Windows, fixed with an r+b handle, the complete tmp chunk was kept). Collision fade threshold 0.10 (v5 0.25) after the 2:06.5 Golden Gate / $1B check; Malin 1 added to RELAX. Checks on the encoded file: h264 yuv420p 3840x2160 60 fps, 33,570 frames, PTS step 256; -14.0 LUFS, TP -2.3; flash_check PASS (worst 1 s = 2); 37 seams clean; 1:1 crops of the watch, labels, Voyager and the card are clean.
- **v6b (2026-11-06, docs/BRIEF_dopa_long1h.md):** shadow/contact pops fixed. v4's draw_obj drew obj_shadow + contact only for u = k - cidx <= 2.5 (faded 2.5 → 1.5): a strip-era workaround. Journey6.draw_obj now draws both whenever the card is drawn; `_ground_mats` uses the exact projection while the depth ratio across the ground vectors is >= 0.6 (identical to v6a there) and blends into the anchor's weak perspective near the camera plane (never None/pop). Reflections were not u-gated (only sc < 6). "YOUR MOM" → "YO MAMA" (label + banner "DOMINO 587  vs YO MAMA"). Affected frames (eligible i < EARTHLY+20 objects drawn with u > 1.5 or a depth ratio < 0.61): chunks 0-14 (to frame 13500); joke: chunks 36-37. Chunks 15-35 copied byte-for-byte from v6a into chunks_v6b. Gotcha: GNU sed "\u" in a replacement uppercases the next character (it ate the ∞ escape).
- **v6b DELIVERED (2026-11-06):** review\domino_v6\domino_full_4k.mp4 = v6b (render resumed after a blue screen at chunk 4); v6a file moved to archive\domino_v6a\. Checks: ffprobe 3840x2160 60 fps 33,570 frames, PTS step 256; -14.0 LUFS, TP -2.3; flash_check PASS; 37 seams clean; frames 3600/4500 match fresh renders (0.44 mean diff vs ~3.7 for neighbours).
