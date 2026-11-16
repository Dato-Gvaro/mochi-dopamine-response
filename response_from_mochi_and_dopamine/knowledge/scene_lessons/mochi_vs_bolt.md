# mochi_vs_bolt
- Rule: each wall bounce makes the bouncer x1.045 faster (cap 1750 px/s); on collision the FASTER one deals damage = speed/120 (rounded).
- Collisions are equal-mass elastic, so a hit hands speed across; this keeps the lead swinging (without it the faster fighter runs away).
- Seed search (`--search N`) scores lead changes, low winner HP, 24-38 s fight, climbing hit rate. FR 92, HP 100.
- seed 77: Bolt wins on 2 HP after 20 hits, 25.2 s fight; hits/5s 3, 2, 4, 5, 6; walls/5s 9, 11, 13, 20, 34.
- KO: winner grins/hops + confetti + "BOLT WINS!", loser dizzy (X eyes, stars), 2.2 s hold; reset 1.5 s glide home + HP refill.
- Sound: hit = eine_kleine note + squash (pop on KO); wall = bounce; victory arpeggio. peak_db -6 (sparse impulses peaked -1.6 dBFS at -4).
- Shipped sample: 28.93 s, -14.0 LUFS, peak -2.5 dBFS, flash_check PASS. Theme lilac.
- Args: --seed, --dmgdiv, --search, --label, --cap, --melody.
- Owner review 2026-10-03: Interesting, but at the crash you can't tell who is attacking.
