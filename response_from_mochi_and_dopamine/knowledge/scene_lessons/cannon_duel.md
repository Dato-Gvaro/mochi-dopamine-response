# cannon_duel: Broadside vs Mortar, age of sail (batch30)

- **Format (choice duel):** two lanes, one sea, one world (wooden ships, canvas, rope, iron shot, powder smoke, gulls, a palm island and a stone fort on the horizon). First to SINK its derelict target wins. No one is hurt; only hulks are hit.
  - **MOCHI (coral) chose a BROADSIDE:** a frigate firing 6-gun volleys, near-flat (E0 = 4.8 deg) and rippled bow to stern. Fast, many small holes.
  - **BOLT (mint) chose a MORTAR:** a bomb ketch (masts aft, mortar on the foredeck) with one mortar fixed at 45 deg. One shell per 2 bars.
- **Why Bolt wins (shown live):**
  - The bottom HUD shows ACCURACY 52% vs 80% and DAMAGE PER HIT 0.9% vs 25%. Each lane shows its own ROLL readout.
  - The broadside guns aim WITH the hull, so the roll tilts every flat shot: bow up sends it high through the sails, bow down sends it into the sea.
  - At 45 deg, dR/dtheta = 0, so the ship's roll barely moves the shell's landing point. The mortar's problem is RANGE, which it fixes with the powder charge.
