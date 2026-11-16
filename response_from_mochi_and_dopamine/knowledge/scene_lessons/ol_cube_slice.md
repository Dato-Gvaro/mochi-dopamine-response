# ol_cube_slice (DopamineEXE, channel 2)
- Batch 59 (docs/BRIEF_batch59.md #3). A big translucent 34 cm cube stands on a trapdoor inside a glass box. Laser sheets slice it, alternating axes (x, y, z): **every slice cuts every piece in 2** (1 -> 2 -> 4 ... -> 4,096). After 12 slices the pieces are 1.8 cm dice (pips appear); on the cadence the trapdoor swings open and the 4,096 dice pour into the box and pile up.
- Caption (baked, `--cap`; `--cap ''` = base): `Every slice cuts it in ^2^…|until it's a pile of ~DICE~`.
- Delivered: `<VIDEOS_DIR>\DopamineExe\review\ol_cube_slice.mp4` (Full HD, seed 4, label fhd3, **10.50 s, 630 frames**).
- **Shipped 4K (batch60, approved "interesting"):** `<VIDEOS_DIR>\DopamineExe\schedule\2026-11-07\2_ol_cube_slice.mp4` (`NF_SCALE=2.0 python scenes/ol_cube_slice.py --label ship`, defaults, seed 4; the cached pour sim), 16:00 local Nov 8 (= 07:00 US East Nov 8). FHD review copy archived as `archive\ol_cube_slice_fhd.mp4`.
- 4K checks: h264 High yuv420p 2160x3840, 60 fps, 630 frames, 10.50 s; **flash_check PASS** (0, mean lum 0.034); **-14.00 LUFS**, peak -6.45 dBFS, last 0.5 s digital silence. Events json + audio wav bit-identical to the reviewed fhd3. Frames read at 0.1, 3, 7.6, 9.6 s = the FHD timeline.

## World (logical px = mm; orthographic camera yaw 35°, pitch 22°)
- Glass box 520 x 520 footprint, one thin white line (far edges 45%, near edges 85%), faint floor tint. Trapdoor: two grey translucent plates at height 232, hinged at the side walls.
- Cube E 340 (34 cm), translucent (alpha 0.72 for big pieces, opaque past 512 pieces: only the outer shell is drawn). Colour = ordered sweep across the cube (teal top-back-left -> green -> gold -> red -> magenta bottom-front-right, S 0.68); big pieces get the sweep as a per-face gradient, so frame 0 is multi-hue.
- Lasers: hot-pink translucent sheets with a bright front edge + emitter edge; vertical sheets (x and z cuts) descend from above, flat sheets (y cuts) sweep in from the left. No flash.
- **Kerf (honest cut):** each cut burns away 3 mm: side cuts leave 3 mm gaps (eased open over 0.12 s), flat cuts let every piece above settle by 3 mm. Piece sizes are exact: 34 -> 17 -> ... -> 1.84 cm (15 kerfs per axis).
- Dice: a standard die per piece (opposite faces sum to 7, random orientation), pips drawn as true projected ellipses.
- HUD: meter y 1300 = slices done / 12 (tick per slice) toward a gold DICE goal; readout "PIECE 17 × 34 × 34 cm" -> "1.8 cm DICE". Counter y 1500 = PIECES (-> DICE, gold) + "×2" pill (pops per slice). One smooth zoom (x1.15) onto the pile 8.0-9.4 s. Watermark 35%.

## Physics (`simulate` = the pour; the cutting is exact geometry)
- 3-D PBD: 4,096 spheres (r = half the die edge, starting on the settled lattice), Verlet, 6 substeps x 3 iterations, cKDTree contacts, tangential friction between touching dice, floor friction 0.6, box walls; the two trapdoor plates are kinematic colliders swinging down over 0.75 s (ease-in), so the block tilts, slides and breaks from the middle. Splash cap: no die rises faster than 350 px/s. g = 2,000 px/s^2 (brisk). Sim ~7 s, cached; `--resim`.
- Each die tumbles with a random spin (4-11 rad/s) from release; the spin dies out as it comes to rest.

## Timeline (clip s, seed 4)
- Frame 0: the first laser sheet a third of the way down the whole cube. Slices complete at 0.19, 0.94, 1.69, 2.44, 3.19, 3.94 (every 2 beats), 4.50, 5.06, 5.62, 6.19 (1.5 beats), 6.56, 6.94 s (1 beat): 2, 4, 8 ... 4,096.
- **7.50 s the trapdoor opens** (score beat 20 = the cadence into A major); dice land 7.65-8.5 s (4,968 landing/bounce contacts), settle by ~9 s; pile 184 px high. Hold to 9.9 s, 0.6 s dissolve back to frame 0.

## Sound
- **Music:** J. S. Bach, The Well-Tempered Clavier I, **Prelude No. 5 in D major BWV 850** (1722; d. 1750, PD). Mutopia Project `bwv850a.mid` (Public Domain; Breitkopf & Hartel 1866), saved at `<SOUNDFONTS_DIR>\scores\bach_prelude_d_bwv850\` (+ .rdf). Score beats 0-20 (bars 1-5, the perpetual 16ths, to the cadence into A major on bar 6's downbeat = the trapdoor) at a steady 160 bpm; our A-major tutti held under the pour. Not on any used list; not kid-coded; not banned.
- Arrangement: piano both hands (velocity crescendo), pizzicato bass, harp on the 8ths, a string pad from bar 3, timpani roll into the cadence; cadence = strings, piano, horns, timpani A, a falling celesta.
- SFX: a clean falling laser "zap" per slice, a crisp glass tick per piece cut (2^k per slice, spread over the sweep, >= 14 ms, pitched to the score), a low clunk for the trapdoor, plastic dice clacks for every landing/bounce (>= 9 ms, A-major tones). `audio.master(peak_db=None, reverb=0.45)`, last 0.6 s digital silence.

## Checks (encoded Full HD, delivered file)
- h264 High yuv420p 1080x1920, 60 fps, 630 frames, 10.50 s. **flash_check PASS** (0 flashes).
- **-14.00 LUFS**, peak -6.45 dBFS, last 0.5 s digital silence. RMS/s (audio test) -19.0, -18.9, -17.7, -16.9, -16.6, -16.7, -15.9, -14.9, -15.1, -21.2 (hold), silence. SFX events/s 4, 4, 9, 16, 18, 13, 26, 20, 48, 13.
- Seam mean |delta| 0.210.
- Frames read from the mp4 at 0, 0.3, 1, 2, 3, 4, 5, 6, 6.7, 6.95, 7.2, 7.6, 7.8, 8.1, 8.3, 8.6, 9.5, 9.6, 10.4 s; 1:1 crops at 7.08 s (the dice cube: pips on the shell) and 9.6 s (the pile: tumbled dice with pips).
- Side safe zone: the box 146-870 px; during the x1.15 zoom the pile spans ~0.12-0.86 w (the box's side plates go wider: decoration).

## Doubts
- Past ~2,048 pieces the cube reads as a fine textured block at phone size; the dice (and pips) only read clearly in the pile and at 1:1.
- The pile fills the box floor as a mound-topped layer (the box contains it) rather than a free cone.
- 5-6 s the SFX rate dips slightly (13/s) between the 2-beat and 1.5-beat slices.
- The dissolve cross-fades the zoomed pile into frame 0 (a reset, not a seamless loop).

## Flags
`--seed (4) --label --cap --still --frame a,b --dry --audio --resim --sound 0 --sfx (1.0)`. Physics `--g (2000) --sub (6) --iters (3) --vup (350) --trap (0.75)`. Clip `--bpm (160) --pour (1.9) --hold (0.5) --zoom (1.15)`.

## Upload draft
- Titles: "Every slice cuts it in 2… until it's a pile of DICE ✂️ #satisfying #physics #shorts" · "12 laser slices turn one cube into 4,096 dice ✂️ #satisfying #physics #shorts" · "How many slices to turn a cube into DICE? ✂️ #satisfying #physics #shorts".
- Pinned comment: "12 slices, 4,096 dice, and every single one has its own pips… how many slices did you guess it would take?"
