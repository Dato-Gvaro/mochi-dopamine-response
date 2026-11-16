# factorial_tank — "Mochi DOUBLES it, Bolt goes FACTORIAL" / "whose tank BURSTS?"

- Brief: docs/BRIEF_mochi_1113.md clip 4. Sequel to growth_race3 (18K). New file `scenes/factorial_tank.py`; growth_race3 untouched. ONE change: Bolt uses n!.
- Mochi = 2^n, Bolt = n!, n = 0..7, both start with 1 ball (2^0 = 0! = 1). Exact counts, 1 ball = 1 ball:
  n1 2/1 · n2 4/2 · n3 8/6 · **n4 16/24 (LEAD CHANGE, 2.75 s, at 10 vs 11 mid-pour)** · n5 32/120 · n6 64/720 · n7 128/**5,040**.
- Tank holds exactly 1,000 (hex rows of 20, 50 rows, ball r 8.5). FULL line "FULL 1,000" visible at frame 0.
- n = 7: Bolt's first 280 fill to 1,000 (FULL 9.33 s), the next 600 overflow both rims (accelerating), 9 cracks spread, BURST 11.18 s on the Can-can's ff downbeat; the tank's 1,000 blow out, the last 3,440 pour through the broken tank; counter ends exactly 5,040 (12.9 s).
- HUD: caption 2 lines; WHY line "n! multiplies by a BIGGER number every round" from the lead change; "n = k"; pops "x2" / "x k" (x1 = no change) under the hoppers; labels "DOUBLES 2^k" / "FACTORIAL k!"; counts (gold = leader).
- Sound: growth_race3's Can-can (Offenbach 1858, PD; by-eye reading of the 1860 Heugel score), rounds on bars, accelerando 150 -> 200 bpm; marble clicks per landing group; crack ticks; 3 glass breaks + tutti at the burst.
- Burst balls fade out past the table edge (y FLOOR+8..+54) so nothing covers the counters.
- Maths: n! > 2^n for every n >= 4 ((n+1)! = (n+1)·n! > 2·2^n); Stirling n! ~ sqrt(2 pi n)(n/e)^n outgrows any c^n.
- Doubts: frame 0-3 s is sparse (1-16 balls in a 1,000 tank), the honest exponential, same as growth_race3; the burst is a dramatisation (the true part: 5,040 > 1,000).

## Commands
- `NF_SCALE=1.0 NF_FAST=1 python scenes/factorial_tank.py --still --frame 0,400,700 --label x`
- `NF_SCALE=1.0 python scenes/factorial_tank.py --label fhd` (~3 min)
