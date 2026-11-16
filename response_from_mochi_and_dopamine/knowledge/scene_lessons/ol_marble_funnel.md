# ol_marble_funnel (Dopamine.exe)
- New scene, character-free (docs/BRIEF_channel2.md, docs/BRIEF_overnight_1023.md). Skeleton: ×2 gates (each marble that rolls through a gate becomes 2) toward a named end state with a PHYSICAL payoff: the jar bursts. Concrete objects (glass marbles, a glass jar), vertical gravity (clearly not ol_spiral_maze's circular maze).
- Caption (baked, `--cap`; `--cap ''` = base): `Every marble through a gate becomes ^TWO^|until the jar ~BURSTS~` (`^x^` = newest-marble hue, unwrapped, capped at rose 0.95; `~x~` = gold).
- Delivered: `<VIDEOS_DIR>\DopamineExe\review\ol_marble_funnel.mp4` (**v2**, Full HD, seed 1, label fhd2, 17.80 s, 1068 frames). No 4K yet.
- v1 (superseded, 2026-10-23): same run, calm "fills to the brim" finale; growth only ×4.5 (286 → 1,300), sparse top ramps. Owner: "interesting but lacks something, needs more engagement" (physical payoff works, slow filling fails) → v2: ×52 growth, accelerating drops, per-gate counts, crack + burst + flood finale.

## World (logical 1080x1920, static camera)
- Zig-zag marble run: 4 ramps (slope 0.10, x 178-836; ramp 4 ends at x 592 over the jar neck), 3 banked semicircle U-bends (r 60, outer edge x 116 / 896); backstop + short dispenser tube top left (x 204). Thin white lines (3 px, 85 %).
- ×2 gates: a 3D hoop (ellipse 10 × 34) around each ramp at 40/42/40/48 % of its length: (441, 430), (560, 567), (441, 702), (719, 823). Back half behind the marbles, front half in front; glows in the outgoing hue on every pass. Above each: a "×2" pill (pops with the hits) + the running number of marbles out of that gate (2 per pass), e.g. 266 → 476 → 802 → 1,236 at 14 s.
- Jar: neck x 392-624 from y 900 (gold dashed line), shoulders 922-982, body x 263-753 to y 1236, 40 px corners. Faint glass fill, gloss streaks, outline white 85 % that warms toward gold through bar 12.
- Floor: one line y 1242 (drawn x 70-1010); invisible walls at the screen edges keep the flood in frame.
- Marbles: r 7, glossy (radial gradient lit top-left, specular dot). Hue = ordered sweep by DROP time, 0.55 + 0.024/s (cyan → blue → violet → magenta → red), −0.03 per gate passed; S 0.74, V 0.93. Jar bands cyan (bottom) → violet; no yellow/green; gold = the goal only.
- HUD: meter y 1300 ("JAR n %" = marbles delivered into the jar / the number delivered by the burst, monotone; gold BURST goal from frame 0); counter y 1488 total marbles + ×2 pill + "MARBLES" (gold from the burst); watermark "DOPAMINE.EXE" 35 %.

## Rule / physics
- Position-based dynamics, dt 1/60, 4 substeps × 3 Jacobi passes, cKDTree pairs, frictionless discs, segment walls, G 5000 px/s², speed cap 620 px/s, constraint velocity cap 320 px/s. Seeded, deterministic, simulated once, cached (`output/ol_marble_funnel_v2_*_sim.pkl`).
- Dispenser drops one marble per beat-grid note: 7 pre-roll drops every 1.5 beats (one lineage on every ramp at frame 0), quarters in bar 3, **eighths** from beat 12, **sixteenths** from beat 20 (bar 6), closes on the cadence. 112 drops.
- Every marble that rolls through gate k with generation k becomes 2 (twin one diameter above, pops in 0.12 s with a ring). Each drop reaches the jar as 16.
- Burst = the cadence frame: the jar walls leave the sim, packed marbles get an outward impulse (≤ 520 px/s by side and depth), the flood spreads wall to wall; floor damping drops from 0.985 to 0.997 per substep after it so the flood keeps flowing.
- Cracks: 6 seeded branching cracks grow (0.22 s each) on beats 44, 45, 46, 46.5, 47, 47.5 (bar 12). Shards: the outline resampled and cut into ~40 slivers (28-52 px, 4-9 px wide, pale glass fill 30 %, white edge), flung outward/up, fall (2600 px/s²), land, settle, fade 0.9-1.8 s after the burst.

## Timeline (clip s, seed 1)
- Frame 0 (bar 3 downbeat): 30 marbles on all 4 ramps (gate counts 12/16/16/…), jar empty; first gate pass in second 0 (27 passes).
- 0.5 s: 45. 1 s: 59 (first stream into the jar). 2 s: 88. 8 s: 505, jar 24 %, magenta on the run, the run full top to bottom.
- Marbles per second: 30, 59, 88, 124, 171, 227, 304, 399, 505, 629, 764, 916, 1,074, 1,236, 1,401, **1,563 (burst)**, 1,716, 1,860. **Growth ×52 to the burst, ×62 to the end.**
- Events per second (gate passes + jar landings + drops): 30, 59, 62, 74, 84, 122, 145, 174, 203, 245, 277, 311, 316, 321, 240 (jar full: landings dip), 351 (burst). Gate passes alone 27 → 157/s.
- ~14 s: the jar overflows its brim, marbles mound over the neck and spill down the sides, the stream backs up into ramp 4; cracks spread through bar 12 (14.25-14.81 s).
- **Burst 15.00 s** (bar 13 downbeat = the cadence): glass shards fly and settle, the packed marbles flood across the whole floor, 2 soft gold rings + gold glints, a short warm glow through the marbles; meter 100 %, counter gold. The run keeps pouring into the flood.
- Hold 2.2 s → 0.6 s dissolve into the pre-roll. **17.80 s, 1068 frames.** Last frame 29 marbles vs frame 0 30.

## Sound
- **Music played as music:** W. A. Mozart, Symphony No. 25 in G minor, K. 183, I. Allegro con brio (1773; Mozart d. 1791, PD). Source: Mutopia `MozartWA/KV183/Symphony25_1/Symphony25_1.mid` (Public Domain), saved at `<SOUNDFONTS_DIR>\scores\mozart_symphony25_mf\Symphony25_1.mid` + `SOURCE_mutopia.txt` (downloaded 2026-10-23). Not on the used/banned lists, not kid-coded, first use.
- Bars 3-12 (quarter beats 8-48) at a steady **160 bpm**; bar 12's half cadence on D held into the cadence; our G-major chord (Picardy third) on the bar-13 downbeat = the burst. Drops sit on the beat grid.
- Arrangement (lib/orchestra): violins I strings + violin + quiet piano 8vb, violins II, viola, cello + contrabass 8vb + quiet piano, oboes, horns; timpani Eb on frame 0, a soft timpani roll on D through bar 12. Burst: G-major chord on strings, horns, oboe, cello/contrabass, rolled harp, celesta, timpani G2 and a soft boom.
- SFX (×0.34): tonal glass tick per gate pass (chord tone of the score's harmony, C6-B6, ≤ 34/s); glass clack per marble landing (G-minor pentatonic, ≤ 30/s, gain ÷ √(rate/24)); wooden tock per drop (on the beat); a dry tonal tick per crack; at the burst a 0.6 s shower of 34 tonal glass tinks (G-major tones) and a tumbling clack texture for the flood (70/s decaying). No noise anywhere.
- `level_bed` (+3 dB crescendo, cadence +4.5 dB), `audio.master(peak_db=None, reverb=0.5)`, last 0.6 s digital silence.

## Checks (encoded Full HD v2)
- h264 yuv420p 1080x1920, 60 fps, 1068 frames, 17.80 s. **flash_check PASS** (0 flashes, mean lum 0.012).
- **−14.00 LUFS**, peak −7.90 dBFS, last 0.5 s digital silence, energy > 5 kHz 0.06 %. RMS per second: −19.3, −18.5, −19.0, −18.5, −18.2, −17.7, −17.4, −17.9, −17.2, −17.6, −17.3, −17.2, −17.9, −18.0, −17.2, −17.4 (burst), −18.7, −56.3.
- Seam (encoded mean |Δ| last → 0): 1.14; normal steps in the same file 0.48-3.93 (frames 1→2 = 1.01), so an ordinary step (check_clip's generic 1.1 line does not fit this motion level).
- Frames read from the mp4 at 0, 0.5, 1, 2, 8, 14.6, 15.0, 15.3, 16.5, 17.78 s; 1:1 crop of the cracked, overfull jar + gate labels at 14.6 s.

## Flags
`--seed (1) --label --cap --still --frame a,b --dry --audio --resim --sound 0 --sfx (0.34) --fin (2.0)`. Sim-changing (re-check that the brim is reached just before the cadence): `--npre (7) --prestep (1.5) --b8 (12) --b16 (20) --bpm (160) --vmax (620) --dvx (330) --bhw (245) --neck (900) --burstv (520) --hrate (0.024)`.

## Doubts
- Frame 0 has only 30 marbles (the price of ×50 growth): every ramp has a few, the jar is empty; the first stream reaches the jar at ~0.7 s.
- The jar is over the brim from ~14 s, so landings dip for ~1 s before the burst (gate passes and the counter keep climbing).
- The flood marbles near the screen edges sit outside the 0.10-0.84 w band (decoration only).
- Mozart 25 is G minor and dramatic; the G-major burst chord brightens the payoff. 17.8 s, top of the 13-18 s window.

## Upload draft
- Titles: "Every marble through a gate becomes TWO… until the jar BURSTS 🫙💥 #satisfying #physics #shorts" · "30 marbles → 1,563 in 15 seconds… then the jar gave up 💥 #satisfying #physics #shorts" · "Doubling marbles until the glass jar BREAKS 🫙 #satisfying #physics #shorts".
- Pinned comment: "the jar started cracking like a whole bar before it went, did you catch it?"