- **Physics:**
  - Gravity plus quadratic air drag on every ball and shell, integrated at dt = 1/240.
  - g is calibrated so a ranged 45-deg shell flies 4 beats (g = 344 px/s^2). The same g drives the wave dispersion and the splinters.
  - Sea: a sum of 4 sines per lane, plus a ROGUE swell (a 30 px Gaussian hump moving at 300 px/s through Mochi's lane, with a white crest).
  - Each ship's pitch and heave are damped oscillators driven by the wave slope and height under its keel.
  - Hit tests run against the target hull and sails in the target's own rocking, sinking, listing frame. Balls are simulated in one causal time loop, so damage so far sinks the target before the next ball arrives.
- **Damage model:**
  - Damage = C x (impact speed / reference speed)^2. Broadside C_B = 0.019 per ball; mortar C_M = 0.268 per shell, referenced to the impact speed of a ranged shell.
  - Masts fall: Mochi's target at 50% and 80% damage; Bolt's target on shell hits 2 and 3. Shell hit 4 SNAPS the keel and the halves sink in a V.
  - A ball landing after the final hit scores 0 (the race is decided).
- **The mortar gunner:** shell 1 uses the vacuum rule v0 = sqrt(gD) and falls SHORT by ~160 px because of drag. The banner reads "TOO SHORT! +POWDER". Each next charge is scaled by (aim/landing)^0.7, since range goes roughly as v^1.4 with drag. Shells 2-5 then plunge through the deck.
- **Seed search:** the race below is `simulate(22)` (rogue offset +0.5 s, C_B = 0.013), chosen from 120 sea seeds x 4 rogue timings x 3 gun constants. Criteria:
  - shell 1 misses and shells 2-5 hit;
  - the rogue volley loses all 6 balls;
  - Mochi leads early, Bolt takes the lead on hit 4, Mochi retakes in the last bars;
  - Mochi finishes at 90-97%.
- **Measured story** (bar = 1.4286 s, bar 1 at 0.60 s):

| time | event |
|---|---|
| 2.51 s | shell 1 splashes short |
| 6.77 s | shell 2: PLUNGING HIT -24% (Mochi 47%) |
| ~9.9 s | the ROGUE WAVE swamps a whole volley (bar 7) |
| 11.06 s | shell 3: MAST DOWN, Bolt 50% vs Mochi 56% |
| 15.80 s | shell 4: MAST DOWN, BOLT TAKES THE LEAD (79% vs 57%) |
| 19.22 s | MOCHI RETAKES THE LEAD on the last bars' rapid volleys |
| 19.84 s | shell 5, fired on the bar-13 downbeat, snaps the keel: SUNK, with Mochi's target at 7% LEFT |

  - Totals: broadside 198 balls, 103 hull hits (52%). Mortar 5 shells, 4 hits.
- **Hook:**
  - Frame 0 is the payoff: Bolt's target split in a V with splinters in the air, "MORTAR WINS!", and "SO CLOSE! 4% LEFT" above it.
  - A 0.45 s fast rewind (hermite, -1x at the seam), then the first volley and first mortar shell fire at 0.60 s.
  - Music at 0.0 s: an E-flat fff stroke with a boom, then a timpani roll into bar 1.
- **Loop:** after the final hit, the clip runs in slow motion at 0.4x through the sink, then a silent 0.55 s rewind to the frame-0 moment (T_FINAL + 0.5 s sim time). Exact payoff to payoff.
- **Banners:** popped at 1.12x -> 1.0x and full alpha from the first frame, 58-92 px. The final banners sit over the sea so they do not hide the wreck. The broadside shows ONE damage popup per volley (summed), because per-ball popups cluttered the frame.
- **Music:**
  - **History:** v1 used the 1812 Overture finale ("God Save the Tsar!"). The coordinator dropped it on 2026-10-12 because it is a politically loaded anthem.
  - **Piece:** Handel, *Water Music*, Suite No. 2 in D, HWV 349, "Alla Hornpipe" (1717; Handel died 1759). Public domain.
  - **Notes (parsed, never memory):** IMSLP #270469, "PMLP11283-Handel Water Music 11.mid", IMSLP label "12. Alla Hornpipe". MIDI by Pierre Gouin, Les Éditions Outremontaises 2013, CC BY-SA 4.0. Only the pitches and rhythms of the PD work are used.
    - The file is written in F, 3/2, as two keyboard tracks. Its middle section is in the relative minor, which fits the Alla Hornpipe's A-B-A.
    - Cached at `<SOUNDFONTS_DIR>\scores\handel_hornpipe\`. Bars 1-13 are cut into `scenes/cannon_duel_hornpipe.json`.
    - Played at -3 semitones, in D major, the suite's key. The melody (top voice) runs A3-A5.
  - **Arrangement (lib/orchestra):** at the file's own tempo: a 3/2 bar = 1.4286 s, which is exactly 8/3 of the old Q grid, so the mortar cycle is 3 bars.
    - Melody: strings and violin, with horns an octave down. The echo bars 11-13 are lifted an octave so the tutti stays full.
    - Trumpets on the long notes, folded to E5 or below. Violas on the inner voices.
    - Bass: contrabass + sub + cello, and tuba from bar 4.
    - Choir aahs on the harmony from bar 4. Timpani (D/A) on every volley.
  - **Sync:**
    - Broadside volleys sit on the melody's ACCENTS: each bar's downbeat plus its longest (syncopated) note, then every quarter-note melody onset in bars 12-13. That is 33 volleys, and the rate climbs at the end.
    - Mortar shells fire with a "boom" on the downbeats of bars 1/4/7/10/13. Impacts carry taiko + crash.
    - Bar 14 holds the dominant (A) over a timpani roll and cymbal swell, and the D major tonic lands on the final shell's impact.
    - The hook at 0.0 s is a D major fff stroke + boom, with a timpani roll into bar 1.
  - **Foley:** our own synthesis (cannon, mortar, wood crack, splash, blast).
- **Checks (Full HD, encoded):**
  - h264 yuv420p 1080x1920, 60 fps, 1424 frames = 23.73 s (v2, hornpipe).
  - Audio: -14.01 LUFS; peak -5.00 dBFS; last 0.5 s -78 dBFS.
  - flash_check: 0 flashes = PASS (mean lum 0.196). The muzzle flashes and shell bursts stay local.
  - Seam: the mean delta is 1.1 at 270 px. It sits between its neighbours (0.6-0.7 before; 2.0 and 8.4 after, as the hook rewind accelerates). check_clip's 1.325 is high only because the seam is mid-rewind, not a cut.
  - Encoded frames read: v1 at 0, 0.5, 1, 2, 3, 11.1, 15.9 and 20.2-20.7 s; v2 at 0, 1, 10.1 and 20.2 s.
- **Fixes made during the build:**
  - The ranging shell hit the bow, so shell drag was raised (K_M 0.0011) and the charge rule became drag-aware.
  - A ball landing after the decisive hit used to keep draining Mochi's hull bar.
  - Per-ball popups cluttered the frame; they are now one popup per volley.
  - "KEEL SNAPPED!" started semi-transparent because its fade was longer than its duration.
  - The final banners now sit over the sea so they do not hide the split wreck.
- **Delivered:** <VIDEOS_DIR>\batch30\cannon_duel.mp4 (Full HD). Owner (2026-10-12): "it's good" -> APPROVED. 4K ship render (label ship, 2160x3840, -14.01 LUFS, 0 flashes) -> <VIDEOS_DIR>\Schedule\2026-10-15\1_cannon_duel.mp4.
- Owner review (2026-10-12): good -> APPROVED, 4K (Oct 15 slot 1).
