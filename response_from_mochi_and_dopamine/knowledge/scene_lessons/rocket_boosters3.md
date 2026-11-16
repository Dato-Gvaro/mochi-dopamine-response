# rocket_boosters3 — Bolt HITCHHIKES on Mochi's rocket (batch69)

- Brief: docs/BRIEF_batch69.md §3 (owner: "let Bolt win again with an ABSURD thing"), coordinator follow-up: an honest INTERACTION with Mochi. New file `scenes/rocket_boosters3.py` (generated from rocket_boosters2.py; rocket_boosters2 untouched). Opens on @<viewer>'s comment card as before. Caption: "Rematch: tank + ~2 BOOSTERS~ vs ~3 STAGES~" / "who reaches ~ORBIT~ first?".

## Why an interaction (swept first, all honest, all LOSE)
- Mochi solo reaches 400 km at sim 10.23, Bolt solo 12.58 (161 km behind at her crossing).
- Fireworks bundle carried from liftoff (black-powder exhaust 0.3x ours, up to 200 t, any burn 0.5-2 s): lit at liftoff 11.43, later = worse; even at 0.5x ours 10.76. After stage 3 burnout no add-on can win (needs ~4.6x our exhaust speed).
- Dumping the whole capsule (10 -> 0.3 t): best 11.75 (at liftoff). Soda bottle / party popper: far smaller.
- So the absurd thing has to take energy from MOCHI: a harpoon rope.

## THE ONE CHANGE
- At sim −0.6 (clip frame 0) Bolt's suction-cup harpoon on a rope sticks to Mochi's tank (rope length = the 2.42 km gap then); he is towed for TOW_S = 1.25 s, then lets go. Both keep burning exactly their own rules (Mochi: rocket_boosters2's core + 2 boosters; Bolt: ep. 1's stages).
- One coupled integrator (dt 1/240): a = (thrust ∓ T)/m − g for each; rope = spring-damper that only pulls (K 400, C 60; T ≥ 0). Max pull ≈ 790 t-force (shown live as "ROPE PULL … t").

## Honest result
- Mochi still leads the whole flight… until 0.2 s before the line: Bolt passes at sim 11.57 ("BOLT TAKES THE LEAD!"), reaches ORBIT at 11.75 = the cadence (BOLT WINS); Mochi arrives 0.28 s later (12.03; "IN ORBIT 0.3 s LATER").
- What the 1.25 s tow did: Mochi's booster drop at 31 km (solo 40), core dry at 120 km (solo 144); Bolt's stage 1 drop at 26.6 km (solo 13), stage 3 dry at 239 km (solo 194).
- Sensitivity (harpoon at −0.6): tow 1.0 s → Mochi wins (11.39 vs 11.98); 1.25 s → Bolt by 0.29 s; 1.5 s → Bolt by 1.36 s; ≥ 2.5 s Mochi never reaches orbit. Tow length is Bolt's choice (the joke: he lets go as soon as it's enough).

## Timeline (clip = sim + 0.6; 15.75 s = 945 frames)
- 0.0 harpoon sticks ("HEY!!", "HITCHHIKING!", rope pull readout) · 1.85 LET GO! · 2.5 boosters dropped · 3.6 / 7.8 / 10.2 stage drops · 5.24 Mochi fuel empty · 12.17 BOLT TAKES THE LEAD! · 12.35 BOLT WINS! / IN ORBIT! · 12.63 Mochi in orbit (0.3 s later), annoyed · dissolve 15.15-15.75.

## Sound
- Valkyries as rocket_boosters2 (re-timed: cadence = Bolt's crossing). Added: a harpoon whoosh (glide) + thunk at the hook, a release twang + tick.

## Checks (encoded Full HD, label b69)
- h264 yuv420p 1080x1920 60 fps, 945 frames = 15.75 s. −14.00 LUFS, peak −2.00 dBFS, last 0.5 s digital silence.
- RMS/s −19.3 −17.4 −17.8 −16.9 −17.7 −17.4 −16.6 −17.4 −16.2 −16.3 −16.4 −16.0 −14.1 −14.4 −20.1. SFX events/s 14 12 11 15 11 10 9 15 10 9 21 10 16 0.
- flash_check pass. Encoded seam 1.41 (space → blue-sky dissolve; rocket_boosters2 1.13).
- Frames read: 0.1, 0.6, 1.3, 12.2, 12.5, 13.4 (+ Fast stills 0, 30, 70, 120, 400, 725, 740, 800).

## Doubts
- Mochi's flight is not rocket_boosters2's bit-for-bit any more (the brief asked for that; the coordinator chose the interaction, which must slow her).
- The hook happens at frame 0 (the harpoon flight is before the clip).
- The tow length (1.25 s) decides the margin: a shorter tow loses, a longer one wins big.

Delivered `<VIDEOS_DIR>\MochiAndBolt\review\batch69\rocket_boosters3.mp4`. Owner review: pending.
