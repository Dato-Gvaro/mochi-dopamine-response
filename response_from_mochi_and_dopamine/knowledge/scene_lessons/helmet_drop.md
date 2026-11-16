# helmet_drop — Every drop is 2× HIGHER: Soft or Hard, which helmet saves the MELON? (batch62, 2026-10-31)

- Brief: docs/BRIEF_batch62.md (Mochi & Bolt 2). New scene file; caption/HUD/sound chain copied from blender_pulse / paper_plane; lib/ and tools/ untouched.
- Deliverable: `<VIDEOS_DIR>\MochiAndBolt\review\batch62\helmet_drop.mp4` (**v1**, Full HD 9:16, output label v1).
- Caption (baked; `--nocap` = base): "Every drop is ^2× HIGHER^" / "~Soft~ or ~Hard~: which helmet saves the ^MELON^?" (Soft = Bolt mint, Hard = Mochi coral, ^^ = gold).

## Story (clip times)
- Two guided drop towers on steel anvils; a melon wears a helmet and falls helmet-first (like a headform test). Bolt = PILLOW helmet (12.5 cm foam, springs back). Mochi = HARD SHELL (shell + 6 cm crushable liner; it crushes for good, so she slots a NEW HELMET after every drop, the dented one goes on a pile).
- Heights 0.5 / 1 / 2 / 4 m (ruler with ×2 rungs, gold dashed release line). Impacts at 0.15 / 3.35 / 6.55 / 10.55 s (the concerto's downbeats, beats 0/8/16/26 at quarter = 150).
- 0.15 s R1: 22 g vs 85 g, "PILLOW: 3.8× GENTLER". 3.35 s R2: "BOLT LEADS: 22 g vs 85 g". 6.55 s R3: "PILLOW FOAM 96% USED" (amber, from 7.0 s).
- R4: SLOW-MO ×8 from 60 ms before contact to 100 ms after (clip 10.07-11.35, labelled). The pillow flattens, bottoms out, its trace spikes to 444 g: "BOTTOMED OUT! 444 g", the melon splits into clean red wedges + seeds; one lands on Bolt's head (deadpan, drips). The hard liner crushes 4.9 of 5.0 cm at 85 g (98 %, a near-miss): melon intact, wobbles.
- 11.35 s cadence: "MOCHI WINS" + "the softest foam ran out of room". Dissolve 14.1-14.7 into the frame-0 state (R1 mid-fall). Length 14.70 s (882 frames).

## The physics (honest model, scenes/helmet_drop.py `impact()`)
- 1D, m = 6 kg (melon + helmet), dt 20 µs. Foam: plateau F_p (built over the first 3 mm) to the usable crush d_use, then F_p + k_d (x − d_use), k_d = 3 MN/m.
  - Pillow F_p 1.3 kN (22.1 g), d_use 10 cm → 130 J; unloading F_max (x/x_max)^6 (springs back, ~14 % returned).
  - Hard liner F_p 5.0 kN (85.0 g), d_use 5 cm → 250 J; keeps 95 % of its crush (single-use).
- g = contact force ÷ (m g) (what an accelerometer in the melon reads). Melon limit 150 g = our model value (labelled "≈150 g").
- Sim results: pillow 22.1 g at 2.5 / 4.9 / 9.6 cm (25 / 49 / 96 %), R4 bottoms out at 10.8 cm → 444 g. Hard 84.9 g every round, crush 0.75 / 1.34 / 2.53 / 4.92 cm (15 / 27 / 51 / 98 %). Impact speeds 3.1 / 4.4 / 6.3 / 8.9 m/s.
- Chip "g ≈ v² ÷ (2 × crush distance)" (exact for a flat-top pulse).

## Nerd stats
- HUD per side: PEAK g (red above the limit), FOAM USED % bar, a g-vs-time trace (90 ms axis) with the dashed red MELON LIMIT ≈150 g line from frame 0; earlier rounds faint; the bottom-out spike leaves the chart with "444 g ↑". Pillow = low long hump, hard = narrow flat-top pulse.
- At the anvil: "HIT x.x m/s" per lane, live crush "x.x cm" during contact, the permanent dent on Mochi's helmet.

## Sound
- **Piece:** L. v. Beethoven, Piano Concerto No. 3 in C minor Op. 37, I. Allegro con brio (1800-03, PD), the orchestral opening (string theme + wind answer), beats 0-28 at quarter = 150; our own C major tutti cadence at 11.35 s. Source: Mutopia PD edition `<SOUNDFONTS_DIR>\scores\beethoven_piano_concerto3_1\Concerto_No3.mid` (+ .rdf, SOURCE.txt). Replaces the brief's Symphony No. 9 II (no PD MIDI reachable; midiworld's "beeth9-2" is mislabelled).
- Timpani octave stroke (C2+C3) on every impact; soft pizzicato eighths under the winch-ups.
- SFX (tonal, ≥12 ms after a note): hard shell = crisp TOK + tiny liner crunch; pillow = low muffled thoomp; bottom-out = knock; splat = short wet body (no bed); wedge landings = small pitched plaps; latch clacks at release; winch ratchet ticks on the eighth grid; helmet swap clack-clack; banner dings.

## Checks (v1 encoded, Full HD)
- h264 High yuv420p 1080x1920 @ 60 fps, 882 frames = 14.70 s. Muxed -14.00 LUFS, peak -1.99 dBFS, last 0.5 s -240 dBFS (silent).
- RMS/s: -18.4 -17.6 -17.9 -17.3 -18.3 -18.0 -17.5 -16.5 -16.3 -15.1 -16.4 -14.7 (cadence) -16.6 -30.0 -60.7. SFX events/s: 6 11 7 7 10 7 5 10 10 1 4 7 2 0 0.
- flash_check PASS (0 flashes, mean lum 0.03). Seam mean |delta| 1.05 (the melons are mid-fall at the seam: motion, not a cut; dissolve into the pre-roll).
- Side safe zone: lanes x 196-820, characters x 115-901, HUD x 110-905, all text inside 0.10-0.84w. Content above 0.71h except the lane tags/HIT line (y 1302-1344) and the HUD (1374-1556).
- Frames read from the mp4: 0.05, 0.2, 3.4, 7.2, 7.3, 10.3, 10.75, 11.0, 11.5, 12.6, 14.65. Stills earlier at 0.67, 2.5, 6.67, 9.33, 10.67, 11.67, 13.67.
- v1 fix before delivery: the crush tag after contact reads "dent x.x cm" (the hard liner keeps 95 % of its 4.92 cm crush; the HUD says FOAM USED 98 %).

## Args
- `--limit` (150), `--sfx`, `--findb`; `--still --frame a,b`, `--audition`, `--report`, `--reuse`, `--nocap`, `--label`.

## Outcome
- (fill after upload)
