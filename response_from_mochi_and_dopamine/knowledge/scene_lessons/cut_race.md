# cut_race: Laser vs Diamond Saw, first through ALL 10 layers wins (batch32)

- **Duel:** Mochi's tool is a LASER. It cuts by melting, so its speed depends on how much of the beam the material absorbs. Bolt's tool is a DIAMOND SAW. It cuts by abrasion, so its speed depends on how hard or gummy the material is. The two stacks are identical.
- **Stack (top to bottom):** wood, ice, rubber, aluminium, brick, glass, steel, copper, granite, titanium. Hardness escalates loosely; copper sits after steel so the lead keeps swapping.
- **Per-layer times** (s, laser / saw) and the reasons shown on screen:

  | Layer | Laser | Saw | Laser reason | Saw reason |
  |---|---|---|---|---|
  | WOOD | 1.0 | 1.3 | dark: burns | soft |
  | ICE | 2.6 | 0.9 | clear: beam passes | soft |
  | RUBBER | 0.8 | 3.4 | dark: melts | grabs the blade |
  | ALUMINIUM | 2.8 | 1.0 | mirror: reflects | soft metal |
  | BRICK | 1.2 | 2.2 | absorbs heat | abrasive |
  | GLASS | 3.0 | 1.6 | clear: beam passes | chips through |
  | STEEL | 1.2 | 3.0 | absorbs | hard: blade drags |
  | COPPER | 2.8 | 1.1 | reflects 95% | soft metal |
  | GRANITE | 2.2 | 2.7 | rock must melt | hardest stone |
  | TITANIUM | 1.8 | 3.0 | absorbs, holds heat | gums + overheats |

- **Tags:** each layer shows its tag for that tool. "xN FAST" means at least 1.5x faster than the other tool, "SLOW" means at least 1.5x slower, and anything else is "EVEN".
- **The WHY is drawn:**
  - On ice and glass the beam continues THROUGH the layer.
  - On aluminium and copper reflected rays bounce off.
  - Rubber makes the saw jitter.
  - On titanium the saw rim glows red as it overheats.
- **Race:**
  - Progress is analytic (piecewise-linear in time), so there is no seed.
  - Lead changes at 1.0, 3.6, 5.8, 7.5, 8.8, 11.6, 13.5 and 17.8 s. Each one after 2 s gets a "LASER/SAW LEADS!" banner.
  - The laser breaks through layer 10 at 18.95 s. The saw is at 9.74/10, about 0.8 s behind.
- **Hook:**
  - Frame 0 is mid-cut: the laser is 45% and the saw 35% into the wood, with sparks, sawdust and the beam already running.
  - Laser through at 0.55 s, saw at 0.85 s.
  - The faces ride lifts in the middle gap at the depth of their own cut, so their height difference shows who leads.
  - The layer being cut is bright and outlined; the other layers are dimmed 40% so the cut pops.
- **Payoff:**
  - At breakthrough: a burst of sparks and a glow.
  - The winner's stack splits into two halves that slide 30 px apart and rock 0.08 rad outward about their outer bottom corners, then land with a double thud at +0.48 s, followed by a dust puff.
  - "LASER WINS!" stays up for the 2 s hold. The loser's saw spins down.
  - At the rock peak, the left half's corner leaves the frame briefly.
- **Loop:**
  - The last 0.5 s dissolves the payoff into the pre-roll (t = -0.5 to 0), which flows straight into frame 0. There is no rewind.
  - The HUD switches at the midpoint of the dissolve.
  - Pre-encode seam = 0.513, the same as a normal frame step (0.513).
  - The encoded seam scores 1.06. That is H.264 noise: textured content is ~1.7 off raw at both ends, and frame 0 is an IDR while the last frame is a P-frame.
- **Sound:** no music. Everything is built in a numpy bed (`build_audio`), and the events in the sidecar have note_gain 0.
  - **Laser:** crackle on wood, frying sizzle on rubber, steam hiss plus drips on ice, a zing (1.5-2.1 kHz, lowpassed) on metals, crackle on stone, and a beating glassy zing on glass. A soft 110 Hz beam hum runs underneath.
  - **Saw:** a whine with 6 harmonics, lowpassed at 1.8 kHz. Its pitch drops 30% with load (0.12 s glide) and it spins down after the race. On top of the whine: grind, snowy crunch on ice, rubber bog plus squeaks, chips on stone, and glassy chatter on glass.
  - **Bed:** soft-clipped at 3x RMS so the limiter keys on the clacks.
  - **Through:** a damped knock tuned per material, plus the material's own sound (wood pok, ice snap, metal tick + clank, stone crunch, glass ting). These are lowpassed at 7 kHz, and the material sound is placed 12 ms after the knock.
  - **Other:** a whoosh on lead banners, a riser into the finish, then a snap + clank + crunch at the break and a double thud when the halves land.
- **Mastering:**
  - Uses `peak_db=None`. The extra post-match limiter (-4) squashed the clacks to +2 dB over the bed; without it they ride +7-10 dB and the landing thud +15 dB.
  - Lowpassing the metal tick fixed an AAC overshoot (-0.65 dBFS measured before the fix).
- **Checks (encoded Full HD, v1):**
  - Video: h264 yuv420p 1080x1920 at 60 fps, 1287 frames = 21.45 s.
  - Audio: -14.02 LUFS, peak -1.92 dBFS, last 0.5 s at -66 dBFS.
  - flash_check: 0 flashes (mean luminance 0.045).
  - Frames read at 0, 0.5, 1, 2, 3, 10.7, 18.97 and 19.4 s, plus a 1:1 crop of frame 0 and of the climax.
- **Caption (baked):** "LASER vs DIAMOND SAW" (coral / teal) and "First through ALL 10 LAYERS wins". Use `--cap ""` to drop it.
- **Commands:**
  - Stills: `NF_SCALE=1.0 NF_FAST=1 python scenes/cut_race.py --still --frame 0,600`
  - Race table: `python scenes/cut_race.py --report`
- **Note:** tools/check_loop.py does not match this scene's still naming (`<scene>_<label>_f<N>.png`, no orientation tag). Measure the seam by diffing stills 0, 1 and nf-1 directly.
- Owner review (2026-10-15): nope. Dropped.
