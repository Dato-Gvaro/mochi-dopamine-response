# comment_overflow — reply to @<viewer>: "i thought it reached 2147483648"

- Comment on press_split2 ("Every ball crushed splits into 3 💥 Press or Hammer?"). 2,147,483,648 = 2^31, the value a signed 32-bit counter cannot hold. Owner approved the build 2026-10-22.
- New scene file (`scenes/comment_overflow.py`); press_split2 untouched, no lib/ or tools/ changes.
- **ONE nameable change: x2, not x3**, so the count runs through exact powers of two and lands on 2^31.
- Caption (in-scene, 2 lines, 64 px): "Every ball ~CRUSHED~ splits in 2" / "until the counter hits ~2,147,483,648~" (number in red).

## History (2026-10-22/23)
- **v1:** one chamber filled with grains, then "● = N balls" legend waves. Owner: "after 256 balls the jar already looks filled; every increase has no visual effect".
- **v2/v3:** the full chamber duplicated into a wall of jars. Owner: "we don't need more jars, we need more balls".
- **v4:** an infinite zoom INTO the pile. Owner: "still doesn't have a good-looking effect".
- **v5a** (not delivered): each jar imploded into one ball inside a bigger jar. Owner clarified (sketch): the jar BREAKS and the SAME balls end up in a bigger jar.
- **v6 = v5.2 + MUSIC FIRST (owner 2026-10-23: "the music is still not pleasant to listen to"):**
  - **The soundtrack is the piece, played as music.** Für Elise (Beethoven 1810, PD), both hands from the Mutopia MIDI (piece 931). One steady tempo: a quarter = 0.5 s, dotted quarter = 80 bpm in 3/8.
    - Arrangement via lib/orchestra (MuseScore_General, MIT):
      - Grand piano: right hand legato ×1.18; left-hand notes held to the bar line (pedal).
      - A soft strings_slow pad on each bar's harmony (taken from the left hand).
      - A light contrabass on each bar's lowest note, an octave down.
      - A gentle crescendo through the piece.
    - It plays from the pickup to the A cadence at beat 34.5 (A section, B section, return).
    - No event-triggered notes, stutters or bursts in the music. The sidecar lists the melody as played (98 notes).
  - **The visuals follow the music grid:**
    - Press contacts on beats: the CUP on eighth notes 0.25–2.0 s; then every 1.25 / 1.25 / 1 / 1 / 0.4 beats.
    - Each container breaks on a phrase end: beats 5, 11, 18, 24, 30 = 2.5 / 5.5 / 9.0 / 12.0 / 15.0 s.
    - Each break → slump → zoom → the next press contact spans exactly one bar (0.75 s).
    - +1 at beat 33.5 (16.75 s). The flip and the SILO collapse land on the final A cadence (beat 34.5 = 17.25 s), with a rolled A-minor piano chord, strings, low bass and soft oohs.
    - The plate speeds up if needed to land ON the beat: contacts measured within ±0.02 s of the grid.
  - **SFX are quiet under the music:**
    - A soft tonal knock per stroke (0.03).
    - A sparse squelch texture (0.01, ≥ 60 ms apart).
    - Glass = a gentle A-minor tinkle of sine pings (0.012). No noise bursts.
    - Overflow = soft tonal bit-blips (0.012).
    - The collapse = a soft low thud (0.05) and a tinkle.
  - **Leveller:** a slow gain ride (0.8 s RMS, 0.7 s smoothing, ±6 dB) keeps the body flat and sets the cadence +6 dB before mastering (measured +2.9 dB after).
  - Clip 19.77 s (1186 frames).
