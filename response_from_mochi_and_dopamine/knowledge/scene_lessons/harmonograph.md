# harmonograph — a pendulum drawing machine draws a 4-pen glowing rose (Mozart 40 on piano)

- Brief: the 2026-10-10 batch22 task: a Victorian harmonograph, the drawing large and the machine small, Mochi and Bolt push the pendulums. The music changed mid-build: the owner said slow/calm music is "too slow / boring". Swan Lake was dropped. The Habanera's pitches are certain but its vocal rhythm is not, so Mozart 40 (certain, driving) was used instead.
- Physics: rotary harmonograph.
  - The pen circles at a(t)·e^{+iθ1}; the table circles the other way at b(t)·e^{−iθ2}.
  - The drawing is their relative motion z = a e^{iθ1} + b e^{−iθ2}.
  - θ1':θ2' = p:q draws a (p+q)-point star.
  - a and b decay exponentially (DA 0.14 /s, DB 0.20 /s), so the star rounds off as it spirals inward into nested shells.
  - The table runs ±1 % detuned, so each shell turns slightly.
  - Push: a 0.35 s smooth rise to a = 0.62 R, b = 0.38 R. R = 452 px, centre (540, 756).
- Escalation: 4 pens, ONE continuous line that is never lifted or restarted.
  - On the downbeat of each phrase, Mochi (pen pendulum) and Bolt (table pendulum) lunge-push.
  - The bobs slide on their rods: rod length ∝ 1/f², visible.
  - The ratio steps 2:3 → 3:4 → 4:5 → 5:6, which is a 5 → 7 → 9 → 11-point star.
  - A new pen colour drops each time: gold, rose, violet, cyan.
  - θ1' + θ2' = 2π per eighth note, so the pen hits one star tip per eighth note (the accompaniment pulse). The nib flares on every melody note.
  - Pens start at 0, 6.84, 12.29 and 17.75 s. HUD: "PENS: N" + "ratio p:q → n-point star".
- Finish/loop:
  - Around the cadence (21.9 s) the swings die out (smooth, 21.1 → 23.7 s) and the pen spirals into the centre.
  - The finished rose holds 0.7 s, then fades over 1.5 s back to the blank table. The bobs slide back to 2:3 and the counter drops to 1.
  - Frame 0 is the blank table: amplitude 0, both characters mid-push (the push anim wraps across the seam).
- Light: float buffers for ink, ink-glow, live comet and live-glow.
  - Each frame's 96 fine samples are resampled to 0.45 px and splatted bilinearly.
  - Glow (σ 1.6 / 7 px) is updated only inside the segment's crop. This is exact because the filter is linear.
  - Ink per px of line, so brightness does not depend on pen speed. Hue-preserving tone-map plus 30 % whitening.
- Music: W. A. Mozart, Symphony No. 40 in G minor, K. 550, 1st mvt, Molto allegro (1788; Mozart d. 1791). Public domain.
  - Played on our own `audio.synth_piano` as a bed: no recording, no pad, no noise bed.
  - One intro bar of pulsing eighths (as the violas open the piece), then the theme twice.
  - Theme (pickup Eb D):

    | Bar | Melody |
    |---|---|
    | 1 | D Eb D D Eb D |
    | 2 | D Bb' · Bb' A' |
    | 3 | G' G' F' Eb Eb D |
    | 4 | C C · D C |
    | 5 | C D C C D C |
    | 6 | C A' · A' G' |
    | 7 | F#' F#' E' D D C |
    | 8 | Bb Bb |

  - The second statement doubles the melody an octave down and the bass in octaves.
  - Our arrangement underneath: pulsing eighth dyads, bass on beats 1 and 3, Gm Gm Cm D7 D7 D7 D7 Gm.
  - Quarter = 176, with a 35 ms-per-beat breath of ritardando into the final G-minor cadence (Bb over a rolled Gm + low G octave).
  - Everything is faded out 1.4 s before the end.
- Args: --bpm (176), --r (452), --cap, --label, --still --frame (replays from frame 0), --report.
- Checks (encoded Full HD, v1):
  - h264 yuv420p 1080x1920 60 fps, 26.05 s (1563 frames). Render ~20 min.
  - Audio: -14.00 LUFS, peak -6.3 dBFS. Below -68 dBFS from T-1.6 s; last 0.5 s -118 dBFS.
  - flash_check: 0 flashes = PASS (mean lum 0.01).
  - Encoded seam: mean delta 0.181 (good band). Frame 0 and the last frame are both the blank table, with "PENS: 1" and the characters mid-push.
  - Frames read at 0, 0.5, 1.5, 13, 21, 24 s and the end, plus 1:1 crops of the finished rose and the machine.
- Delivered <VIDEOS_DIR>\batch22\harmonograph.mp4. Owner review: pending.
- Owner review (2026-10-09): disliked. Dropped.
