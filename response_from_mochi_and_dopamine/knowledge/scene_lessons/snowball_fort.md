# snowball_fort — One GIANT snowball or 100 small ones: whose fort falls FIRST? (batch52, 2026-10-27)

- Brief: docs/BRIEF_batch52.md ("snowball_fort") + BRIEF_batch50/51 lessons. New scene file; lib/ and tools/ untouched. Style reused from ice_crack_race (winter palette, pines, HUD, banners, sound/mastering chain), sandcastle_wave (cell-grid destructible structure, debris, piles).
- Deliverable: `<VIDEOS_DIR>\MochiAndBolt\review\batch52\snowball_fort.mp4` (**v1**, Full HD 9:16, 14.47 s, 868 frames; output label v1).
- Caption (baked; `--nocap` gives the base): "One ~GIANT~ snowball or 100 small ones:" / "whose fort falls ~FIRST~?"
- **Story (honest sim):** Bolt's small balls take Mochi's fort 93% → 4%. He leads the whole race. Her 3 m ball rolls down the slope and lands on the cadence. It goes through his whole wall (100% → 0% in 0.4 s) and buries him to the eyes. **Mochi wins with 4% of her fort left.**

## Layout (one side view, 40 px = 1 m)
- **Field** at y 1180: Mochi's fort (x 128–240) and Bolt's fort (x 700–812). Each is a 112 × 140 px snow-block wall (28 × 35 cells of 4 px, 3 merlons, a leaning face).
- **Flags:** Mochi's is planted behind her fort (x 118). Bolt's is planted between his wall and him (x 818).
- **Bolt** stands at x 862 (right edge 900 ≤ 0.84w).
- **The hill:** Mochi's ridge at y 700 (x 0–472), a 80° snow slope with a 100 px fillet down to the field just in front of Bolt's wall.
- **On the ridge:** a "WET SNOW 100 cm DEEP" powder band ahead of the ball and the scraped trail behind it.
- **Readouts:**
  - the ball's diameter over it (gold at 3.0 m);
  - "×N" over Bolt;
  - a "% FORT LEFT" box + bar under each fort (from frame 0);
  - HUD (y 1366–1544): "WHOSE FORT FALLS FIRST?" → "BOLT'S FORT FELL FIRST!"; ball size / ×N; rules; LEADING → WINNER / FLATTENED.
- Static camera; dusk blues, snow whites, the characters' coral/mint accents only. No white flash (mean luminance 0.19).

## The physics
- **Bolt's snowballs:** each is a true parabola (g 1400 px/s², 1.0 s ± 4% to his aim). He aims at the centroid of what is left of her wall, with a 16 px scatter.
  - The first wall cell it touches gets a crater of radius 10 px.
  - Any part with no path down to the base falls.
  - Chunks fly ballistically, then land in a pile (angle of repose).
  - As her fort shrinks, more balls miss and puff into the snow (15 of 104).
- **Impacts on the music grid:** 1 per beat (bars 1–4), 2 per beat (bars 5–9), 3 per beat (bar 10 on). He stops throwing 0.35 s before the hit (he sees it coming); balls already in the air still land.
- **Mochi's ball:** a ball rolling through snow of depth h picks up its layer: 4πr² dr = h·2r ds → r² = r0² + (h/π)s.
  - It grows 0.5 → 3.0 m over 7.0 m of ridge in 0.98 m of snow (the snow depth is derived so it is exactly 3 m at the edge).
  - Her effort is steady (a shove on every beat), so speed ~ 1/r: 1.1 m at 0.5 s, 1.7 m at 2 s, 2.5 m at 6 s, 2.9 m at 9.3 s, 3.0 m at the edge at 10.65 s.
- **Down the slope:** a final shove (140 px/s), then rolling energy (5/7 g) along the resting-centre path, 1.11 s, arriving at 990 px/s just as it meets Bolt's wall on the cadence.
- **Through the wall:**
  - Every cell the ball sweeps costs E_C = 1.55e8 (px units, m = r³).
  - The 3 m ball sweeps 810 cells; the 80 cells above its path fall. It keeps 15% of its energy and stops against Bolt (x 842), then slumps into a mound over him.
  - **Counterfactual (`--report`):** a 2.7 m ball has 697 cells' worth and would stop inside the wall; a 2.4 m one, 489. The size mattered.