- **v5.2 (owner clarification, 2026-10-23):**
  - **Finale:** no freeze and no invisible walls. When the SILO breaks, its walls, housing and plate fly away and the sim switches to "collapse": only the floor is left (side walls gone, dense-pile speed cap raised from 260 to 800 px/s). The pile slumps and pours out into a wide heap, partly off the screen edges, on a faint ground line.
  - **Every earlier break:** the old plate holds through the 0.14 s cracks. Then the glass is gone and the pile slumps outward under gravity for 0.28 s (SLUMP) before the zoom-out starts and the bigger container catches it.
  - **Music is continuous through every break and zoom:** melody notes keep walking ~0.15 s apart from the break to the next press contact, the glass tinkle is lowered to 0.08, and the riser and pad continue. RMS per second now stays −14.6…−16.4 with no dips (v5.1: −18.0 at breaks).
  - Clip 19.42 s (the slump adds 0.28 s per break).
- **v5.1 (owner review of v5, 2026-10-23):**
  - The "JAR n" labels became made-up escalating containers: **CUP 0.3 L → JAR 1 L → BUCKET 10 L → BARREL 200 L → TANK 5,000 L → SILO 1,000,000 L**. The name sits on the housing (30 px gold), the capacity on the cylinder (20 px). Silhouettes stay straight-walled, so the physics is unchanged.
  - **Finale:** the balls no longer erupt. At the flip the SILO's glass, housing and plate fly away, but the sim FREEZES: the pile stands as a still block in the container's exact shape, held by invisible walls. A slow soft sheen sweeps across it (white at alpha 0.07 per layer, a 55 px diagonal band every 1.3 s). That impossible block is the punchline.
- **v5.** Lessons:
  - Keep the same objects visibly multiplying.
  - Containers growing around them reads; containers copied or merged does not.

## Mechanic (v5): growing jars, one continuous granular sim
- **Jar 1:** the press_split2 opening, with the comment card first. 1 → 256 balls by 1.92 s (KR 0.805); 256 fill the jar.
- **The jar BREAKS (SETTLE 0.10 s after its last crush):**
  - Cracks run across the glass for 0.14 s.
  - Then the glass walls (16 pieces), the housing halves and the plate halves fly OUTWARD and fade.
- **The camera ZOOMS OUT** (0.62 s, smooth in log scale) about the floor anchor (508, 1250).
  - In the sim, the SAME balls (positions, radii, velocities) shrink by 1/s.
  - The walls of the next, s× bigger jar close in from off-screen (factor w = s·λ → 1), and the balls settle into it, filling ~35 % / ~27 %.
  - Its bigger press comes down DURING the zoom (jar coordinates scaled by w) and makes contact right as the zoom ends.
- **Six jars, 8 + 4 + 5 + 5 + 5 + 4 = 31 doublings.**
  - Jar scale per jar s = 1.296^(waves/2): 1.68 / 1.91 / 1.91 / 1.91 / 1.68. The pile's area grows ×1.296 per wave, so each jar fills exactly by its last wave.
  - Wave periods per jar: opening, 0.46, 0.40, 0.36, 0.32, 0.30 s (faster each jar). Crushes spread over 40 % of the period, top layer first.
- **Honest drawing:**
  - Balls really split until 1,024 (wave 10). From wave 11 each drawn ball stands for M balls: a crushed ball SWELLS ×1.296 in area instead of splitting (its M balls became 2M), and M doubles.
  - Legend "● = M balls" from 4 to 2,097,152. The counter = n × M, exact.
  - Balls shrink with every zoom-out and swell back as they are crushed: ~5–10 px on screen in the later jars, a dense rainbow texture.
- **Container labels (v5.1):** CUP / JAR / BUCKET / BARREL / TANK / SILO with 0.3 L / 1 L / 10 L / 200 L / 5,000 L / 1,000,000 L.
- **Colours:** every child/crushed ball's hue moves 45 % toward a smooth diagonal screen gradient (±5° by side), saturation 0.75. The gradient drifts +40° per jar: green → teal → blue → violet → magenta. Each jar's glass has its own colour, and a "JAR n" label sits on the housing.
- **Finale:**
  - The last crush of wave 31 = 2^31: the counter shows 2,147,483,647 (gold, held 0.40 s, "+1").
  - 0.55 s glitch: scramble, RGB split, slice jitter, no white flash.
  - Then **−2,147,483,648** in red: the SILO's glass, housing and plate fly away and the pile COLLAPSES with real physics into a wide heap (v5.2; v5.1 froze, v5 erupted). "INTEGER OVERFLOW" + a drawn boom.
  - Mochi: wow → annoyed. Bolt: laughs.

