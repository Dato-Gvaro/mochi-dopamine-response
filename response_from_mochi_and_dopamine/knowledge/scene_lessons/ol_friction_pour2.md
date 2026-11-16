# ol_friction_pour2 (DopamineEXE, redo of ol_friction_pour, 2026-11-01)

Owner on v1: "interesting to watch but can't figure out what's the difference". Coordinator (owner rule "if you disagree, make it your way"): REDO with a real, visible difference. v1 stays runnable (`scenes/ol_friction_pour.py`, `docs/scenes/ol_friction_pour.md`).

## What it is
Two lidded jars with a central mouth, the pour doubling every 2 s. Left: smooth round BALLS (frictionless). Right: rough angular GRAINS (bent 3-disc shards drawn as irregular polygons, Coulomb μ 0.6). Each spawn is a PAIR of exactly equal area at the same place, time and speed, so both jars always hold the same amount. Balls spread flat; grains heap into a steep cone whose live slope is measured on a protractor. The cone reaches the mouth while the corners under the lid are still empty, the neck clogs and the grain jar overflows first.

## Truth over brief (read before changing the caption/end card)
- **The brief's mechanism is wrong for an OPEN jar:** a heap's peak can stand above the rim; grains only spill when the slope's foot reaches the rim, so the cone makes an open jar hold MORE. Hence the lid + mouth: then the cone hits the mouth while the corners are empty (that part of the brief is real).
- **Packing is NOT looser for the grains in this model:** area fraction 0.84-0.88 for both (shards nest). Equal amount → nearly equal FULL % at any moment (settled 90% vs 93% in the shipped run). The only difference is WHERE the empty space is (corners vs a flat band on top) and that the grain neck clogs.
- **The steep angle is the DYNAMIC angle (fed by the pour).** Stop-the-pour test (seed 2, pour closed at 3 s): a 40-50° heap relaxes to a static ~20-29° within ~1.5 s, then holds. So after the overflow the grain pile partly slumps; the finale's empty regions are modest.
- Overflow = a piece actually leaves the jar (over the collar onto the lid) while the pile touches the lid; both spouts close at that instant. A 'clogged neck' rule (≥2 resting pieces at the brim, `--clog`) was tested and dropped: the neck reached the brim at ~76% but kept absorbing the stream (0 grains out), so it was no overflow. Cost of the honest rule: the grain stream backs up in the neck as a short column (~0.15 s) before it spills (the 4-column spout feeds it neatly; `--jit 2 --vxsd 45` scatter softens it).

