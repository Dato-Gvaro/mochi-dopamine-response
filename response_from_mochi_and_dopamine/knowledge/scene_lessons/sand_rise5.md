# sand_rise5 — ONE room, ONE hatch (batch70)

- Brief: docs/BRIEF_batch70.md §4 = research/mochi_performance_2026-11-05.md pick 2. New file `scenes/sand_rise5.py`, generated from sand_rise4.py v6 (untouched).
- Caption: "Every second the room fills with ~MORE~ balls" / "~ONE~ way out: who gets out first?". The hatch reads EXIT + "ONE WAY OUT" from frame 0.

## THE ONE CHANGE
- One room 760 px wide (screen x 128-888) instead of two 360 px rooms. One hatch in the middle (± 54 px); Mochi's ladder at local x 262, Bolt's at 498. Two showers (local x 130 / 630), each = sand_rise4's calibrated SCHED_N (total ×2, N_FULL 4,096 = the FULL line). Same ball solver, same Mochi draw (seed 1150: 70 % jumps, 3 rungs, a miss tumbles 3-4), same Bolt (a rung per beat).
- The hatch is a one-person trapdoor: open for the first one through, springs shut 0.4 s later (LOCKED), kicked open by the winner at T_KICK for sand_rise4's rope rescue ("again?").
- The bodies are rigid discs for the balls and for each other (the lower one is held below if they touch). On separate ladders they never touched in this run.

## Honest result (seed 6; clip = sim − 6.2)
- Lead changes (clip): MOCHI 1.5, BOLT 2.35, MOCHI 4.0 (she is 0.1 m from the hatch), then her draw misses: a 4-rung tumble at 4.3 → BOLT LEADS 4.85, BOLT ESCAPES 5.17, Mochi 0.81 m short. LOCKED 5.57, FULL! 5.8, rope 6.3-6.7, tugs 6.8-8.3, Mochi pops out 8.8 ("again?").
- Mochi's tumbles in the clip: 1.8 and 4.3 s (4 rungs each).

## Sound
- Mendelssohn, Midsummer Night's Dream Intermezzo Op. 61/5 (PD; Mutopia MIDI, read from the zip), score beats 0-27 re-timed (quarter 0.326 s) so beat 27 = the pop-out, + our A-major tutti (harp, horns, timp). sand_rise4's tonal SFX re-pitched to A minor.

## Checks (encoded Full HD, label b70)
- h264 yuv420p 1080x1920 60 fps, 624 frames = 10.40 s. −14.01 LUFS, peak −5.5 dBFS, last 0.5 s silent. flash_check 0 = PASS. Seam 4.81 (thousands of moving balls; sand_rise4 5.55).
- RMS/s −19.8 −18.0 −18.3 −18.5 −16.9 −16.3 −15.9 −16.3 −14.5 −16.5.
- Frames read: 0, 1.6, 4.2, 5.25, 5.8, 7.2, 9.0, 10.2 (+ Fast stills 0-520).

## Doubts
- The pile is V-shaped (showers at the outer walls, the ladders in the dip): it reaches the climbers' feet only in the last ~3 s.
- 10.4 s (frame 0 ≈ 40 % full at the walls, as the brief asked); shorter than sand_rise4.
- sand_rise4's flood schedule was calibrated for one 360 px room; doubled here, not re-calibrated.

Delivered `<VIDEOS_DIR>\MochiAndBolt\review\batch70\sand_rise5.mp4`. Owner review: pending.