- Parameters were searched (scratch script) over crater radius 7–11 px, scatter 12/16 px and 40 seeds for a close race. rc 10, seed 5 gives a gradual collapse with her fort at 3.9% on the cadence and no further loss. Other seeds at rc 10–10.5 also land at 2–8%, so the close finish is not a knife-edge.

## Timeline (clip s)
- **0.0:** mid-fight. Mochi's fort is 93%, ×13 thrown, 3 balls in the air. A hit at 0.0, then one every 0.28 s. Mochi is pushing a 0.5 m ball.
- **0.5 / 1 / 2 s:** ball 1.1 / 1.4 / 1.7 m; her fort 92 / 90 / 86%; ×15 / 16 / 20. Bolt laughs at 0.55 s.
- **3.36 s:** "2 PER BEAT!".
- **6 s:** ball 2.5 m; her fort 68%.
- **7.56 s:** "3 PER BEAT!".
- **8–10 s:** big top-of-wall collapses (54% → 13%). Mochi looks worried at 60 / 30 / 15%.
- **10.65 s:** the ball is 3.0 m at the edge ("3 m!"); her fort is at 8%. It tips over, and Bolt goes wow, then worried.
- **11.76 s (cadence, bar 15 downbeat, A major):** contact. The wall goes 100 → 82 → 12 → 0%.
  - Bolt's flag snaps at ~11.9 s.
  - **Lead change / FLAT at 12.16 s** (Bolt 0% vs Mochi 3.9%): "FLATTENED!", "MOCHI WINS!", her cheer + gold stars.
  - The mound buries Bolt to the eyes (annoyed). Mochi laughs, then looks smug.
- **13.86–14.46 s:** dissolve into frame 0.

