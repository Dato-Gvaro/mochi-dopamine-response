# Melody bank audit: `lib/audio.py` `MELODIES` (2026-10-17)

Read-only audit. `lib/audio.py` was NOT edited. Each entry was compared with a score of
the piece by pitch-class sequence, allowing one consistent transposition or octave shift.
Grace notes and ornaments were dropped, and octave doublings were collapsed to the melody
voice. Scratch files and tools are in
`<local path removed>`
(`tools/dump.py` reads MIDI, `tools/mxl.py` and `tools/meas.py` read MusicXML, and
`tools/diff.py` diffs the bank against the corrections).

Verdicts: **CORRECT** · **MINOR** (1-3 notes wrong, missing or extra, contour intact) ·
**WRONG** (wrong phrase or many wrong notes) · **UNVERIFIABLE** (no source found).
"ref-check" means the tune was checked against its standard published form from memory,
with no score file diffed. These are only the simplest trad tunes.

## Scheduled clips first

| entry | clip / upload | verdict |
|---|---|---|
| fur_elise | press_split2, Oct 16 | **CORRECT** |
| turkish_march | double_bounce3, Oct 17 | **WRONG** (last 5 of 19 notes) |
| habanera | lava_ice2, Oct 18 | **WRONG** |
| mountain_king | halloween_switch2, Oct 31 | **WRONG** |
| spring_vivaldi | halloween_switch2, Oct 31 | **WRONG** |

## Full table

