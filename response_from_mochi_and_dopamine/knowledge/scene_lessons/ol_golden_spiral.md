# ol_golden_spiral (Dopamine.exe)
- New scene, character-free (docs/BRIEF_channel2.md). Fibonacci squares tile outward in the classic golden rectangle inside a phone-screen outline, each new side = the last two added, until the golden spiral fills the SCREEN. Not related to the Mochi & Bolt `golden_spiral` (phyllotaxis / golden angle, rejected "no hook").
- Caption (baked, `--cap`; `--cap ''` = base): `Every square = the last ^TWO^ added|until the spiral fills the ~SCREEN~` (`^x^` = newest-square colour, `~x~` = gold).
- Delivered: `<VIDEOS_DIR>\DopamineExe\review\ol_golden_spiral.mp4` (**v4.2**, Full HD, label fhd42, 16.25 s, 975 frames). **4K ship file ready:** `<REPO>\output\ol_golden_spiral_ship_9x16.mp4` (2160x3840, label ship, verified; ships on the owner's OK).

## Versions
- v1 (`--n 47` + `--cam 1`, old 2-squares-per-beat timing, not kept as a flag): 47 squares to 2,971,215,073, ×phi zoom about the eye at the outline centre, 0.8 s glide. Coordinator: "a small ~250 px patch, looks like the same picture every second".
- v2 (`--cam 2`): tiling kept centred and fitted 66% -> 100% (pulsing zoom, moving eye). Owner: "moving too much, gives me vertigo; also it unfolds before the line touches its edge".
- v3 (`--leads 0`): calm camera B + square first, then its arc. Owner: "close but something is off: each square should appear AFTER the line creates space for it".
- v4 (`--alead 1.5 --fillw 0.5`): same calm camera; the gold line LEADS, each square fills in after the line's full quarter. Owner: "better, but the squares are a little too late".
- v4.1 (`--alead 1.15 --fillw 0.65`): each square starts filling in when the line is halfway through its quarter and lands 0.15 beat after it. Owner: "make the squares appear a little bit sooner".
- **v4.2 (current, final pass, `--cam 4 --leads 1 --alead 1.0 --fillw 0.75`):** each square starts filling in when the line is 25% into its quarter and lands ON the beat exactly as the line completes the quarter.

## World (logical 1080x1920)
- SCREEN: a thin white rounded phone outline (2.5 px, 85%, r 30) with a small island, x 241-775, y 340-1204 = 534 x 864, the golden portrait = exactly the final tiling. Visible from frame 0; its rim turns gold when full. Everything inside is clipped to it.
- Tiling: squares F(1) .. F(25) = 1 .. **75,025**, placed right / up / left / down of the rectangle so far; arc i = quarter circle on the far end of the shared edge, so the arcs join into one spiral. Eye = (0.6, 0.8) in square-1 units (fixed point of the x phi + 90 deg map). With N = 25 the final framing puts the big last square on top and the eye in the lower right (golden spot).
- Colour rule: one ordered gradient by age, newest -> older over 3.6 squares: teal (h .47, S .62) -> azure (.56) -> violet (.72) -> rose (.89, S .52); fills V 0.64 with a soft diagonal gloss, thin white outlines. Gold (1.0, .80, .34) = the spiral, its tip glint, the eye, the SCREEN goal; nothing else warm.
- HUD: meter y 1250 (gradient fill = squares landed / 25, white marker, gold mini-phone + "SCREEN" goal from frame 0); "+" pill y 1330 = the newest square as "a + b" (F(-1)=1, F(0)=0, so frame 0 reads "1 + 0"); counter y 1478 = the newest side; "phi ~ 1.618" in gold under it from 0.35 s after the cadence; watermark "DOPAMINE.EXE" (900 right, 1338), 35%.

## Mechanic and order (v4.2: the line leads by a hair, one square per beat)
- The gold spiral is one unbroken line drawn at a steady 90 deg per beat (arc i over beats [b_i - 1, b_i], `--alead`; arc i+1 starts the instant arc i ends, so the line never pauses). It runs out past the tiling into the black, with a glowing tip.
- When the line is 25% into quarter i (b_i - 0.75), square i starts filling in right behind its tip, over 0.75 beat (`--fillw`), growing almost alongside the line: "+" phase (first 45%: the two squares it is made of light up, the newest one's side glows in place (b), the parallel side of the one before slides onto the rest of the shared edge (a), so the joined edge = a + b), then extrusion (last 55%: the joined edge sweeps out under the line, ease-out-back 2%, none on the last 5), landing ON the beat at the instant the line completes that quarter (short brightening, outline flash, counter + pill pop, snap).
- Squares land on beats b_i (b_25 = bar 9's downbeat = the cadence); events (a square landing or a quarter of line) every beat, line moving continuously; squares landing per second 2, 1, 2, 2, 2, 1, 2, 2, 2, 1, 2, 2, 2, 1.

## Camera (v3/v4, `--cam 4`)
- The eye stays FIXED at the outline centre (508, 772) from frame 0 to 11.5 s. ONE smooth zoom-out at a constant rate of 0.97 x phi per beat (`--zrate4`, slightly slower than the squares, so the tiling grows), easing to a stop (velocity -> 0 over 0.8 s, `--ztau`) at 12.88 s: the latest stop that keeps every frame (tiling + the line running ahead) inside the SCREEN.
- ONE glide: smootherstep (zero speed and acceleration at both ends) over 1.5 s (`--gwin`), ending as the last quarter of line starts (12.98 s = square 24's landing, `--gend`), carrying the eye ~227 px to its golden spot (627, 965) (peak ~280 px/s) while squares 23-24 fill in; the last quarter of line and squares 24 (full width) and 25 then run at the final framing. No rotation, no pulsing, no reversal. Overflow 0.5 px max (clipped).
- Why the tiling is moderate: the golden rectangle flips landscape/portrait every square around an off-centre eye, so a fixed eye caps it (eye at its final spot: ~10%; at the outline centre with the final squares' limits: the values below).
- Visible tiling + line height / width (% of the outline), v4.2: 0 s 20/55, 1 s 27/44, 2 s 32/32, 5 s 27/51, 8 s 31/58, 10 s 41/42, 12 s 37/56, 13 s 41/100, 13.56 s 100/100.

## Timeline (clip s)
- Frame 0 = score beat 9.5: square 1, the line already through square 2's quarter, square 2 starting its a + b; the line runs on into square 3's quarter. Square 2 lands 0.29 s.
- 1 s: 3 squares (side 2). 2 s: 4 (side 3). 5 s: 10 (55). 8 s: 15 (610). 12 s: 22 (17,711).
- **SCREEN full 13.558 s** (the line completes the last quarter at 13.56 s as square 25 = 75,025 fills in under it and lands on the cadence). Finale: spiral glow, two calm white-gold shimmers out along the spiral, rim and goal turn gold, "phi ~ 1.618".
- Hold 2.1 s -> 0.6 s dissolve into the pre-roll. **16.25 s, 975 frames.**

## Sound
- **Music played as music:** Chopin, Etude in A-flat Op. 25 No. 1 "Aeolian Harp" (1836; Chopin d. 1849, PD), score beats 9.5-33 (mid-bar 3 to bar 9's downbeat), both hands, at the marked **104 bpm**, steady. Source: Mutopia "Mutopia-2013/03/23-489" (Peters/Scholtz 1900, Public Domain), `<SOUNDFONTS_DIR>\scores\chopin_aeolian_harp\chopin-op-25-01.mid` + `SOURCE_mutopia_489.txt`. Not on the used/banned lists, not kid-coded (the channel used Op. 10/1, 10/5, 10/12).
- Arrangement (lib/orchestra): piano plays every note (melody beat-notes vel .66, LH beat-notes .56, inner notes .36-.40, pedal per beat); harp doubles the melody notes; strings_slow hold the melody; cello + contrabass the beat bass; oohs pad on each beat's chord; a soft timpani E-flat roll under bar 8. Cadence: piano A-flat chord rolled up, strings + oohs held, cello/contrabass A-flat, soft timpani A-flat2, a rising harp + celesta cascade with the shimmer. No boom.
- SFX: one soft wood-and-glass snap per square landing (24, on the beats): tonal partial on a chord tone of the beat, 2x and 2.76x partials < 5 kHz, a short wooden body, 1.2 ms soft click; the last one an octave lower. sfx x0.30.
- `level_bed` (fin_db 7.5, cresc 3 dB), `audio.master(peak_db=None, reverb=0.5)`, last 0.6 s digital silence.

## Checks (v4.2)
- Full HD (label fhd42 = the review file): h264 yuv420p 1080x1920, 60 fps, 975 frames, 16.25 s. **flash_check PASS** (0 flashes, mean lum 0.021). **-14.00 LUFS**, peak -5.95 dBFS, last 0.5 s digital silence, energy > 5 kHz 0.019% (audio identical since v3). RMS per second: -18.4, -17.3, -17.7, -17.5, -17.3, -17.5, -16.8, -16.9, -16.7, -16.3, -16.5, -16.5, -15.9, -14.8, -13.2 (cadence), -20.5, silence; finale +3.0 dB over the late body. Seam last -> 0 0.385 vs a normal step 0.25-0.26 (check_clip 0.352). Frames read at 2, 5, 8 s; Fast stills of one beat (4.70-5.12 s) for the line/square order. Overflow past the SCREEN 0.5 px max (clipped).
- **4K ship (label ship, NF_SCALE 2.0):** h264 yuv420p 2160x3840, 60 fps, 975 frames, video and audio both 16.250 s (no re-mux needed). flash_check PASS (0 flashes); -14.00 LUFS, peak -5.95 dBFS, last 0.5 s digital silence; seam last -> 0 0.333 vs 0 -> 1 0.260 (check_clip 0.310). Frames read: 1:1 crop of the 5 s line tip + newest square, the 14.4 s finale.
- Earlier versions: v1 seam 0.723/0.721, v2 0.680/0.647, v3 0.315/0.16-0.20, v4 0.339/0.24, v4.1 0.381/0.25; all flash PASS, -14.00 LUFS.

## Flags
`--label --cap --still --frame a,b --dry --sound 0 --sfx (0.30) --fin (2.0) --bpm (104) --hold (2.1) --n (25)`. Order: `--leads (1)` (0 = v3, square first), `--alead (1.0) --fillw (0.75)` (v4 = 1.5 / 0.5, v4.1 = 1.15 / 0.65). Camera: `--cam (4)` with `--zrate4 (0.97) --ztau (0.8) --gwin (1.5) --gend (-(alead-1) beats)`; `--cam 3` = eye fixed at the golden spot (tiny build); `--cam 2` = v2 (`--fmin --fpow --zsig --csig`); `--cam 1` = v1 (`--lead --cwin`). Look: `--fv (0.64) --cspan (3.6)`. `--dry` prints squares/s, the overflow check and the eye speed.

Owner review (2026-10-23): "moving too much, gives me vertigo; it unfolds before the line touches its edge" -> v3: steady smooth camera; each square unfolds only after the spiral arc reaches the corner.

Owner review (2026-10-23): "close, but each background square should appear only after the line has created space for it: the line goes out of the square, and when it has moved enough for another square, that square appears" -> v4.

Owner review (2026-10-23, v4): "better, but the squares are a little too late; make them appear a little earlier" -> v4.1: each square starts filling in at the line's halfway point and lands 0.15 beat after the line finishes its quarter.

Owner review (2026-10-23, v4.1): "make the squares appear a little bit sooner, to be more satisfying to watch" -> v4.2 (final pass): fill starts at 25% of the quarter, lands as the line completes it; 4K ship file rendered.
