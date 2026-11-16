# ice_crack_race — Tiptoe or SPRINT across thin ice: who reaches the shore? (batch52, 2026-10-27)

- Brief: docs/BRIEF_batch52.md ("ice_crack_race") + BRIEF_batch50/51 lessons. New scene file; lib/ and tools/ untouched. Style reused from sandcastle_wave (stacked lanes, divider strip, HUD, banners, caption) and rocket_stage (sound/mastering chain).
- Deliverable: `<VIDEOS_DIR>\MochiAndBolt\review\batch52\ice_crack_race.mp4` (**v2**, Full HD 9:16, 18.27 s, 1096 frames; output label v2). v1 (16.27 s, 976 frames) archived as `MochiAndBolt\archive\ice_crack_race_v1.mp4`.
- Caption (baked; `--nocap` gives the base): "Tiptoe or ~SPRINT~ across thin ice:" / "who reaches the ~SHORE~?"
- **Twist:** the sprinter leads all race (up to 11 m), but his own cracks + the thinning spring ice catch up with him 5.1 m from the shore. Mochi wins (honest sim; Bolt's ice holds 4 times first, so the fall is not a given).

## batch55 (2026-10-28): rings on BOTH poles → 4K ship
- Owner on v2: "the rescue ring sitting only on Mochi's end looks bad: put a second one at Bolt's finish too, or remove it". Fix: `draw_flag` hangs a ring on BOTH finish poles from frame 0 (symmetric shore safety rings); Mochi's leaves her pole at T_PICK and is thrown, Bolt's stays put all clip. Nothing else changed (sim, timing, sound identical).
- Shipped 4K (`--label ship`): h264 High yuv420p 2160x3840 @ 60 fps, 1096 frames = 18.27 s; −14.00 LUFS, peak −1.99 dBFS, last 0.5 s silent (−240 dBFS); flash_check PASS (0 flashes, mean lum 0.10); seam mean |Δ| 0.765. Encoded frames read at 15.35 (ring in flight, Mochi's pole empty, Bolt's ring on his pole) and 16.6.
- Rings sit at x 884–964 (0.82–0.89w), the shore decoration zone as in v2 (Bolt's spare is decoration; Mochi's throw starts inside the safe zone).
- Staged: `MochiAndBolt\schedule\2026-11-03\3_ice_crack_race.mp4`, 00:00 local Nov 5 (= 15:00 US East Nov 4). The v2 FHD review copy → `MochiAndBolt\archive\ice_crack_race_fhd.mp4`.

## v2 (2026-10-28): the rescue
- Owner on v1: "good, but Bolt is freezing at the end… not the rope thing again: maybe throw the floating ring" (BRIEF_batch53).
- Unchanged: the race, sim (seed 165; break 10.71 s at 54.9 m; lead change 11.77 s; 1000 / 1158 crack segments), the music up to the cadence, "MOCHI WINS!", "5.1 m SHORT!", the HUD. HOLD 2.1 → 4.1 s (+2.0 s).
- A red-and-white ring buoy (4 red bands, NO rope) hangs on Mochi's flag pole from frame 0 (x 924, decoration zone), so the rescue is set up rather than conjured.
- Beats (clip s; all on the 6/8 beat grid after the cadence 13.57):
  - 14.52: she hops 18 px to the pole and lifts the ring over her head. Her name tags fade out while she holds it.
  - 14.80–15.00: wind-up (leans back 0.20 rad, squash). **15.00 (cadence + 2 beats): the throw**, with a lean forward and an open mouth. Sound: a soft tonal slide-whistle glide D5→D6, then down to A4 during the flight.
  - 15.00–15.71: one-beat arc on the global layer (it crosses the divider), 1.25 spins, tipping flat (0.40 squash) in the last 45%.
  - **15.71 (cadence + 3 beats): it lands 70 px left of Bolt with a splash** (22 droplets, ripples; tonal thud, big bloop, 5 droplet bloops).
  - 15.81–16.03: a "wow" face; he paddles 18 px into it while it drifts to him. He then floats higher (sink 0.55 → 0.22 r), bobbing with the ring: its back half is drawn behind him, its front half over him.
  - 16.13: the 3rd "brr.", with harder shivering and a teeth-chatter face (worried, wobbly mouth).
  - **16.43 (cadence + 4 beats): thumbs-up.**
    - A mint mitten hand pops up beside the ring; Bolt has a relieved happy face and Mochi smiles (^ ^).
    - Sound: two soft dings, then the march's own pp staccato ending "DUM – DUM" in D major (pizz + contrabass + bassoon) at 16.43 and 17.14.
  - 17.67–18.27: dissolve into frame 0 (the ring is back on the pole).
- Mochi's late "laugh" (cadence + 1.05) was dropped, since she helps him instead. Bolt's "annoyed" ends at the ring splash.
- **v2 checks (encoded Full HD):**
  - h264 yuv420p 1080x1920 @ 60 fps, 1096 frames = 18.27 s.
  - −14.00 LUFS, peak −1.99 dBFS, last 0.5 s silent.
  - flash_check PASS (0 flashes, mean lum 0.10). Seam mean |Δ| 0.916 (v1 0.905; the same thin-crack coding noise).
  - RMS/s: … −13.9 (cadence) −14.7 (throw/splash) −18.1 (thumbs-up + DUM-DUM) −23.9 (decay), then silence. SFX events/s in the rescue: 2 / 7 / 6.
  - Frames read from the mp4: 0.5, 14.70, 14.95, 15.35, 15.76, 16.20, 16.60, 17.95. Stills: 0, 14.52-17.97 (11 frames), plus a 1:1 crop of Bolt in the ring with the thumbs-up.
- **v2 doubts:**
  - The ring flies "down the screen" from her lane into his (the lanes are side by side on one lake).
  - The ring is small on a phone once he's in it: its front half shows as a red-and-white band at his chin.
  - The event rate drops after the cadence (2-7 events/s): the rescue is a story beat, not a climb.

## Layout
- Two stacked lanes across one lake (1080 × 490 each): Mochi on top (y 290), Bolt below (y 850). The SHORE (snow bank, pines, gold flag) on the right from frame 0; the start line at x 112, the shore edge at x 860 = 60 m (12.5 px/m).
- Each lane: a 0-60 m ruler along the bottom (ticks every 5 m, labels 15/30/45 m), "ICE 15 cm · THINNER → · 8 cm" along the top, the ice darkens toward the shore (thinner = water shows through). A distance tag over each racer ("23.8 m").
- Divider strip: the live gap ("BOLT LEADS BY 7.8 m" → "BOLT FELL IN!" → "MOCHI LEADS BY 4.1 m" → "MOCHI MADE IT!") + a "CRACKS SPLIT ×2 EVERY STEP" pill.
- HUD (y 1366–1544): "FIRST TO THE SHORE (60 m) WINS"; per side name, m TO GO, a progress bar, the rule ("TIPTOE · SMALL STEPS" / "SPRINT · BIG LEAPS"), LEADING / SPLASH! / WINNER / IN THE LAKE pill.
- Key content inside x 0.10–0.84w; only the snow bank, pines and the flag go wider. Static camera. Calm ice blues, cracks as thin pale-cyan lines with a faint glow, dark-teal water; no white flash.

## The physics (simulated, seeded, not scripted)
- **Runners.** Mochi: a 0.76 m step on every eighth note (3.2 m/s), impact 0.6. Bolt: one leap per beat landing ON the beat, 2.4 m growing +0.25 m per leap to 3.6 m (≈5 m/s); landing impact 3.0 × (leap / 3 m)².
- **Cracks.** Each impact starts a star (Mochi 3 rays, Bolt 6) with ray length 6.76 px × stress. On each of the owner's next steps every tip splits in TWO (±0.32–0.62 rad), each child 0.62× its parent (Mochi 2 generations, Bolt 4, the break 5). A branch that crosses an older crack joins it and stops; cracks stay on the lane's ice. Bolt ≈ 1160 segments, Mochi ≈ 1000.
- **The ice.** Thickness 15 cm → 8 cm toward the shore (h^1.5 profile), strength = (h / 15 cm)² (a plate's bearing capacity). Stress = impact × (1 + 0.008 × crack length already within 30 px of the foot) / strength. Stress > 10.5: the ice sags and floods but holds (teal flood patch, "IT HOLDS!"), Bolt freezes for a beat and restarts at 2.4 m. Stress > 13.5: it gives way.
- Parameters were searched (scratch scripts) so that the honest sim breaks on the music's forte; seed 165 does it over a range of thresholds (S_SAG 10.05–11.1 all give the same story), i.e. the result is not knife-edge. Mochi's stress peaks at 6.1, well under 10.5.
- The hole: wedges between the breaking landing's own six rays tip into the water and float at the rim; Bolt drops in (splash droplets, ripples), pops up to eye/mouth level, tries to climb out at +1.25 s and the rim chunk breaks off (+1.6 s), shivers, "brr." ×2.

## Timeline (clip s; clip = sim)
- **0.0 s:** mid-race. Mochi 17.3 m with a trail of tiny cracks, Bolt 21.7 m landing a fresh 6-ray star (forms within 0.1 s). BOLT LEADS BY 4.4 m.
- **0.5 / 1 / 2 s:** Mochi 18.8 / 20.4 / 23.6 m tiptoeing (a tick + crack every 0.24 s); Bolt mid-leap 23.8 m, lands 25.3 m and laughs ("HA HA", 0.8 s), lands 31.5 m (2.14 s) with a wide star; the gap 4.9 → 5.4 → 7.8 m.
- **3.57 s:** first sag at 39.7 m (lead 11.0 m): the ice floods, "IT HOLDS!", Bolt worried, freezes a beat.
- **6.43, 7.86, 9.29 s:** sags 2-4 (47.7, 50.1, 52.5 m); each costs him a beat. The gap shrinks 8.8 → 7.1 → 5.5 → 3.2 m.
- **10.71 s (bar 14 beat 2, the forte E-flat chord):** the landing at 54.9 m gives way: deep tonal crunch + splash, "SPLASH!", "BOLT FELL IN!". Mochi glances down (wow).
- **11.77 s:** lead change: Mochi passes his 54.9 m (ding pair, she laughs, then smug).
- **11.96 / 12.31 s:** Bolt's climb-out fails (the rim breaks off), "brr." (11.66, 12.96).
- **13.57 s (cadence, bar 16 beat 2, D major):** Mochi steps onto the snow: "MOCHI WINS!", gold stars, chime; "5.1 m SHORT!" over Bolt (soaked, annoyed, shivering). HUD WINNER vs IN THE LAKE.
- **15.67–16.27 s:** dissolve into the frame-0 state; the HUD/divider switch at the midpoint.

## Sound (music first)
- **Piece:** Charles Gounod, *Marche funèbre d'une marionnette* (Funeral March of a Marionette, 1872/79; Gounod d. 1893, PD) — the "Alfred Hitchcock Presents" tiptoe theme: suspenseful-playful, a perfect sneaking/tiptoe fit. Not on any used/banned list (jenga_pull wanted it but found no score). Not kid-coded.
- **Source:** two PD printed editions from the Internet Archive, saved with `SOURCE.txt` at `<SOUNDFONTS_DIR>\scores\gounod_marionette\`: Paris, H. Lemoine 1882 (`marchefunbredune00goun`, Allegretto dotted quarter = 84) and St. Louis, Kunkel 1886 (`b10332613`, cross-check). The Cortège theme was hand-read (note heads located by script against the staff lines). Downloaded 2026-10-27.
- **Excerpt:** D minor 6/8, dotted quarter = 84 (bar 1.43 s), one steady tempo. Clip bars 1-4 = source bars 1-4 (the motif twice), clip bars 5-10 = source bars 11-16 (the held A over the motif, the rise, the forte E-flat in bar 14, the dim. bar 15, the cadence). The final tonic is voiced D **major** for the win (the source ends D minor, pp).
- **Arrangement** (lib/orchestra, MuseScore_General): bassoon on the motif (staccato; grace E4), clarinet an octave up from bar 3; oboe on the held A; violins + bassoon (8vb) on bars 13-15, flute from bar 14; pizzicato strings = the score's left hand (bass on beat 1, chord on beat 2) + the staccato "DUM" chords; soft string pad from bar 5; timpani steps into the forte; at the forte an E-flat brass/horn/strings stab + timpani (= the collapse); bar 16 an A chord with a timpani roll, then the D-major tutti (strings, brass, horns, violins, flute, contrabass, timpani, harp sweep).
- **SFX** (all tonal; energy above 4 kHz 0.19%):
  - Mochi's tiptoe: a tiny round tick on a chord tone each step; + 0–3 soft "stress pings" per step (one per 1.6 of ice stress) — the thinner the ice, the more it sings (this is what makes the event rate climb);
  - Bolt's landings: the lake-ice "pew" (a crisp tone falling onto a chord tone) + a tonal thump on the bass, level ∝ stress;
  - crack branches: a tiny falling chirp per 32nd-grid group of finished branches, per lane;
  - sag: a low tonal "boom" (flexing sheet) + a water bloop;
  - break: a deep tonal thump on E-flat + 4 falling pews + a big low bloop + 7 droplets on the 32nd grid;
  - climb-out: pew + bloop + 3 droplets; "brr.": two chord tones trading at 16 Hz; lead change: 2 dings; cadence: D-major arpeggio chime; snow steps: a soft pat.
- Mastering: `level_bed` (+3 dB crescendo, `--findb 2.0`), then `master_keep_lift` (−14 LUFS, 5 ms lookahead at −2 dBFS); last 0.5 s zeroed.

## Checks (v1 encoded, Full HD)
- h264 yuv420p 1080x1920 @ 60 fps, 976 frames = 16.27 s.
- −14.01 LUFS, peak −1.99 dBFS, last 0.5 s −84 dBFS.
- RMS/s: −18.8 −19.0 −18.1 −16.0 −19.0 −16.8 −16.0 −16.2 −17.4 −15.8 −15.3 −14.5 −16.9 −14.7 −14.0 (cadence/hold) −18.8, then the silent tail.
- SFX events/s: 15 14 18 17 14 19 20 19 15 17 28 28 24 13 (cadence second) 0 (hold).
- flash_check PASS (0 flashes, mean luminance 0.10).
- Seam: pre-encode last → first 0.46 vs adjacent frames 0.23–0.55 (continuous). Encoded check_clip 0.905 / my extraction 1.16: I/P-frame coding noise (each encoded frame differs ~1.65 from its own source PNG; the thin bright crack lines on dark ice are hard for yuv420p); adjacent encoded P-frames 0.2–0.6.
- Frames read from the mp4: 0.5, 1, 2, 9.3, 10.75, 11.0, 11.8, 13.0, 14.5; 1:1 crops of the break (10.78) and of Mochi's crack trail (2.0). Stills (pre-encode) at 0, 1, 2, 3.6, 7.5, 9.3, 10.8, 11.7, 12.3, 13.0, 13.6, 14.8, 16.25.

## Doubts
- Bolt freezes on 4 of the last 11 beats (each sag costs him a beat); that is what lets Mochi close the gap, but he spends a lot of the second half standing still and worried (always with a flood, a boom and "IT HOLDS!").
- The ice thinning toward the shore (15 → 8 cm) was added so the honest sim breaks late instead of at a random beat. It is shown (labels + darker ice) but small; the 1-second read is "big leaps = big cracks".
- Cartoon scale: a racer is ~6 m "tall" on the 60 m ruler; leaps of 3.6 m read as ~45 px hops.
- Mochi's cracks are tiny (a fine trail) — correct for the rule, but less spectacular than Bolt's.
- The Funeral March of a Marionette ends quietly in D minor; the D-major tutti cadence is an arrangement liberty. "Funeral" is in the piece's name only (never shown).
- Encoded seam metric 0.9–1.16 (see Checks), like rocket_stage's 0.909.
- Overlap check: batch32 `thin_ice` (Mochi runs vs Bolt slides on his belly, pressure gauges; Mochi breaks through) shares the "one falls through thin ice" payoff and a darker thin zone. Different mechanic (branching ×2 crack networks, a race to a shore, a sprinter who leads) and the other character falls, but a viewer of both may see a family resemblance.

## Args and cost
- Physics: `--lmin --lstep --lmax --eb --em --kappa --rad --ssag --sbrk --clen --q --seed --kb0 --h0 --h1`; sound `--sfx --findb`; `--still --frame a,b`, `--audition`, `--report`, `--reuse`, `--nocap`, `--label`.
- Sim < 1 s; Full HD render ~1 min at 2 encoder threads.
- Owner review: v1 fix (rescue) → v2; v2 fix (rings on both poles) → shipped 4K (batch55).

## Outcome
- (fill after upload)