| entry | piece | source | verdict | diff (bank → score) | corrected list (bank register) |
|---|---|---|---|---|---|
| fur_elise | Beethoven WoO 59, bars 1-8 (first ending), RH | [Mutopia 931 MIDI](https://www.mutopiaproject.org/ftp/BeethovenLv/WoO59/fur_Elise_WoO59/fur_Elise_WoO59.mid) | **CORRECT** | 35/35 notes identical to the RH top voice | (no change) |
| turkish_march | Mozart K.331 iii, bars 1-8 | [Mutopia KV331 MIDI](https://www.mutopiaproject.org/ftp/MozartWA/KV331/KV331_3_RondoAllaTurca/KV331_3_RondoAllaTurca.mid) | **WRONG** | notes 1-14 correct (B A G# A C, D C B C E, F E D# E). Tail `81,72,74,76,72` is invented. The score continues B5 A G# A B A G# A C6 | `71,69,68,69,72, 74,72,71,72,76, 77,76,75,76,83,81,80,81,83,81,80,81,84, 81,84, 83,81,79,81, 83,81,79,81, 83,81,79,78,76` (38, bars 1-8). Same-length 19-note drop-in: first 19 of this list. Shortest clean stop: first 23 (ends on C6) |
| habanera | Bizet, Carmen, "L'amour est un oiseau rebelle", bars 1-8 | Bizet's own piano-solo arrangement, MusicXML ([Sao Mai](https://saomaicenter.org/en/music-library/habanera-piano-solo-arr-georges-bizet-1)), cross-checked with a second edition ([Sao Mai](https://saomaicenter.org/en/music-library/habanera-carmen-6)) | **WRONG** | the chromatic descent D-C#-C-B-Bb-A is right. The bank's rising `69,70,71,72,74` does not exist; the real line goes on A-G#-G-F, G-F-E-F-G-F-E, and the repeated Cs are missing | `74,73,72,72,72,71,70,69,69,68,67,65, 67,65,64,65,67,65,64, 74,73,72,72,72,71,70,69,69,67,65,64, 65,64,62,64,65,64,62` (38). Phrase 1 alone = first 19 |
| mountain_king | Grieg Op. 46/4, theme bars 1-8 | Mutopia 1888 (cached `<SOUNDFONTS_DIR>\scores\grieg_mountain_king\`) | **WRONG** | two wrong notes in the first statement: `65,62,65` should be F-**C#**-F and `64,61,64` should be E-**C**-E. The second half ("up a minor 3rd", `62…67`) is not in Grieg; the phrase actually ends B C# D E F# D F# **B**, A F# D F#, A | `59,61,62,64,66,62,66, 65,61,65, 64,60,64, 59,61,62,64,66,62,66,71, 69,66,62,66, 69` (26, **same length as the bank**, so a drop-in that keeps halloween_switch2's `len(MK)` timing) |
| spring_vivaldi | Vivaldi RV 269 i, ritornello bars 1-3 | Mutopia 301 violin I (cached; same as `scenes/glass_tower.py` `SPRING`, -12) | **WRONG** | first 8 correct. `70,71,70,71` is invented: there is no A# anywhere, and the score repeats the bar (A G# G# G# F# E B B) and then cadences A G# A B A G# F# D# B | `64,68,68,68,66,64,71, 71,69,68,68,68,66,64,71, 71,69,68,69,71,69,68,66,63,59` (25). Same-length 12-note drop-in: `64,68,68,68,66,64,71,71,69,68,68,68` |
| ode_to_joy | Beethoven Sym. 9 iv theme, bars 1-8 | ref-check | **CORRECT** | standard 8-bar theme | (no change) |
| korobeiniki | Russian folk song, 2 phrases | ref-check + [Wikipedia folk score](https://en.wikipedia.org/wiki/Korobeiniki) | **CORRECT (variant)** | matches the widely known form (E-B-C-D-C-B-A…, i.e. the line people know from Tetris). Bar 3 has `71,71` (B B) where the Game Boy line has B. C; both readings exist. The folk notation on Wikipedia opens E-G#-B-G#-E instead, so the folk song has variants | (no change; optional `71,71`→`71` at index 12-13) |
| blue_danube | J. Strauss II Op. 314, waltz 1 theme | [Mutopia MIDI](https://www.mutopiaproject.org/ftp/StraussJJ/O314/blue_danube/blue_danube.mid) (in C, +2) | **WRONG** | the score has D D F# A A, then the octave "pings" A' A', F#' F#'. The bank has D F# A A A B B A F# F# (invented B-B), the second phrase never turns to G' G', and the third phrase (C# C# E B B…) is missing | `62,62,66,69,69,81,81,78,78, 62,62,66,69,69,81,81,79,79, 61,61,64,71,71,83,83,79,79, 61,61,64,71,71,83,83,78,78` (36; the pings are an octave up, as in the score) |
| entertainer | Joplin, A strain bars 1-8 | Mutopia (cached; `scenes/snake_perfect.py` `LEAD`) | **WRONG** | first 8 (pickup + bounce) correct. `60,62,64,67…` and `62,62,62,64,65…` are invented. The score has C D D# E C D E B D C, then the second half A G F# A C E D C A D | `62,63,64,72,64,72,64,72, 72,74,75,76,72,74,76,71,74,72, 62,63,64,72,64,72,64,72, 69,67,66,69,72,76,74,72,69,74` (36 = LEAD onsets 0-35) |
| twinkle | "Ah! vous dirai-je, maman" / K.265 theme | ref-check (K.265 bass in [Mutopia MIDI](https://www.mutopiaproject.org/ftp/MozartWA/KV265/guitar-duo-complete/guitar-duo-complete.mid) fits) | **CORRECT** | standard | (no change) |
| when_the_saints | trad. spiritual | ref-check | **MINOR** | three CEFG calls + E C E D are right. The final `60` is extra: phrase 3 ends on D | drop the last note (16 notes), or play the full tune: `60,64,65,67, 60,64,65,67, 60,64,65,67,64,60,64,62, 64,64,62,60,60,64,67,67,65, 64,65,67,64,60,62,60` (32) |
| pachelbel_canon | Pachelbel, violin I bars 3-6 | [Mutopia, Canon per 3 Violini e Basso](https://www.mutopiaproject.org/ftp/PachelbelJ/Canon_per_3_Violini_e_Basso/Canon_per_3_Violini_e_Basso-mids.zip) (+ [CanonInD.mid](https://www.mutopiaproject.org/ftp/PachelbelJ/CanonInD/CanonInD.mid)) | **MINOR** | the last 2 notes should be G-F#-**G-E**, not G-F#-E-F# | `66,64,62,61,59,57,59,61,62,61,59,57,55,54,55,52` |
| greensleeves | trad. English | [Mutopia accordion MIDI](https://www.mutopiaproject.org/ftp/Traditional/GreensleevesAcc/GreensleevesAcc.mid) | **CORRECT** | 16/16 (an excerpt that stops before B G# E) | (no change) |
| la_cucaracha | trad. Mexican | ref-check | **MINOR** | "ya no puede caminar" is F F E E D D C; the bank collapses it to F E D C (3 notes missing) | `60,60,60,65,69,60,60,60,65,69,65,65,64,64,62,62,60` |
| eine_kleine | Mozart K.525 i, bars 1-4 | [Mutopia MIDI](https://www.mutopiaproject.org/ftp/MozartWA/KV525/eine-kleine-nachtmusik-mvt1/eine-kleine-nachtmusik-mvt1.mid) | **WRONG** | bar 2 is missing the D-G (G D G B D); the answer is C A C A C A F# A D, but the bank has an invented D A D A D F# A D | `67,62,67,62,67,62,67,71,74, 72,69,72,69,72,69,66,69,62` (18) |
| jingle_bells | Pierpont, chorus | ref-check | **MINOR** | two notes missing in bars 6-8: "…ride in a one-horse open sleigh" = F E E E **E** E D D E **D** G | `64,64,64,64,64,64,64,67,60,62,64, 65,65,65,65,65,64,64,64,64,64,62,62,64,62,67` |
| frere_jacques | trad. | ref-check | **CORRECT** | | (no change) |
| row_your_boat | trad. | ref-check | **CORRECT** | | (no change) |
| mary_lamb | trad. | ref-check | **CORRECT** | | (no change) |
| london_bridge | trad. | ref-check | **CORRECT** | | (no change) |
| beethoven_5 | Beethoven Op. 67 i, bars 1-5 | [Mutopia MIDI](https://www.mutopiaproject.org/ftp/BeethovenLv/O67/Symphony5_1/Symphony5_1.mid) | **CORRECT** | G G G Eb, F F F D exact. The bank plays it twice (Beethoven moves on to Eb-C, Ab-G…), so it is just an 8-note loop | (no change) |
| joy_to_world | tune "Antioch" (L. Mason, after Handel) | [Mutopia hymn MIDI](https://www.mutopiaproject.org/ftp/HandelGF/antioch/antioch.mid) (in D, -2) | **MINOR** | phrase 2 should be G **A A B B** C, not G G A A B C (2 notes) | `72,71,69,67,65,64,62,60,67,69,69,71,71,72` |
| silent_night | Gruber, phrases 1-4 | [Mutopia stille-orig](https://www.mutopiaproject.org/ftp/GruberFX/stille-orig/stille-orig.mid) (in D, -2) | **CORRECT** | the bank is the standard hymnal form. Gruber's 1816 original adds neighbour notes (E D# E C# / D C# D A) at "Alles schläft / einsam wacht" | (no change) |
| brahms_lullaby | Brahms Op. 49/4 | [Mutopia Wiegenlied](https://www.mutopiaproject.org/ftp/BrahmsJ/O49/Wiegenlied/Wiegenlied-mids.zip) (in Eb, -3) | **CORRECT** | 13/13 | (no change) |
| bach_toccata | Bach BWV 565, bars 1-2 | Mutopia 1780 (cached; = `scenes/last_brick.py` source) | **WRONG** | only the opening A G A is right. Bach answers it with G F E D C# D, then A3 (G A) E F C# D. The bank's descending D-minor scale `62,60,58,57,55,53,52,50` is not in the piece | `69,67,69,67,65,64,62,61,62, 57,55,57,52,53,49,50` (16; mordents realised A-G-A as in last_brick. The third statement an octave lower, `45,43,45,43,41,40,38,37,38`, is optional and drops to C#2) |
| bridal_chorus | Wagner, Lohengrin "Treulich geführt", bars 1-8 | IMSLP MIDI PMLP03617 (Gouin), [Lohengrin page](https://imslp.org/wiki/Lohengrin,_WWV_75_(Wagner,_Richard)) (in Bb, -5) | **WRONG** | first 4 right (C F F F). The bank then has E F G F F G A A G F G C; the score has C G E F, C F Bb Bb A G F E F G, then C F F F, C G E F, C F A C A F D C Bb A G F | `60,65,65,65, 60,67,64,65, 60,65,70,70,69,67,65,64,65,67, 60,65,65,65, 60,67,64,65, 60,65,69,72,69,65,62,60,58,57,55,53` (38) |
| danny_boy | trad. Irish "Londonderry Air" (Petrie, 1855) | modern engraving, MusicXML ([Sao Mai](https://saomaicenter.org/en/music-library/traditional-music-danny-boy)) | **WRONG** | the bank (C F G A C B A F G A F D C) is not the air. The air is E F G \| A G A D' C' A \| G F D … | `64,65,67, 69,67,69,74,72,69, 67,65,62,65,69,70, 72,74,72,69,65,69, 67, 64,65,67, 69,67,69,74,72,69, 67,65,62,64,65,67, 69,70,69,67,65,67, 65` (44, phrases 1-2, F major) |
| auld_lang_syne | trad. Scottish | [Mutopia Horetzky No. 31](https://www.mutopiaproject.org/ftp/HoretzkyF/horetzky31/horetzky31.mid) (in D, -9) + [Wikipedia score](https://en.wikipedia.org/wiki/Auld_Lang_Syne) | **CORRECT** | 14/14 | (no change) |
| william_tell | Rossini, Overture finale (gallop) | MusicXML, flute part ([Sao Mai "Lone Ranger"](https://saomaicenter.org/en/music-library/lone-ranger-0)) (in E, -4) | **WRONG** | the call is 8 Gs then C **D** E; the bank has 7 Gs then C E with no D, and its second phrase is a plain repeat. The score answers G G G C E E D B G and climbs to G' F E D | `67,67,67,67,67,67,67,67,72,74,76, 67,67,67,67,67,72,76,76,74,71,67, 67,67,67,67,67,67,67,67,72,74,76,72,76,79,77,76,74,72,76,72` (42) |
| jolly_good_fellow | trad. "Malbrough" | [Wikipedia score](https://en.wikipedia.org/wiki/For_He%27s_a_Jolly_Good_Fellow) (in F, -5) | **WRONG** | the bank (C F F F G F E C C D E D C) is a different tune shape. The score has G(pickup) C E E E D E F E E D D D C D E C C … | `60,64,64,64,62,64,65,64,64,62,62,62,60,62,64,60,60,64,64,64,62,64,65,69,69,67,67,65,62,60` (30) |
| funeral_march | Chopin Op. 35 iii, bars 1-8 RH | piano MusicXML ([Sao Mai](https://saomaicenter.org/en/music-library/marche-funebre-chopin-0)) + 2 band arrangements (agree) | **MINOR** | pitches and order are right; the repeat counts are off. The score has 4 Bbs (not 5) before Db C C, 4 Bbs (not 2) after it, Db×4 at the end of phrase 2 (not 2), and the Bb-Ab-Gb-F-F-Db tail twice | `58,58,58,58,61,60,60,58,58,58,58, 61,61,61,61,65,63,63,61,61,61,61, 70,68,66,65,65,61, 70,68,66,65,65,61` (34) |
| ievan_polkka | trad. Finnish, A phrase | [Flute Tunes MIDI](https://www.flutetunes.com/tunes.php?id=341) (modern transcription; no PD print found) | **CORRECT** | 20/20 against that transcription | (no change) |

## Totals

32 entries: 13 CORRECT (+1 CORRECT-variant: korobeiniki) · 6 MINOR · 12 WRONG ·
0 UNVERIFIABLE (ievan_polkka was checked against a modern transcription only).
`MELODIES_BENCH` was not audited.

## Impact notes

- Clips already in `final/` keep the notes they were rendered with. Fixing the bank only
  matters for re-renders or new clips.
- `halloween_switch2` times its finale from `len(MK)` and `len(SPRING)`. The mountain_king
  fix is the same length (26). For spring_vivaldi use the 12-note drop-in to keep timing.
- `double_bounce3` and `lava_ice2` cycle the list through `MelodyWalker`. A longer
  corrected list changes which note lands on the last event, so check the cadence
  after a swap.
- The bank comment "A# where the score has A" (spring) is confirmed: there is no A# in
  bars 1-10.