## Model (`simulate`, seeded, ~4-5 min CPU on one thread)
- PBD, 1 m = 1000 px, g 9.81 m/s², **16 substeps** × 8 Jacobi iterations (×1.5 relaxation). 8 substeps compressed the pile (area fraction 0.92-0.98, overlap ~12% of a sub-disc radius) and hid every difference: never go back.
- Grains: rigid clumps by 2-D shape matching every iteration + a rigid velocity projection. Shapes: a middle disc r 3.6-4.4 + one each side at 3.2-4.1 px, bent ±0.6 rad (aspect ~1.8), × a per-pair size factor 0.82-1.18 (equal discs crystallise into stacks that hold fake slopes). Drawn as a 6-8-vertex polygon inscribed in the union.
- Balls: equal-area discs, μ 0 (ball-ball and glass).
- Friction: position-level Coulomb capped by μ × the ACCUMULATED normal correction of the substep (capping by one iteration's correction let heaps creep flat). Glass μ 0.5.
- Contacts may add at most 60 px/s per substep (`--vgain`; 5 = paste-like balls that dome, 250 = fluidised grains), restitution 0.4 for both (`--rest`; without it PBD sent pieces back up out of a clogged neck at full speed: a geyser).
- Pour R(t) = 3 × 2^((t + 6)/2) pieces/s per jar (pre-roll 6 s → frame 0 is mid-pour). Spout 80 px, 4 columns, 1700 px/s, capacity ~347/s (queue never builds).
- Jars: inner x 120-410 / 610-900, lid y 760 (FULL), mouth 100 px with a 34 px collar, floor y 1140.
- FULL % = mean height of the pile's top (all but the falling stream, 10 px bins) under the lid, eased 0.12 s. Angle = line fit to each flank's tops between the glass and the stream's impact zone (bins pressed to the lid or empty skipped), eased 0.25 s; the protractor shows the outer flank and fades 0.3-0.7 s after the overflow.

## Seeds (final model): grains overflow first in 3/3
| seed | grain spill | balls spill | settled FULL balls / grains | flank angle over the pour, median (IQR): balls / grains |
|---|---|---|---|---|
| **1 (shipped)** | 7.04 s | none in clip | 93.3% / 90.4% (10 grains out) | 13.0° (8.3-17.8) / 50.2° (44.9-55.1) |
| 2 | 7.23 s | none | 95.0% / 92.5% (14 out) | 14.1° (10.1-18.1) / 50.5° (45.8-53.7) |
| 3 | 6.99 s | none | 93.5% / 90.8% (10 out) | 13.9° (10.1-17.9) / 49.2° (43.0-53.8) |

Angles are the DYNAMIC (fed) slope; the balls' 13-14° is mostly the stream's impact dome (settled ball surface −1 to 10°). Static grain repose in this model ~20-29° (stop-the-pour test). Earlier tuning runs (for the record): round 3-disc blobs packed denser than the balls (0.88 vs 0.84) and tied; 8 substeps compressed the pile 12%; uniform sizes crystallised the balls.

## Timeline (seed 1, 591 frames, 9.85 s)
- 0 s: 60 pieces per jar, both streams pouring; balls flat (~10°), grains a small heap · ×2 pill at 2, 4, 6 s · 2 s 130 · 4 s 269 · 5 s 385 (FULL 42% / 45%, grain cone 59°, balls 13°) · 6 s 548 · 6.9 s grains back up in the neck (~0.15 s column) · **7.04 s grains spill = OVERFLOW!** (787 per jar; spouts close; glass-harp chord) · 7.5 s "still room on top" · 7.84 s "SAME AMOUNT / the rough one overflowed at 90% full", gold EMPTY regions (balls: flat band; grains: corners beside the mound) · settled FULL 93% / 90%, 10 grains on the lid · 9.25-9.85 s dissolve to frame 0.

## Screen
- Caption (baked; `--cap ''` = base): `Smooth ^BALLS^ vs rough ^GRAINS^, pour DOUBLES…|until one jar ~OVERFLOWS~`.
- Pieces coloured by pour band (one hue per doubling). Thin white jars, gold dashed FULL line under each lid from frame 0, gold brim on the overflowing jar.
- Under each jar: SMOOTH BALLS / ROUGH GRAINS, "μ 0 · roll and flow" / "μ 0.6 · lock and heap", FULL meter with a gold end mark.
- Counter (big) + ×2 POUR pill + "SAME VOLUME IN EACH JAR".
- Finale: OVERFLOW! over the grain jar, "still room on top" over the balls, "SAME AMOUNT / the rough one overflowed at X% full" (X = the settled FULL value, = the meter), gold-filled EMPTY regions under both lids.
- Side safe zone: jars + labels x 120-900 (0.11-0.83w); content ≤ y 1316 (0.69h); counter 1500.

## Sound (ASMR, owner rule for pours)
- Per jar landing ticks (≤3/frame, density-scaled): balls = soft rounded glassy patter; grains = dry gritty click (band-limited crunch over a small pitched body). D-major pentatonic, low/mid. Shimmer per piece spilling. Wooden tok per doubling. One rich D-major add9 glass-harp chord (strummed 12 ms) on the overflow. No music bed (pours = ASMR only; the channel brief's "note per event" rule is overridden for pours).

## Checks (encoded Full HD, `<VIDEOS_DIR>\DopamineExe\review\fixes_1101\ol_friction_pour_v2.mp4`)
eview\fixes_1101\ol_friction_pour_v2.mp4`)
- h264 High yuv420p 1080x1920 60 fps, 591 frames, 9.85 s; AAC 48 kHz stereo.
- **-13.97 LUFS** (muxed, stereo), peak -3.88 dBFS, last 0.5 s digital silence; RMS per 5 s -23.8 → -14.9. Landing ticks/s 26, 15, 76, 77, 95, 150, 225 up to the overflow.
- flash_check PASS (0 flashes, mean lum 0.015). Seam mean |Δ| 0.235 (good band).
- Stills read (Fast) at 0, 5, 6.8, 7.07, 7.4, 8.3 s; 1:1 crops of the encoded file at 7.07 s (grain neck, 40° protractor) and 8.7 s (card + EMPTY regions).
- Safe zone: key content x 120-900 (0.11-0.83w), content ≤ 0.69h.
- Blemish: the grain EMPTY outline can spike where a single grain sits in the neck.

## Flags
`--seed --label --cap --still --frame --dry --resim --audio --sound 0 --verbose`; physics `--mu (0.6) --muw (0.5) --sub (16) --iter (8) --relax (1.5) --vgain (60) --rest (0.4) --accum (1) --shape chain|blob --sr0/--sr1 --sd0/--sd1 --sz0/--sz1 --nsub`; pour `--r0 (3) --pre (6) --vp (1700) --spw (80) --mw (100) --close (0) --hold (2.2) --tmax`; stream `--jit (2) --vxsd (45)`; tests `--stopat T` (close the spouts at T), `--clog` (also stop on a clogged neck).

## Upload draft (true to seed 1)
- `Smooth balls vs rough grains: which jar overflows first? 🫙 #satisfying #physics #shorts`
- `Same pour, same jar… rough grains heap at 50° and spill first 🫙 #satisfying #physics #shorts`
- `The pour doubles every 2 seconds until one jar overflows 🫙 #satisfying #physics #shorts`
- Pinned: `same amount in both jars the whole time. the rough ones pile up steep, jam the neck and spill with the corners still empty. did you guess the grains?`
- No description (no owner track).

- **STAGED 4K** (2026-11-01): `--label v2k4 (defaults, seed 1)` at NF_SCALE 2.0 -> `<VIDEOS_DIR>\DopamineExe\schedule\2026-11-14\2_ol_friction_pour.mp4` (events json byte-identical to the reviewed Full HD). 2160x3840 h264 yuv420p 60 fps, 591 frames, -13.97 LUFS, peak -3.88, flash 0, seam 0.14. Full HD -> archive/ol_friction_pour_v2.mp4.
