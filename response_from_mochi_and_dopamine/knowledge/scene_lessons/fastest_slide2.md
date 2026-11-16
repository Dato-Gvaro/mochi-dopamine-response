# fastest_slide2: the brachistochrone race with an ASMR soundtrack (no music)

- **Owner review of fastest_slide (2026-10-11):** "good, but replace the song with sound effects — ball sound or some pleasant ASMR sound".
- **What is reused:** the visuals, physics, timing, hook and loop are fastest_slide v2. `scenes/fastest_slide2.py` imports `fastest_slide` unchanged, so the frames are identical. The delivered clip reuses the v2 video stream (`--video`).
- **What is new:** only the soundtrack, all our own numpy/scipy synthesis. There are no samples, no music, and nothing to credit. The round story and numbers are in docs/scenes/fastest_slide.md.

## Sound design

The bed is passed to `kit.deliver(bed=...)` with silent sync events. master() runs with peak_db -6, because the clacks are impulses.

### ROLL (one per bead)

Every control parameter is driven by the bead's TRUE physics speed v, sampled at 1 kHz.

| layer | how it follows v |
|---|---|
| filtered noise | band centre (brightness) = 170 + 175·v Hz (11-band filter bank, 4th-order low-pass at 2.6 kHz) |
| "singing rail" tone | 90 + 40·v Hz, plus 2nd and 3rd harmonics; pitch rises with speed |
| low rumble | low-passed at 140 Hz |
| grain | at the bead's rotation rate, 14 % AM |
| level | (v / 7.5)^0.7 |

- **Pan:** follows the bead's x.
- **Slow-mo:** pitch × (0.62 + 0.38·rate).
- **After the gate:** a 60 ms coast-out.
- **Gain per bead:** Bolt and Mochi 1.0, ghosts 0.38, R4 beads 0.8, R5 beads 0.48.
- **Result:** you hear the cycloid bead get bright and high first; the straight-ramp bead catches up in pitch only late.

### One-shots

- **Release:** a soft click, one per round.
- **Glass "tink":** when a bead is set down (Mochi's head start, the two beads lifted back, the 5 R5 extras rising by a whole tone each).
- **Finish:** a gate CLACK (rounded modal 1.65/2.78/3.9 kHz + a 165 Hz thump), then a bell chime 12 ms later (mixer 10 ms rule).
  - Bolt: E5, bright.
  - Mochi: C5, soft.
  - Ghosts: G4, quiet.
  - R4 tie: the two clacks are 12 ms apart, and the chimes form a major third.
- **Slow-mo start:** a soft whoosh (1.5 kHz → 320 Hz).
- **Rewind (0-0.82 s):** a tape whoosh (380 Hz → 2.1 kHz, flutter) plus the finale chord swelling in reverse. Sound starts on frame 0 at a -10 dBFS peak.
- **Finale:** 7 rolls converge into ONE clack (×1.5) and a 7-note chime chord, C major add 9 (C4 E4 G4 C5 E5 G5 C6), at 19.42 s.
- **Tail:** fades to zero between T-2.25 and T-1.45.

## Checks (encoded Full HD v1)

- **Video:** h264 yuv420p 1080x1920 60 fps, 1399 frames = 23.32 s.
- **Audio:** -14.00 LUFS, peak -7.84 dBFS. The window T-1.3 to T-0.5 peaks at -54 dBFS and the last 0.5 s at -90 dBFS.
- **flash_check:** 0 = PASS.
- **Encoded seam:** 0.464 (pre-encode 0.000, same frames as v2).
- **Clack onsets in the muxed mp4:** the key moments land within 3 ms of the physics finish times. Detected: R1 release 0.819, R1 Bolt 2.022, Mochi 2.243, R2 Bolt 5.020, R4 tie 13.420, R5 chord 19.419.
- **Unverified:** there was no listening test.

## Delivery

- **Delivered:** <VIDEOS_DIR>\batch27\fastest_slide2.mp4 (Full HD).
- **Owner review:** pending.
- Owner review (2026-10-11): 'ok, let's try what viewers react to' -> APPROVED (test), 4K.