## Timeline (clip, seed 0)
- 0 s: comment card, one big green ball under the descending plate, "1 / 2,147,483,648". First split 0.06 s.
- 0.5 s: 4. 1 s: 16. 2 s: jar 1 full, 256, caption up.
- Jar breaks 2.02 / 4.52 / 7.20 / 9.68 / 12.03 s; new jars ready 2.72 / 5.22 / 7.90 / 10.38 / 12.73 s.
- 5 s: jar 2, 4,096 (● = 4 balls), its press crushing.
- 9 s: jar 4, 1,048,576 (● = 1,024).
- 13 s: jar 6 filling, 268,435,456 (● = 262,144).
- Milestones: 1 THOUSAND 3.48 s, 1 MILLION 8.83 s, 1 BILLION 13.53 s.
- 13.85 s: 2,147,483,647. 14.25 s: +1 → glitch. 14.80 s: flip + jar 6 shatters, pile erupts, cadence.
- Dissolve 17.12–17.72 s into the pre-roll. Clip **17.72 s** (1063 frames).
- The clip starts at sim 1.00 s (CLIP0), so the plate is slower at the seam (seam 1.01, was 1.10).

## Sound
- One note per sampled crush walking **Für Elise** (Beethoven 1810, PD), notes from the Mutopia MIDI (piece 931, right hand, the press_break list).
  - 1 note per wave for waves 1–8, 2 for waves 9–17, 3 from wave 18 (the rate climbs with the faster jars).
  - Rotated so the +1 note is FUR_ELISE[34], the A closing bars 1–8.
  - 69 notes, 12 distinct.
- Crisp squelch per crush (rate-capped 24 ms, ducked by density). Press thunk + clank per stroke.
- **Each break:** two light glass cracks, a clank, and a tonal glass tinkle (E5 C5 A4 E4 C4 sine pings, 50 ms apart, no noise). Then a riser into the bigger press's first contact.
- An A open-fifth pad rising with the count. Overflow stutter + bit-crush blips + power-down glide. The A-minor cadence lands at the flip.
- Mastering `peak_db=None`; post-master fade so the last 0.5 s is digital silence.

## Checks (v6, encoded Full HD)
- h264 yuv420p 1080x1920, 60 fps, **19.77 s** (1186 frames).
- −14.01 LUFS, peak −5.9 dBFS (peak_db=None), last 0.5 s silent (−240 dB).
- **RMS per second:** −16.1, −17.0, −17.1, −15.9, −17.0, −17.2, −16.7, −17.4, −16.4, −16.8, −16.2, −15.4, −16.9, −17.2, −15.7, −16.9, −17.3, −14.3 (cadence), −16.6, −62.5 (fade).
  - The body stays within ±1 dB of −16.5.
  - The break seconds (2, 5, 9, 12, 15) read −17.1 / −17.2 / −16.4 / −16.9 / −15.7: no dips or spikes.
- Finale momentary max −10.9 vs body median −13.7: **+2.9 dB**.
- flash_check 0 flashes. Seam 0.94.
- Side safe zone 0.104–0.836 w through 16.75 s. The collapse heap spreads wider (decoration).
- Frames read from the encoded file at 0, 2, 2.67, 5, 9, 13, 16.75, 17.67, 18.67, 19.75 s.
- **4K ship render** `output/comment_overflow_ship_9x16.mp4`:
  - Video: h264 yuv420p 2160x3840, 60 fps, 19.77 s (1186 frames).
  - Loudness: −14.01 LUFS, peak −5.9 dBFS, last 0.5 s silent.
  - Seam 0.86. flash_check 0 flashes. The same RMS per second.

