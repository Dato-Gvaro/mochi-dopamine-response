# pool_splash — Cannonball or belly flop: who makes the BIGGEST splash? (batch59, 2026-10-29)

- Brief: docs/BRIEF_batch59.md (Mochi & Bolt 4). New scene file; caption/banner/HUD/sound chain copied from paper_plane / coffee_milk; lib/ and tools/ untouched.
- Deliverable: `<VIDEOS_DIR>\MochiAndBolt\review\batch59\pool_splash.mp4` (**v1**, Full HD 9:16, 14.43 s, 866 frames; output label v1).
- Caption (baked; `--nocap` gives the base): "~Cannonball~ or ~belly flop~:" / "who makes the ~BIGGEST~ splash?"
- **Story:** side view of a pool with a measuring wall (1-4 m dashed lines). Frame 0: both are mid-air off two 3 m boards: Mochi tucked into a ball, Bolt spread flat. Bolt hits at 0.44 s, "SLAP!" (comic burst), and slow-mo kicks in (x10, shown in the HUD). "BELLY FLOP: A WALL OF WATER!": his wide sheet leads (1.4 m vs her 0.7 m crown). Under water, Mochi drags a labelled AIR POCKET. 3.8 s "THE AIR POCKET SLAMS SHUT…", 5.8 s "…AND SHOOTS A JET UP!": the jet passes the belly flop and climbs (slow-mo x7) to 3.8 m on the cadence (10.94 s): "MOCHI WINS · 3.8 m vs 1.4 m". Back to real speed: Mochi pops up laughing; Bolt floats up bright RED, deadpan, a little steam: "(Bolt won the loudest SLAP)".

## Layout
- Water surface y 1090, 172 px/m (4 m line y 402), underwater view to y 1370 (1.63 m) so the air pocket reads. Characters r 83 px (0.48 m). Lanes x 273 (Mochi) / 764 (Bolt). Bolt's spread limbs reach ~x 935 (decoration); the belly-flop spray flies off both edges (water only).
- Peak-hold markers per diver (coloured line + "x.x m" tag); HUD y 1376-1554: SPLASH HEIGHT per diver, HIGHER pill, the live slow-mo factor.
- Static camera, no zoom; deep blue dusk sky so the white water reads; no flash.

## The physics (honest-ish; real seconds)
- Same board (3 m), same jump (1.2 m/s up): impact 7.8 m/s (Mochi, tucked) / 8.0 m/s (Bolt, flat lands a touch lower).
- 7,320 droplets, each an analytic ballistic particle with gravity + linear air drag (k 0.15 /s); peak-hold = the highest droplet apex so far.
- Belly flop: the whole flat body hits at once; a wide sheet from the body length at 25-62 deg, 0.35-0.78 v, plus a low middle spray. Peak 1.44 m.
- Cannonball: a small crown (62-84 deg, 0.22-0.50 v, ~0.7 m); the air pocket pinches shut 0.34 s after entry (deep seal), and its collapse fires a narrow Worthington jet (tip 9 m/s, then slower), peak 3.80 m. Lead change real 0.54 s after entry.
- Slow-mo schedule: real speed in the air, x10 from impact, easing to x7 for the jet's rise; the jet's apex is pinned to the music cadence; real speed again after it.

## Sound
- **Piece:** J. S. Bach, Italian Concerto BWV 971, I. (no tempo marking / Allegro) (1735; d. 1750, PD). Not on any used/banned list; not kid-coded.
- **Source:** Mutopia Project (Mutopia-2012/02/05-1826, edition CC BY-SA 3.0; only the PD notes are used), `<SOUNDFONTS_DIR>\scores\bach_italian_concerto\piano.mid`; read at runtime.
- **Excerpt:** 2/4, bars 1-13, quarter = 142.7 (tempo set so the bar-14 C major cadence lands on the jet's peak, 10.94 s).
- **Arrangement:** piano (score), violin on the top line, flute 8va very soft, cello + pizzicato on the bar bass; cadence = timpani C, strings, harp sweep, piano chord, celesta, held strings.
- **SFX (tonal):** the SLAP (a short bright tonal crack over a body thump), Mochi's deep entry bloop and the pocket-collapse gloop, a tick per 0.1 m of each splash height (rising pitch, a ding every metre), droplet "plips" for a sample of droplets landing back (lane pitch), bubble bloops, banner dings, Bolt's two sad bloops when he surfaces red.
- Mastering: `level_bed` (+3 dB crescendo, findb 2.0) → `master_keep_lift` (-14 LUFS, -2 dBFS); last 0.5 s zeroed.

## Checks (v1 encoded, Full HD)
- h264 yuv420p 1080x1920 @ 60 fps, 866 frames = 14.43 s. -14.00 LUFS, peak -2.16 dBFS (measured on the muxed mp4), last 0.5 s -240 dBFS.
- RMS/s: -18.1 -18.1 -17.2 -18.1 -17.1 -16.5 -16.5 -16.6 -16.0 -15.4 -15.7 -13.6 (cadence) -25.1 -33.6.
- SFX events/s: 5 9 5 16 24 33 30 24 23 22 15 30 10 0.
- flash_check PASS (0). Seam mean |delta| 2.24 (grey), against 1.89 between frames 0 and 1: the divers fall at real speed at the seam, so a one-frame step is that large; the dissolve lands exactly on frame 0.
- Frames read from the mp4: 0.5, 3.9, 5.85, 11.0, 13.2 + a 1:1 crop of the jet / sheet at the lead change (5.85 s).

## Doubts
- The splash numbers come from a tuned particle model (emission angles/speeds per entry type), not CFD; the ranking (cannonball jet > belly-flop sheet) and the cause (cavity collapse → Worthington jet) are the real physics.
- 10 s of the clip are slow motion; the climbing height ticks and banners carry it.
- Event rate is lowest in the first 3 s (5-16/s) while the sheet is up and the pocket forms.

## Args and cost
- `--seed` (5), `--sfx`, `--findb`; `--still --frame a,b`, `--audition`, `--report`, `--reuse`, `--nocap`, `--label`.
- Sim ~2 s; Full HD render ~75 s at 2 encoder threads.

## Outcome
- (fill after upload)
