# press_tools2 — comment reply: the Trident goes DEEP (batch70)

- Brief: docs/BRIEF_batch70.md §3 = research/mochi_performance_2026-11-05.md pick 1. New file `scenes/press_tools2.py` (from press_tools.py; untouched). Opens on @Haroldedits123-3D1T's comment card (verbatim "Trident would have been the winner if he went deeper", drawn, no likes/age), card 0-2.5 s, then the caption "Every ball ~HIT~ splits into 3" / "Now the ~Trident~ goes DEEP like the ~Spike~:" / "which ~OVERFLOWS~ first?".
- THE ONE CHANGE: the trident drives to the floor (no D_TRI stop). Honest cost: same jackhammer power P = F·v; in the pile 3 prongs = 3× the force → TRI_IN = SPK_DN/3 = 1,667 px/s (above the pile both keep press_tools' speeds). Everything else = press_tools (×3 split, MAX y 660, stops, overflow snap). T_PAYOFF 1.8 → 2.6 s (time for the payoff line).

## Honest result (seed 0)
- Balls trident/spike per s: 5/9 49/27 165/91 403/185 795/349 1,261/521 1,759/817 2,127/1,123 2,547/1,511 2,847/1,919 3,229/2,247 3,441/2,619 3,753/2,929.
- The TRIDENT OVERFLOWS at clip 12.98 s with 3,951 vs 3,243 → "TRIDENT WINS!" + "THE COMMENT WAS RIGHT!". It leads from ~0.8 s to the end (no lead change). Seed 1: trident too (15.2 s, 4,269 vs 3,543); MAX 600: trident (19.0 s).
- Why: deep, 3 columns of fresh big balls per stroke beat 1 column 3× faster. The spike's crush rate climbs to the end (155-204/s from 5 s); the trident's peaks at 4-5 s (230-249/s) and eases.

## Sound
- One note per crush (70 ms groups), walking Schubert's Marche militaire D. 733/1 (PD; Mutopia 1545, primo top line bars 5-20, an octave down; DopamineEXE's ol_rice_board used it, never Mochi & Bolt). press_tools' crunches, tinks, stab, snap; cadence re-voiced to D major.

## Checks (encoded Full HD, label b70)
- h264 yuv420p 1080x1920 60 fps, 15.60 s. −14.01 LUFS, peak −8.6 dBFS, last 0.5 s silent. flash_check 0 = PASS. Seam 1.74 (press_tools 2.46: tools mid-strike at frame 0).
- RMS/s −18.0 −17.0 −16.7 −16.2 −16.7 −16.1 −16.7 −16.6 −16.3 −16.1 −16.6 −16.3 −16.3 −14.2 −19.4.
- Frames read: 0, 2.9, 13.0, 13.7, 14.3, 15.0 (+ Fast stills).

## Doubts
- No lead change: the honest answer is "you were right", from the start.
- The 1/3 speed is the constant-resistance model (force per prong); a viscous model (1/√3) favours the trident even more.

Delivered `<VIDEOS_DIR>\MochiAndBolt\review\batch70\press_tools2.mp4`. Owner review: pending.
