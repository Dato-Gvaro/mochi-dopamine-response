# jar_versus4 — CHAINSAW vs JACKHAMMER: every ball splits into 3, first jar to OVERFLOW (batch71)

- Brief: docs/BRIEF_batch71.md §1. New file `scenes/jar_versus4.py` (from jar_versus3; v3 untouched).
- Changes: ONE colour family per jar (5 close shades, never by size); the press family's ×3 split, each piece 2/3 as wide (area ×4/3 per split; pieces placed touching at 0.77 r); NGEN 6 (42 → 3.7 px); 18 big balls (rows 4/3/4/3/4 → 18 kept); OPEN jars (rim y 380, round rim lips, spilled balls fall outside and are culled below the base; they can't cross into the other jar); MAX line y 470; impact split V_BREAK 2000 (650 cascaded to full in 2 s); ball-ball overlap corrections give at most CORR_V 350 px/s (newborn overlaps swell the pile instead of exploding it).
- Fill = VOLUME level: (ball area inside + the tool's bulk) / (width × PACK 0.82); OVERFLOW = level above MAX for 20 frames. The visual pile-top measures (3 % quantile, width profile) were fooled by thrown balls and wall jams.
- Engine: per-size contact search (cKDTree per generation), saw push + chain friction vectorised.
- Seed 1 result: lead changes SAW 3.6 s, JACKHAMMER 4.57 s; **BOLT (jackhammer) OVERFLOWS at 12.40 s**; Mochi's level 60-80 % (her saw throws balls out of the open jar: 2,594 spilled vs 260). Splits/s saw 11-450, hammer 15-294 (bursty, not monotone).
- Tuning notes: vbreak 1800 → 6.5 s, 1900 → 7.5 s, 2200 → 15.4 s (chaotic); MAX 450 → 15.0 s, 470 → 12.4 s (same run).
- Sound: jar_versus3's (Figaro overture, D-major downbeat on the overflow; split clicks; hammer knocks).
- Checks (encoded Full HD, label b71): h264 yuv420p 1080x1920 60 fps, 936 f = 15.60 s; −14.01 LUFS, peak −5.35, last 0.5 s −67 dB; flash PASS; seam 0.59. Frames read 0.3, 3.7, 7.0, 12.38, 12.6, 13.5, 15.2.
- Doubts: Mochi's coral pile jams in a slab up the left wall (looks as high as Bolt's at the overflow, though its volume is lower); balls fly over the caption; split rate not climbing.
- Delivered review/batch71/jar_versus4.mp4. Owner review: pending.

## v2 (batch71b, owner: "balls and jackhammer are the same colour")
- Tools recoloured with colours no ball family uses: steel bar/bit, charcoal, hazard yellow with black stripes, 4 px ink outline + a white halo; both drawn ON TOP of the balls (were drawn before Bolt's balls). The sim is bit-identical (same cached pickle, 969 sound events). Edited in place (v1 never shipped; archived).
- Checks (label b71bv2): 936 f = 15.60 s; −14.01 LUFS, peak −5.35; flash PASS; seam 0.62. 1:1 crops at 5.0, 9.0, 12.4 s out of the encoded file: both tools read at a glance on both piles.