## Sound (music first)
- **Piece:** Emile Waldteufel, *Les Patineurs* (The Skaters' Waltz), Op. 183 (1882; Waldteufel d. 1915, PD). The famous Waltz No. 1 theme: wintry, a skating rink classic, not a carol, not kid-coded. Not on any used list.
- **Source:** IMSLP orchestral parts mirrored on the Internet Archive (`imslp-patineurs-op183-waldteufel-emile`), saved with `SOURCE.txt` at `<SOUNDFONTS_DIR>\scores\waldteufel_patineurs\`. The melody was hand-read from the 1st violin part (sul G); note heads were located by script against the staff lines. The harmony comes from the bass part (A2 C#3 B2 E3 … F#3 … B2 … E3 … A).
- **Excerpt:** A major, 3/4, dotted half = 71 (bar 0.84 s), one steady tempo. Bars 1–14 of the theme, then the bar-15 A cadence is the hit.
- **Arrangement** (lib/orchestra):
  - violins on the tune an octave up, cellos at pitch;
  - celesta two octaves up (winter sparkle), flute from bar 9;
  - oom-pah-pah (contrabass + pizz bass on 1, pizz chords on 2–3, soft horns on 2–3 from bar 9), string pad from bar 5;
  - timpani on bars 13–14 + a roll into the hit;
  - the cadence: timpani A + bass drum boom, A-major tutti (strings, brass, horns, violins, flute, contrabass), harp sweep, celesta.
- **SFX** (all tonal; energy above 4 kHz 1.4% of the mix):
  - each snowball hit: a soft tonal thud + 1–3 crunch ticks;
  - a miss: a soft "puff" (a short downward tone);
  - landing chunks: ticks gathered on a 16th grid;
  - Mochi's shove each beat: a snow "tok" + a tick that grows with the ball;
  - the ball rolling down: a tick every 18 px climbing the E7 chord (accelerating) + a 3-tone swell;
  - the hit: a huge thump on A1 + A2 and an 8-tick cascade down A major;
  - the mound puff, Bolt's muffled "mmf", the win chime.
- **Mastering:** `level_bed` (+3 dB crescendo, `--findb 2.0`) → `master_keep_lift` (−14 LUFS, 5 ms lookahead at −2 dBFS); last 0.5 s zeroed.

## Checks (v1 encoded, Full HD)
- h264 yuv420p 1080x1920 @ 60 fps, 868 frames = 14.47 s.
- −14.01 LUFS, peak −2.00 dBFS, last 0.5 s digital silence.
- RMS/s: −19.4 −19.0 −18.0 −18.2 −17.8 −17.7 −17.8 −16.5 −16.9 −16.8 −16.5 −15.1 −14.2 (cadence) −18.8 (hold).
- SFX events/s: 26 22 27 33 37 36 40 45 51 45 49 54 23 (cadence second) 0.
- Bolt impacts/s: 4 4 3 6 7 7 7 9 11 11 10 11 5.
- Mochi fort %/s: 93 90 86 83 79 73 68 60 54 22 13 5.5 3.9 3.9.
- flash_check PASS (0 flashes, mean luminance 0.19). check_clip seam 0.469 (good band).
- Frames read from the mp4: 0.5, 1, 2, 6, 9.3, 10.75, 10.8, 11.5, 11.8, 11.95, 12.2, 12.8, 13.0, 13.6. 1:1 crops of the fort crater (6 s), the hit (11.95 s), the burial (13.0 s) and the edge (10.75 s).

## Doubts
- Characters and forts are smallish (forts 112 × 140 px, CR 38). The whole fight has to fit x 0.10–0.84w with a hill tall enough for the ball's run. The sky above the ridge (y 260–580) is calm: moon, stars, snowfall.
- Bolt leads all the way; the only lead change is the final hit (12.16 s, 0.4 s after the cadence contact). The tension is "will her fort last until the ball lands?", not a back-and-forth.
- The title promises a giant ball, so a viewer can guess the ball is the threat. The uncertainty is the race (her fort is at 8% when it tips over the edge, 4% at the end). The answer to "is the outcome obvious from frame 0?" is **partly**: the giant ball's threat is guessable; who survives is not.
- **Cartoon cheats:**
  - 1 m of wet snow on the ridge (derived so the ball is exactly 3 m at the edge);
  - the 80° snow slope;
  - she can push a 3 m (~5 t) snowball;
  - Bolt pops up to eye level in the mound.
- Bolt's balls land behind the hill face in 2D; they are drawn in front of the hill (depth), never touching Mochi.
- ×N ends at ×104 (caption says "100 small ones").

## Args and cost
- Physics: `--g --tf --rc --sig --seed --r0 --rf --ec --v0 --stop`. Sound: `--sfx --findb`. Also `--still --frame a,b`, `--audition`, `--report`, `--reuse`, `--nocap`, `--label`.
- Sim ~2 s; Full HD render ~2.5 min at 2 encoder threads.
- Owner review: pending.

## Outcome
- (fill after upload)

## Shipped (4K, 2026-10-28, batch53)
- Owner: "might work" → 4K ship. `NF_SCALE=2.0 python scenes/snowball_fort.py --label ship` (defaults, seed 5; ~2 min at 2 encoder threads, rc-lookahead 12).
- Encoded: h264 yuv420p 2160x3840 @ 60 fps, 868 frames = 14.47 s. −14.01 LUFS, peak −2.00 dBFS, last 0.5 s silent. flash_check PASS (0 flashes, mean lum 0.189). Seam mean |Δ| 0.317. Sim identical to v1 (fort 3.9% at the cadence, 104 throws).
- Frames read from the 4K mp4: 0.5 s, 12.6 s + a 1:1 crop of Bolt buried.
- Staged: `<VIDEOS_DIR>\MochiAndBolt\schedule\2026-11-03\2_snowball_fort.mp4` (16:00 local Nov 4 = 07:00 US East Nov 4). FHD review copy → `MochiAndBolt\archive\snowball_fort_fhd.mp4`.
