# galton_board: GALTON BOARD, 1,380 marbles build a bell curve, Hungarian Dance No. 5 on piano

- Rule: every marble makes 12 fair left/right bounces (one per peg row). The binomial piles become a bell curve. A gold Gaussian outline (normal limit, sigma = sqrt(12/4) bins, scaled to the count landed so far) fades in over the bins (landed 110 -> 530).
- Board: 12-row triangular peg lattice (78 pegs, pitch 72 px, rows 50 px apart, top peg y 470), 13 bins (dividers 1070 -> floor 1395), glass funnel on top. Width 936/1080.
- Bounce: a faithful 50/50 random walk on smooth ballistic arcs. One hop = one eighth note (0.227 s), g 4417 px/s^2, apex ~9 px above each peg contact. In the bins the marbles settle into hex-packed slots (8/7 per row, r 4), in arrival order.
- Escalation, continuous, never restarted:
  - Bars 1-8: one marble per melody note (25). Each marble's first bounce lands ON its note.
  - From bar 9 the drop rate grows exponentially, 3.5/s -> ~670/s (k 0.488): single file -> stream -> flood. While the rate is below one per 16th, the first bounces are snapped to the 16th grid.
  - The last release is calibrated so the LAST marble lands on the final tonic (21.15 s vs cadence 21.16 s).
- Look: dark indigo stage, glowing violet pegs/dividers. Jewel colours by drop order (emerald -> cyan -> sapphire -> amethyst -> ruby -> amber), so the piles grow in rainbow strata. Luminous trails: 10 sub-samples x 11 ms on the flying marbles, thinned in the flood. Pegs flash in the colour of the marble that hit them. Float light buffer, one bincount splat per frame, 2-level bloom, hue-preserving tone-map.
- Story (seed 468, from a 800-seed search): Mochi bet on bin 4 (coral floor), Bolt on the middle bin 6 (mint floor). Small live counts float above the two piles.
  - Lucky start: Mochi's bin leads from 4.96 s (8 vs 3 at 12 s). Mochi hops.
  - The middle takes the lead for good at 14.04 s (landing #54). Bolt hops; Mochi looks worried.
  - Flood: both "wow". Final: 312 vs 178. Bolt cheers, Mochi gives the camera an annoyed stare, then both smile.
  - Final bins: 0 6 22 59 178 275 312 258 171 66 28 5 0.
- Loop: the cadence chord rings ~1.5 s over the finished curve. Then the bin floors split and slide open (T_DRAIN = cadence + 1.55 s), the piles fall through and the counter counts down to 0. The floors close, and marble 0 (spawned at -0.067 s) is already falling = frame 0.
- HUD: caption "1,380 marbles, 50/50 at every peg | ~Watch a BELL CURVE appear~"; counter "MARBLES: N" (= landed) at 0.782h.

## Music
- **Piece:** Johannes Brahms, Hungarian Dance No. 5 (published 1869; Brahms d. 1897). Public domain worldwide. Played by our own `audio.synth_piano`; no recording.
- **Key and tempo:** original key F# minor, 2/4, Allegro quarter = 132. Gentle ritardando (up to +20%) through the last bar only. No accelerando.
- **Form (24 bars):** bars 1-16 (the theme, up to C#6, the sixteenth-note run, home) + bars 25-32 (the arpeggio lead-in and the high reprise), ending on the tonic F#5.
- **Melody:** checked note-for-note against the flutetunes.com reference MIDI (brahms-hungarian-dance-no5.mid, F# minor, 2/4, 136 bpm). Certain. The one change: bar 16's F#4 is held 1.5 beats; its pickup F#5 is dropped, because we go straight to bar 25.
- **Left hand (our arrangement):** oom-pah. Root octave on beat 1, fifth on beat 2, a staccato chord on each off-beat. Harmony:
  - Bars 1-8: F#m F#m C#7 F#m Bm F#m C#7 F#m.
  - Bars 9-16 (and 25-32): F#m F#m E7 A | Bm-A | Bm-F#m | C#7 F#m.
  - Final: a rolled F#m chord, held 1.45 s.
- **Energy:** octave doubling under the melody from bar 9 (notes >= C#5). Phrase dynamics 0.86 / 0.95 / 1.04. Beat accents.
- **Ticks:** very soft glass ticks under the music when marbles land (gain 0.05 vs melody ~0.42). Thinned to <= 16/s and quieter in the flood. All in the bed; events carry note_gain 0.
- **Tail:** everything is faded out by T - 1.35 s (silent seam).

## Clip and checks
- Clip: 24.32 s (1459 frames). Cadence at 21.16 s, drain at 22.71 s. Full HD render ~20 min (with 5 other renders running in parallel).
- Checks on the encoded Full HD file:

| Check | Result |
|---|---|
| Format | h264 yuv420p 1080x1920, 60 fps |
| Loudness | -14.01 LUFS, peak -6.21 dBFS |
| Silence | last 0.5 s peak -90.3 dBFS (all audio faded by T - 1.35 s) |
| Seam | encoded mean delta 0.217 (good band) |
| flash_check | 0 flashes = PASS |
| Notes | 354 piano notes, 35 distinct pitches, ~80-99 per 5 s |

- Encoded frames read at 0, 0.5, 1.5, 12, 18, 19 (1:1), 20.2, 21.3 (1:1) and 23.1 s. Marble 0 is falling at frame 0; first bounce at 0.16 s on the first note.
- Delivered: <VIDEOS_DIR>\batch22\galton_board.mp4 (Full HD). Owner review: pending.

## Args
- --seed (468), --label, --cap, --still --frame, --report, --search N.
- Built 2026-10-09; the music was switched from Canon in D to Hungarian Dance No. 5 mid-build (owner: Canon/slow pieces "too slow / boring").
- Owner review (2026-10-09): ABANDON this idea.