## Checks (v5.2, encoded Full HD)
- h264 yuv420p 1080x1920, 60 fps, **19.42 s** (1165 frames).
- −14.00 LUFS, peak −8.0 dBFS, last 0.5 s silent (−240 dB). Finale +3.5 dB over the body.
- RMS per second: −15.7, −16.0, −16.3, −16.2, −16.4, −16.2, −16.1, −16.2, −16.4, −15.5, −15.8, −16.0, −15.3, −16.1, −15.6, −15.9, −14.6 (flip), −16.0, −29.0 (fade), silent. No dips at the breaks.
- flash_check: 0 flashes (mean luminance 0.030). Seam 1.00.
- Notes: 104 (12 distinct); check_clip events/5 s: 34, 46, 24.
- Timings: breaks 2.02 / 4.83 / 7.85 / 10.68 / 13.40 s; bigger containers ready 3.07 / 5.88 / 8.90 / 11.73 / 14.45 s. 2,147,483,647 at 15.55 s, +1 at 15.95 s, flip + SILO collapse at 16.50 s. Milestones 3.80 / 9.85 / 15.23 s.
- Side safe zone 0.104–0.836 w through the transitions. The collapse heap spreads to the screen edges (decoration, below the caption, above the HUD).
- Frames read 1:1: 2.03 s (cracks, old plate holding), 2.33 s (glass flying, the pile slumping out), 2.67 s (the bigger JAR catching it), and the collapse at 16.50 / 16.83 / 17.33 / 18.0 / 18.67 s.
- **4K ship render** `output/comment_overflow_ship_9x16.mp4`:
  - Video: h264 yuv420p 2160x3840, 60 fps, 19.42 s (1165 frames).
  - Loudness: −14.00 LUFS, peak −7.95 dBFS, last 0.5 s silent.
  - Seam 0.92. flash_check 0 flashes.

## Checks (v5.1: identical numbers to v5 except mean luminance 0.029; encoded Full HD, <VIDEOS_DIR>\MochiAndBolt\review\batch47\comment_overflow.mp4)
- h264 yuv420p 1080x1920, 60 fps, 17.72 s.
- −14.00 LUFS, peak −7.3 dBFS, last 0.5 s silent (−240 dB).
- RMS per second: −15.0, −15.2, −18.0 (break 1 + zoom), −16.0, −16.6, −16.3, −15.6, −17.9 (break 3), −14.9, −15.6, −16.3, −14.9, −17.0, −14.8, −15.3, −13.9 (flip), −21.3 (fade), silent.
- Finale momentary max −8.9 vs body median −12.7: **+3.8 dB**.
- flash_check: **0 flashes** (mean luminance 0.028). The only large-area transition is a monotone darkening at 2.57 s (the first zoom-out).
- Seam **1.01** (normal steps 0.89–0.90; v5a was 1.10).
- check_clip events/5 s: 20, 34, 15 (the last window ends at the +1 at 14.25 s).
- Side safe zone, encoded frames 0–14.85 s: 0.106–0.833 w. The frozen block and the HUD at 16.33 s: 0.106–0.833 w. Only the flying glass at the flip reaches 0.86 w (decoration).
- Labels read 1:1 on encoded frames: CUP 0.3 L (0 s), JAR 1 L (3.5 s), BUCKET 10 L (6 s), BARREL 200 L (8 s), TANK 5,000 L (10.33 s), SILO 1,000,000 L (13 s). Frozen block read 1:1 at 15.0 and 16.33 s.
- **4K ship render** `output/comment_overflow_ship_9x16.mp4`:
  - Video: h264 yuv420p 2160x3840, 60 fps, 17.72 s (1063 frames).
  - Loudness: −14.00 LUFS, peak −7.31 dBFS, last 0.5 s silent.
  - Seam 0.92. flash_check 0 flashes.
- Frames read from the encoded file at 0, 0.5, 1, 2, 2.13 (cracks), 2.33 (glass flying, zoom), 2.67, 5, 9, 13, 13.9, 14.85, 15.33, 17.70 s.

