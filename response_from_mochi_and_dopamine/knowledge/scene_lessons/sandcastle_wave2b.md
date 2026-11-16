# sandcastle_wave2b — rematch v2: Mochi's castle on a HILL, Bolt chills (batch68)

- Brief: docs/BRIEF_batch68.md §5 (owner: "Bolt isn't doing anything new so he can chill, lying with a cocktail; Mochi shouldn't copy him and admit Bolt was right; she tries a higher castle, on a hill"). New file `scenes/sandcastle_wave2b.py` (generated from sandcastle_wave2.py; sandcastle_wave / sandcastle_wave2 untouched). Deliverable `review\batch68\sandcastle_wave2_v2.mp4`.
- Caption: "Rematch: her castle on a ~HILL~" / "whose castle ~SURVIVES~?"

## THE ONE CHANGE
- Mochi: a sand HILL (new material 4 = loose dune sand: erodes at the castle rate, no wall bonus, no structural block, so it slumps cell by cell under rule 1) with a flat top; a keep (88 × 104 px) + top turret on the plateau. Budget = her ep. 1 castle, 2,733 cells: hill 2,007 + castle 721 = 2,728 (the plateau width is solved to fit; hill 120 px = 55 cm high, slopes 1.3 run/rise, x 204-624).
- No wall for Mochi (walled()/wall_up() = Bolt only). Waves, sand rules, Bolt's lane: ep. 1's. The HUD's % = CASTLE cells only (the hill is shown via "HILL -x%" banners).
- Bolt lounges: a striped beach chair, reclined (rot −0.30, small reactions), a cocktail with a paper umbrella, sips at 1.05 / 4.25 / 7.05 / 9.45 s (a soft slurp bloop each), a toast after the win. Picture only; no pats.

## Honest result
- Waves 1-7: her castle stays 100 % (the plateau stays above the run-up); the hill's sea face is eaten: hill 100 → 96.6 (w4) → 91.0 (w5) → 79.4 (w6) → 58.5 % (w7).
- Wave 8 (1.71 m, the cadence): the run-up reaches GL−163 px, 43 px over the plateau; the undercut hill slumps and takes the castle with it: 100 → 0 % (sim 11.53 = "FLATTENED!" + "BOLT WINS!"). Bolt 100 % (wall 545 → 478 cells, as ep. 1).
- Not tuned: hill height 100 / 120 / 140 px and slope 1.0 / 1.3 all give "100 % through wave 7, 0 % in wave 8". With her ep. 1 sand she cannot build a hill above wave 8's 163 px run-up.
- Vs ep. 1 she does much better: ep. 1 was 24 % after wave 6, 15 % after wave 7.

## Timeline (clip = sim + 0.267; 14.37 s = 862 frames)
- HIGHER GROUND! 1.5 s; CHILLING (Bolt) 0.9-3.5 s; HILL −12 % 8.6 s, HILL −21 % 10.2 s; THE LOW WALL HOLDS! 10.0 s; wave 8 lands 11.47; FLATTENED! + BOLT WINS! 11.8 s; dissolve 13.77-14.37.

## Sound
- Vivaldi, Summer RV 315 Presto (Mutopia #336), as batch67's sandcastle_wave2 (not Vltava). SFX as ep. 2 minus the wall thud for Mochi (her waves splash on the hill), + Bolt's sip bloops.

## Checks (encoded Full HD, label b68)
- h264 yuv420p 1080x1920 60 fps, 862 frames = 14.37 s. −14.01 LUFS, peak −2.00 dBFS, last 0.5 s digital silence.
- RMS/s −18.5 −18.1 −18.6 −17.8 −17.6 −17.0 −17.0 −16.8 −15.6 −15.9 −16.0 −14.3 −13.8 −18.1. SFX events/s 5 9 7 13 4 23 11 14 20 7 23 14 21.
- flash_check 0 flashes. Seam 0.582.
- Frames read: 0.5, 1.7, 8.7, 10.2, 10.3, 11.55, 11.85, 11.9, 13.2; Bolt's chair crops (Fast) at 0.5 / 1.6 / 12.8 s.
- First render showed "BOLT WINS!" at the cadence while her castle still read 100 % for 0.3 s; fixed (banners + HUD use the moment her castle drops below 2 %).

## Doubts
- Second 4 is quiet (4 SFX events): small waves, both castles untouched.
- The castle falls as a column of grains (the model's collapse), not a rigid tip-over.
- The chair is mint/cream (Bolt's colours); it reads as a deck chair at Full HD, small on a phone.

Delivered `<VIDEOS_DIR>\MochiAndBolt\review\batch68\sandcastle_wave2_v2.mp4`. Owner review: pending.
