# ol_magnet_sphere (DopamineEXE, channel 2)
- Batch 57 (docs/BRIEF_batch57.md). Shiny magnet balls lie scattered on a table around one resting ball. One ball rolls in and clicks on; **every magnet that sticks pulls in the 2 nearest free ones**, so the clicks double each round (1, 2, 4 ... 128) and the cluster grows into a ball of **256 magnets**; the last one clicks in and the ball spins once.
- Caption (baked, `--cap`; `--cap ''` = base): `Every magnet that ^STICKS^ pulls in 2 more…|until it's a perfect ~SPHERE~`.
- Delivered: `<VIDEOS_DIR>\DopamineExe\review\ol_magnet_sphere.mp4` (Full HD, seed 1, label fhd + sound re-mux at sfx 2.2, **9.07 s, 544 frames**). No 4K yet. The first mux (clicks 6 dB quieter, thinned harder) is kept as `output/ol_magnet_sphere_fhd_v0sound_9x16.mp4` (scratch).
- **Shipped 4K (batch58, unchanged):** `<VIDEOS_DIR>\DopamineExe\schedule\2026-11-02\2_ol_magnet_sphere.mp4` (seed 1, label ship, `NF_SCALE=2.0`), 16:00 local Nov 3 (= 07:00 US East Nov 3); owner: "nice, I have high hopes". FHD review copy archived as `archive\ol_magnet_sphere_fhd.mp4`.
- 4K checks: h264 High yuv420p 2160x3840, 60 fps, 544 frames, 9.07 s; **flash_check PASS** (0 flashes); **-13.96 LUFS**, peak -6.37 dBFS, last 0.5 s digital silence; seam mean |delta| 0.334. Frames read at 0.1, 3, 5.5, 6.6 (+ 1:1 crop of the ball), 7.4, 9.0 s = the FHD timeline.

## World (logical 1080x1920)
- A round dark table (r 400 table px, seen from 52° above, orthographic: screen y = y sin52 + z cos52), thin white rim line, inside 0.10-0.84 w. Balls r 15, drawn as glossy spheres (radial gradient, sharp highlight, table reflection on the lower rim) with soft table shadows, depth-sorted.
- The field: 254 balls on a jittered hex grid in an annulus (r 150 -> ~356), hue = the side of the table each ball sits on (one full ordered sweep, S 0.70): the sphere ends up wrapped in a rainbow by direction. The first two (resting + roller) are chrome.
- Cause -> effect: on every click, thin lines from the ball that stuck to the 2 it pulls (0.35 s) and a white ring on each pulled ball as it starts; a white ring + sparkle on each click.
- One smooth zoom: x1.75 onto the ball, starting 1.3 s before the last click (1.6 s, smoothstep); the last balls fly in from the edges.
- Finale (6.57 s): the ball spins one full turn about the vertical (1.5 s, smoothstep), a gold sheen runs round it, 12 gold sparkles, counter gold.
- HUD: meter y 1290 = MAGNETS n / 256 (progress to the gold SPHERE goal from frame 0), "ROUNDNESS xx.x%" readout under it. Counter y 1488 "n/256" + "+2" pill (pops on every click), label MAGNETS. Watermark DOPAMINE.EXE 35%.

## Physics (scenes/ol_magnet_sphere.py `simulate`, seeded)
- Pull: from rest, a = K N^0.8 / (d + 2r)^4 along the line to the contact point (dipole-like 1/d^4; N = magnets already stuck, so a bigger cluster pulls harder), integrated at 2400 Hz; the ball slides, then hops up onto its site over the last 45% (smoothstep). K0 = 2.2e10.
- Snap: the free close-packed (FCC, spacing 2r) site adjacent to the cluster that is nearest the cluster's centre, biased to the side the ball came from (+ a small bonus for more contacts). The cluster rests on the table (its lowest ball touches it; eased 0.12 s).
- Pulled = the 2 nearest free balls to the cluster at the moment of the click; they start 0.04 s after it.
- ROUNDNESS = Wadell sphericity of the cluster's outer surface (convex hull of the balls): pi^(1/3) (6V)^(2/3) / A. 100% = a perfect sphere; 1 ball = 100%, 2 balls 91.6%; the honest end is **97.6%**.