## Nits / doubts
- **Seconds with a break dip to −18 dB RMS**, against ~−15.5 in the body. The tinkle and riser fill them, but they are the quietest moments.
- **From 1,024 balls on**, a crushed ball swells instead of visibly splitting. This is honest via the legend, but the per-ball split is only literal in jars 1–2.
- **The balls in jars 4–6 are small (~5–10 px):** the owner asked for honest shrinking.

## Args / cost
- `--seed` (0), `--cap`, `--label`, `--cache` (pickles the sim in output/), `--still --frame a,b`, `--report`, `--reuse`.
- Sim ~5 s; Full HD render ~1 min at 2 encoder threads, BLAS threads 1.
- Delivered `<VIDEOS_DIR>\MochiAndBolt\review\batch47\comment_overflow.mp4` (Full HD v6, overwrote v5.2). The 4K v6 ship render is ready in output/. Owner review: pending.

Owner review (2026-10-23): v5 -> v5.1: container sizes (CUP→JAR→BUCKET→BARREL→TANK→SILO) instead of JAR n; finale: walls break but the balls stay boxed as if held by invisible walls (no spray).

Owner review (2026-10-23): v5.1 -> v5.2: NO freeze; when the silo breaks the balls must collapse and pour out naturally (no invisible walls); the music must flow continuously through the container transitions (it cut out unpleasantly).

Owner (2026-10-23): "the music is still not pleasant" -> rebuild the soundtrack music-first (steady natural tempo, real phrasing, visuals synced to the music grid, quiet tonal SFX).

## ASMR variant (owner 2026-10-23): no music, the press and the balls only
- Audio only: the same v6 picture, re-muxed with `-c:v copy -t 19.7667` (never -shortest).
- Command: `python scenes/comment_overflow.py --cache --asmr --video <v6 mp4> --out <mp4>`. `build_asmr()` builds the track from the same sim.
- **Press:** a hydraulic "chunk" on every contact: a 52→122 Hz pitch-dropping thud with a 4 ms attack and tonal 176 / 412 Hz body. No hiss.
- **Balls:**
  - Every split or crushed ball gets a glossy marble click: 3 inharmonic partials, 1.8–3.2 kHz, 10–18 ms ring, low-passed at 6 kHz. Balls larger than r 25 get a rounder 0.7–1.1 kHz clack.
  - Clicks run on 6 voices, at least 12 ms apart each, gain ducked by density.
- **Rattle / pour:** soft clicks at a rate of 2.4 × (number of moving balls) per second, capped at 520/s, on 8 voices at least 12 ms apart.
  - The ball motion comes from the sim frames with the zoom scaling removed.
  - This makes the settling after each zoom-out a soft cascade, and the SILO collapse a big avalanche (×1.6) that swells and thins. No white noise.
- **Breaks:** a glass crack (4 short tonal shard ticks, 2.6–4.2 kHz) plus a light tinkle (10 shards, 1.8–3.6 kHz, 50–120 ms rings).
- **Overflow:** 5 soft tonal bit-blips.
- **Collapse:** a deep chunk + crack + 16 shards + the avalanche.
- No music, pads or drones. The leveller is the same as v6 (+6 dB lift into the finale).
- **Checks (Full HD `<VIDEOS_DIR>\MochiAndBolt\review\batch47\comment_overflow_asmr.mp4` and 4K `output/comment_overflow_asmr_ship_9x16.mp4`, identical audio):**
  - 19.77 s (1186 frames); −14.05 LUFS, peak −5.5 dBFS, last 0.5 s silent.
  - RMS per second: −16.9, −16.4, −17.5, −16.5, −17.5, −17.1, −16.4, −17.6, −15.9, −17.6, −16.4, −16.3, −17.4, −16.5, −16.2, −17.9, −16.7, −13.9 (avalanche), −15.5, −45.1 (fade).
  - Finale +4.0 dB over the body median.
  - Energy above 6 kHz: 0.12 %.
  - flash_check 0. Seam 0.94 (Full HD) / 0.86 (4K).

Ship (2026-10-23): owner kept v6 (music) -> 4K staged at MochiAndBolt/schedule/2026-10-29 slot 2.