## Timeline (clip s, seed 1)
- 0.15 s the roller clicks on. Rounds land at 1.3, 2.35-2.43, 3.03-3.15, 3.61-3.88, 4.23-4.53, 4.87-5.31, 5.65-6.57 s (2, 4, 8, 16, 32, 64, 128 clicks).
- Clicks/s 1, 2, 4, 24, 58, 107, 59 (in 0.57 s = ~104/s). Magnets at s 1, 2, 4, 8, 32, 90, 197, 256.
- **6.57 s** the last magnet = the cadence; spin 6.72-8.22 s; hold 1.9 s, 0.6 s dissolve into frame 0 (the roller about to touch).

## Sound (the clicks are the star)
- Per click: a crisp metallic snap (a short ringing tone + 2.41x / 3.93x partials < 5.5 kHz + a tiny body thump) and the settle: two small re-clicks 26 ms and 47 ms later (click-click-clack). Pitched to a note the music sounds there, 2 octaves up (G5-C7), rising a little as the ball grows; gain / sqrt(rate/4). Every click is heard: one within 7 ms of the last is nudged later (<= 24 ms, else dropped): 169 of 255 sounded. The last one: a bright G6.
- **Light music:** E. Satie, Gymnopedie No. 1 (1888; d. 1925, PD), score beats 12-24: bar 5 (the melody's entrance) to the G-major-7 downbeat of bar 9 = the last magnet. Steady **110.4 bpm** (brisker than usual). Source: Mutopia Project `gymnopedie_1.mid` (public domain), saved at `<SOUNDFONTS_DIR>\scores\satie_gymnopedie1\` + SOURCE.txt. Soft piano (melody + bass/chords), a harp doubling, a quiet string pad; the arrival = G-maj7 piano + strings + harp roll + falling celesta. Not on any used list; not kid-coded; not banned.
- Mix: SFX x2.2 over the bed (bed -18.5 LUFS vs clicks -24.2 at x1.0 -> about level at x2.2), `level_bed` (+4 dB crescendo, cadence +6 dB), `audio.master(peak_db=None, reverb=0.5)`, last 0.6 s digital silence. Spectrum: 0.0% > 6 kHz, 0.4% 3-6 kHz (no hiss).

## Checks (encoded Full HD, delivered file)
- h264 yuv420p 1080x1920, 60 fps, 544 frames, 9.07 s. **flash_check PASS** (0 flashes, mean lum 0.021).
- **-13.96 LUFS**, peak -6.37 dBFS, last 0.5 s digital silence. RMS/s (audio test): -18.8, -18.9, -17.3, -16.4, -16.5, -15.9, -15.4, -15.0 (cadence), fade, silence. Click SFX/s 1, 2, 4, 24, 32, 65, 41 (in 0.57 s).
- Seam (check_clip): mean |Δ| **0.528**.
- Frames read from the mp4 at 0.1, 0.5, 1.4, 3, 5.5, 6.6, 7.4, 9.0 s; fast stills at 0.5, 1.3, 3.3, 5, 5.5, 6.2, 6.7, 7.2, 7.8, 8.3 s.

## Doubts
- **"Perfect sphere" vs 97.6%:** 256 close-packed balls make a faceted ball (it reads as a ball of balls, slightly hexagonal from some angles); the readout says 97.6%. The caption promises "perfect"; the meter goal is reached (256/256).
- 0.2-1.3 s: after the first click only 2 balls creep in (the 1/d^4 pull is slow far away, then whips). The field itself is a full rainbow frame, but events are sparse until ~3 s.
- Click rate peaks in the last round; the final ~0.1 s has the last 3-4 stragglers (the brief's "last ball clicks in").
- The pull is a 1-D creep-and-snap along a line (no ball-ball collisions in the field; pulled balls can pass over others).

## Flags
`--seed (1) --label --cap --still --frame a,b --dry --audio --sound 0 --sfx (2.2)`. Physics `--el (52) --rb (15) --k0 (2.2e10) --kexp (0.8) --delay (0.04) --fr0 (150) --fr1 --gap (7) --vroll (260)`. Clip `--spin (1.5) --hold (1.9) --zoom (1.75)`.

## Upload draft
- Titles: "Every magnet that sticks pulls in 2 more… until it's a SPHERE 🧲 #satisfying #physics #shorts" · "256 magnet balls click together into one ball 🧲 #satisfying #physics #shorts" · "Can magnets build a perfect sphere on their own? 🧲 #satisfying #physics #shorts".
- Pinned comment: "turn the sound up for the last second, 128 clicks at once… what shape should they make next?"
