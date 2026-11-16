# Growth research: Shorts to subscribers, views and long-form (2026-10-31)

**How this was made.** Web search plus official YouTube pages (Help Center, YouTube blog, Google blog, Creator Insider). Transcripts and top comments of 10 videos were read (YouTube transcript panel and yt-dlp; comments use the "Top" sort, 40-80 per video).

**Evidence grades:**
- **A** = official YouTube (Help, blog, Creator Insider, YouTube staff).
- **B** = analysts or creators showing real data.
- **C** = vendor or SEO blogs.
- **D** = anecdotes and comments.

Our numbers come from `research/data_2026-10-30.md`.

## 0. The finding that changes the plan

**YPP rules change on 1 Feb 2027 (A):**
- **Entry for new applicants:** 1,000 subs plus either **20M qualified Shorts views in 90 d** or **8,000 qualified long-form hours in 365 d**. Today it is 10M or 4,000.
- **Shorts pay for members:** members keep their status, but Shorts pool pay needs **10M qualified Shorts views per rolling 90 d**, re-checked monthly. Below that, a channel earns from long-form only.
- **What counts:**
  - A qualified Shorts view = an **engaged view on a public Short**. Loops, ads and image posts are excluded.
  - **Shorts watch time never counts toward hours.** Hours come only from public long-form and archived lives.
- **Terms deadline:** new terms must be accepted by 31 Jan 2027.
- **Unconfirmed:** whether an application filed before 1 Feb is judged on the old bar. No source says.

**Mochi & Bolt against the gates** (last 28 d: 552.9K views, 267.9K engaged, +190 subs, 274 total):

| Gate | Now | Needed | Gap |
|---|---|---|---|
| Subscribers | 274; +6.8/day | 1,000 | ~904 by 31 Jan at the current rate, ~1,000 by mid-Feb. Needs a ~1.15x lift. |
| Qualified Shorts views (old bar) | ~0.86M per 90 d (9.6K engaged/day) | 10M per 90 d (111K/day) | **11.6x short** |
| Qualified Shorts views (new bar) | same | 20M per 90 d | 23x short |
| Long-form hours (old bar, by 31 Jan) | ~0 (first compilation live 30 Oct) | 4,000 | **43 h/day from 1 Nov** |
| Long-form hours (new bar) | ~0 | 8,000 per 365 d | **22 h/day, sustained** |

Hours earned from today count toward both bars.

**What this means:**
- **Subscribers are not the binding gate; qualified views and long-form hours are.**
- **Our sub rate is normal for entertainment Shorts:**
  - Ours: 3.4 subs per 10K public views, 7.1 per 10K engaged.
  - NefiSims: 4.8 per 10K public views (22.8K subs on 47M views).
  - Advice and utility channels are higher: Galloway's 2023 average was ~17 per 10K, vidIQ's own channel ~20 per 10K.
- **Long-form is the lever on every gate:**
  - It converts **1.3x** (Galloway) to **4.7x** (vidIQ) more subs per view than Shorts.
  - Its hours are the only realistic YPP route.
  - From Feb 2027, Shorts pay is ~0 for channels below 10M per 90 d anyway.
- **These features are YPP-only, which is one more reason to get in:** Shorts Series, custom Shorts thumbnails, Hype and the Shorts bonus pilot.

## 1. Top 10 actions (ranked)

The effort figures are owner minutes. Agents do the building.

### 1. Make long-form hours the #1 KPI; ship ≥1 long-form a week (THIS WEEK, then ongoing)
- **Do:**
  - Publish on M&B weekly, alternating an 8-10 min compilation and a ~1 h ambient cut. Each gets chapters and a search-phrase title.
  - Track qualified long-form hours per day against two lines: 43 h/day (old bar) and 22 h/day (new bar).
  - On **6 Nov**, read Compilation 1's hours per day at day 7, then decide whether 31 Jan is realistic.
  - Build long-forms as one complete arc ("every round from 1 to 1,000,000"), not 26 clips glued together.
- **Why:**
  - The rules in section 0 (A).
  - vidIQ's own channel: long-form converts 4.7x better than Shorts (B).
  - Galloway 2026 (B): TV is now >50% of his clients' views, up from ~23% in 2021. Average long-form length is up 51% since 2020. "Every ___" comprehensive formats are working now.
  - Beaupré (A): TV viewers don't want to choose again every 5-10 minutes, which is why series and long videos win there.
  - Sherman (A): long-form made for its purpose beats one that is chopped up or glued together from Shorts.
- **Confidence:** high that this is the lever; medium that 4,000 h by 31 Jan is reachable.
- **Owner effort:** ~15 min per long-form upload.

### 2. Point every Short's related video at the long-form that matches it; fix the top 20 Shorts today (THIS WEEK)
- **Do:**
  - Today, re-point the related video of the 20 most-viewed M&B Shorts (press_split2, press_split4, press_squeeze, sand_rise3, cradle_showdown, foam_overflow…) to **Compilation 1**. It opens on the press saga at 0:00, so the click pays off at once.
  - From now on: press Shorts link to Compilation 1 (later to a press-only long-form); all other Shorts link to the newest compilation.
  - This replaces the current upload-skill rule ("the Short published directly before").
  - DopamineEXE has no long-form yet, so link its Shorts to its best Short (Sierpinski) for now.
- **Why:**
  - YouTube's July 2026 guidance (A) calls the related video the main bridge from Shorts to long-form. It says to match why the viewer watched and to make the first seconds of the long video confirm the click.
  - It is the only clickable path: links in Shorts descriptions and comments have been unclickable since Aug 2023 (A).
- **Caveats:**
  - YouTube reports no click data for the link.
  - Commenters on YouTube's own video say almost nobody notices the link. See action 8.
- **Confidence:** medium.
- **Owner effort:** ~20 min once, then ~1 min per Short (already part of the upload form).

### 3. Measure subs per Short and make more of the formats that convert (THIS WEEK, agent-only)
- **Do:**
  - Export per-Short subscribers and engaged views (`youtube-analytics` skill).
  - Rank Shorts by **subs per 10K engaged views** and compare format families: ×N split/overflow, everyday-myth duels, fractal loops, character duels.
  - Open Studio → Analytics → See more → **Subscription source**. Note the share from "Your YouTube channel" and the losses on the "Subscriptions feed" row, which YouTube says shows how upload frequency affects subscriber count.
- **Why:**
  - Conversion depends on the format. press_split2 made +24 subs on 38.4K views on day 1 (6.3 per 10K), about twice our average.
  - Beaupré (A): the subscribe action is weaker than people think. Even on a channel's best videos, ~90% of its subscribers don't choose to watch.
  - A family that converts twice as well is worth more than one more view hit.
- **Confidence:** high (it is measurement).
- **Owner effort:** 0.

### 4. Run the press franchise as a named weekly series, one nameable change per episode (THIS WEEK)
- **Do:**
  - One name (e.g. "THE PRESS").
  - One playlist with every press Short in order, placed first on the channel Home.
  - The episode number in the title ("Press #6: …").
  - About one episode a week, each with ONE change a viewer could name (new machine, new material, new rule, new winner).
  - Convert the playlist to a **Shorts Series** once we are in YPP. Series launched 23 Sep 2026 and are YPP-only (A).
- **Why:**
  - The press franchise drives most of our views, and the rematch still adds ~15K views a day.
  - Galloway (B): double down on a winning format quickly, because copycats will take it if you don't.
  - Beaupré (A): people subscribe to what they expect next. YouTube is pushing shows and series.
- **Policy guard (A):**
  - YouTube's repetitive-content rules allow a series that follows characters across episodes.
  - They ban "characters put in the same situation over and over again with the same outcome".
  - So every episode needs a new situation, and sometimes a different winner.
- **Conflict (one line):** the owner's 2026-10-17 rule allows one sequel of a winner, a week or more apart. This proposes a standing weekly slot. The owner decides.
- **Confidence:** medium-high for views, medium for subs.
- **Owner effort:** 10 min once (playlist + Home section).

### 5. Decide the two-channel split (THIS WEEK, owner decision)
- **Options:**
  - **(a)** Fold DopamineEXE's best formats (Sierpinski-style "Every X … until Y") into M&B as a second named series. Cut DopamineEXE to ≤1 Short a day, or pause it.
  - **(b)** Keep both channels and run test T5 (cross-channel collab tag).
- **Why:**
  - Beaupré (A): match channels to audiences. Use one channel when the same people would watch both.
  - M&B's best content (the press) is already character-free, the same kind as DopamineEXE.
  - Each channel has to clear 1,000 subs plus the views or hours gate on its own. DopamineEXE has ~10 subs, about 1% of the way.
  - Option (a) frees 1-2 manual uploads a day for long-form.
- **Confidence:** medium (an inference from official guidance and our data).
- **Owner effort:** the decision itself; saves ~10-20 min a day.

### 6. Make the channel page a subscribe page (THIS WEEK)
- **Do** (Studio → Customization):
  - A one-line promise in the banner and description, e.g. "physics duels where the numbers explode. new one every day".
  - Home sections in this order: THE PRESS playlist, latest long-form, popular Shorts.
  - Channel trailer (non-subscribers) = Compilation 1. Featured video (returning subscribers) = newest long-form.
  - Pick a payoff frame as the Short's cover wherever Studio offers a frame choice. Custom Shorts thumbnails are YPP-only (July 2026).
- **Why:**
  - Channel pages bring 2.8% of our views, and that is where a visitor decides what they would be subscribing to.
  - The Shorts grid shows covers; feed viewers mostly don't (Sherman, A).
  - Hoyos: covers make the channel look professional.
  - Evidence is practitioner-grade.
- **Measure:** Subscription source → "Your YouTube channel", 28 d before vs after.
- **Confidence:** low-medium.
- **Owner effort:** 30-45 min once.

### 7. Pinned comment: one side-picking question plus a pointer to the link (ongoing, already allowed)
- **Format:** a question that picks a side, then "full 10 min version is the link under the channel name". Keep the owner's tone rules: casual, lowercase, no AI polish. No URLs, since they are not clickable in Shorts.
- **Why:**
  - Comments are only a partial ranking signal (Beaupré, A).
  - Galloway's 2023 data found no strong link between engagement and views (B).
  - The value is returning viewers and ideas for reply videos.
- **Confidence:** low for subs.
- **Owner effort:** none extra.

### 8. Test a loop-safe on-screen pointer to the related link before rolling it out (TEST T2)
- **What YouTube advises (A):** a spoken call to action that points at the link, or a picture of the target's thumbnail.
- **Our constraints:** no voice-over, and every video must loop cleanly.
- **Plan:** run T2 and roll out only if % viewed holds.
- **Confidence:** low until tested.
- **Owner effort:** 0 (agent post-pass).

### 9. Keep the weekly reply-with-a-Short (ongoing)
- **Why:**
  - Sherman (A) presents reply-with-a-Short as the way Shorts build community; whole channels now run on it.
  - The parent channel's best sub rate came from reply videos.
- **Do:** prefer comments that ask for a variant ("do it with 1M balls"). Each one becomes an episode with a nameable change.
- **Confidence:** medium.
- **Owner effort:** ~10 min a week.

### 10. Stop spending time on myths (now)
- No more posting-time experiments.
- Don't raise volume.
- Never delete and re-upload a flop.
- Never untick "notify subscribers".
- No hashtag tuning.
- Full list in section 3.
- **Confidence:** high (official).
- **Effort:** saves time.

**Already right, keep doing:**
- Mid-action frame 0 and a stayed-to-watch rate of ≥70%. Galloway: hits sit at 70-90% viewed; under 40% rarely passes 10K views. We are at 69.7%.
- Loops.
- Side-picking titles.
- US prime-time slots.
- Pinned comments.
- The related link, now with a better target (action 2).

**This week, owner total ≈ 1.5-2 h:**
- Re-point 20 related links: 20 min.
- Press playlist and Home layout: 45 min.
- Decide the two-channel question.
- Upload the next long-form: 15 min.

## 2. Tests to run (one variable each)

**How to read every test:**
- **Baseline:** the last 28 d.
- **Size:** ≥10 Shorts per arm, matched by format family.
- **When:** read at 48 h and 7 d (Studio → Advanced mode → per-video export).
- **Primary metric:** subs per 10K engaged views.
- **Guard metrics:**
  - Stayed to watch.
  - Average % viewed.
  - Engaged/views ratio (loops show up as public views without engaged views).
- **Monthly:** check the Subscription source "Subscriptions feed" row for unsubscribes tied to upload volume.

| # | Test | Arms | Measure | Decide |
|---|---|---|---|---|
| T1 | Related-link target | A = matching long-form · B = the franchise's best Short (press_split2). Alternate by slot, 2 weeks. | Long-form views by traffic source: watch which row moves (Shorts feed, Other YouTube features, Channel pages), since the related-link source label isn't documented. Also subs per 10K engaged on the Shorts, and channel subs per day. | Keep A unless B lifts subs per 10K by ≥20% without losing long-form views. |
| T2 | Loop-safe pointer | A = none · B = a small "FULL VERSION ↓" chip at the payoff that fades out before the loop seam. It sits inside x 0.10-0.84w, about 0.80h, pointing at the link. | % viewed and stayed (guards); long-form views from Shorts; subs per 10K engaged. | Kill it if % viewed drops more than 5 points. Roll out if long-form views from Shorts rise and subs per 10K hold. |
| T3 | Series branding | Franchise episodes with the series name, episode number and playlist, vs the earlier unbranded press episodes (historical, weak). Better: brand alternate new episodes. | Subs per 10K engaged; returning viewers (Audience tab); playlist views. | Brand the whole franchise if subs per 10K is ≥15% higher. |
| T4 | Long-form format | 9-10 min compilation vs ~1 h ambient vs a purpose-built single-franchise ladder (8-12 min, "every round"). | Qualified hours per day at day 7 and day 28; AVD; traffic mix (Browse, Suggested, Shorts); subs per 1K views. | Make most of whichever gives the most hours per day per build-hour. |
| T5 | Cross-channel collab tag | Tag DopamineEXE as collaborator on 5 M&B Shorts. First check that Studio offers it (Details → Audience → Show more → Collaboration; availability for small channels is unverified). | DopamineEXE subs and views per day; M&B stayed-to-watch (guard). | Keep it if DopamineEXE gains subs and M&B is unchanged. |
| T6 | Vertical live (optional, low confidence) | One 2-3 h vertical live of a live-generated sim with a running counter, not a looped file. | Viewers arriving from the Shorts feed (A: vertical lives surface there), subs during the stream, archived hours (archived lives count as qualified hours, A). | Do once only, and only if the owner wants. Repetitive-content risk; needs OBS and live enabled. |

## 3. Myths / ignore

| Claim | Verdict | Source |
|---|---|---|
| Posting time decides reach | No. Time of day isn't optimised for; freshness matters only for news. Our slots are set; stop testing. | Sherman, Creator Insider 2023 (A) |
| Posting more per day unlocks the algorithm | No: there is no upload-count threshold. YouTube says to put that effort into fewer, better videos. | Sherman 2023 (A) |
| Delete and re-upload Shorts that flop | No. It may be treated as spam. The Oct 2026 originality update also cuts reach for re-uploads. | Sherman 2023; Ritchie Oct 2026 (A) |
| Hashtags drive distribution | Optional, effect depends on the topic. Keep our 3; don't tune them. | Sherman 2023 (A) |
| A slow first hour or a weak subscriber reaction kills a video; untick "notify subscribers" | No. New viewers are reached within the first hour, audiences are scored separately, and YouTube advises against unticking. | Beaupré, Sep 2026 (A) |
| Subscribers = views | No. Even on a channel's best videos, ~90% of subscribers don't choose to watch, and 95% of our views come from the feed. Subs are a YPP gate, not the view engine. | Beaupré 2026 (A); our data |
| Shorts kill long-form | Not how YouTube describes it: separate watch histories since 2022, and Shorts aren't seen as cannibalising. The real risk is a muddled identity without a content bridge. | vidIQ 2022 (B); Sherman (A); vidIQ 2026 data (B) |
| Comment and like bait boosts Shorts reach | Weak: no strong link to performance in 2023 data. Comments are a partial signal, and disabled comments aren't penalised. | Galloway 2023 (B); Beaupré (A) |
| Shorts must be 50-60 s | A 2023 correlation with selection bias. Our short loops get the highest % viewed. Keep "length = honest rungs". | Galloway 2023 (B); our data |
| Shorts watch time counts toward 4,000 h | No, never. | YouTube blog, 12 Aug 2026 (A) |
| Shorts covers matter for feed reach | Mostly unseen in the feed; they matter for the channel grid and search only. | Sherman 2023 (A) |
| Image posts in the Shorts feed will grow us | Still a limited test, and image posts are excluded from qualified Shorts views. Not a priority. | 9to5Google Apr 2026; YouTube blog Aug 2026 (A) |
| Hype, Shorts Series, custom Shorts covers, Shorts bonus | All YPP-only (the bonus pilot is also limited to US/UK/DE/BR/JP/KR). Ignore until we are in. | YouTube Help; Creator Insider Oct 2026 (A) |
| Unsourced vendor numbers | Ignore all of these: "series convert 67% better"; "cliffhanger Shorts convert 3-5x"; "5 Shorts a week = 47% faster growth (Creator Insider)", which isn't traceable to YouTube; "16.9 subs per 10K = 1.69%", a maths error (it is 0.169%). | C blogs |
| "Seed every upload with bought views or likes" (a top comment on the Marcus Jones video) | Fake engagement breaks YouTube policy and would damage the qualified-views gate. Never. | (D) |
| Copy a viral script structure with AI | In Isaac's own 7-day experiment, copying formulas didn't get him there. The Oct 2026 update also favours original work. | Isaac 2026 (D); Ritchie (A) |
| A re-skin is a new episode | Repetitive-content policy: the substance of each video must vary. Keep the nameable-change rule. | YouTube Help 1311392 (A) |

## 4. Best videos found and the most useful top-comment tips

### 1. YouTube Algorithm 2026 – What Creators Need to Know (Creator Insider: Rene Ritchie with Todd Beaupré)
- **Stats:** 2026-09-01 · 150K views · 3.6K likes · grade A.
- **Takeaways:**
  - Ranking is per viewer.
  - New viewers are reached within the first hour.
  - The subscribed audience skips ~90% of uploads.
  - Match channels to audiences.
  - Don't untick notifications.
  - TV favours series.
  - Your best video is not the benchmark for the next one.
- **Top-comment tips:**
  - Many creators report that subscriber notifications don't arrive (one says 7 of 21.9K subscribers were notified), so don't plan around notifications.
  - Otherwise few practical tips.

### 2. How to Grow Long-form with YouTube Shorts (Creator Insider)
- **Stats:** 2026-07-14 · 17K views · grade A.
- **Takeaways:**
  - The related link is the bridge.
  - Match it to the viewer's intent.
  - Use a call to action that points at the link, or show the target's thumbnail.
  - Reward the click in the first seconds.
  - Vertical lives surface in the Shorts feed.
- **Top-comment tips:**
  - Several say the link is too subtle and nobody taps it unless told.
  - A music channel makes each Short complete on its own, links the full piece, and finds playlists help viewers binge.
  - Counterpoints (anecdotes): "Shorts subscribers don't watch long-form or unsubscribe"; "my long-form did better after I stopped Shorts".
  - Creators ask for related-link click analytics; none exist.

### 3. YouTube Shorts Algorithm – Explained! (Creator Insider: Todd Sherman, Shorts product lead)
- **Stats:** 2023-08-23 · 185K views · grade A.
- **Takeaways:**
  - No posting-time effect.
  - No upload-count threshold.
  - Don't delete and repost.
  - Hashtags are optional.
  - A seed audience decides whether a Short grows or tapers.
  - Reply-with-a-Short builds community.
- **Top-comment tips:**
  - The most common complaint: views flatline after the first burst (the seed test failing).
  - With 264 likes: covers on the Shorts tab are brand recognition.

### 4. A deep conversation about Shorts with Jenny Hoyos and Todd Sherman (Creator Insider)
- **Stats:** 2024-12-09 · 140K views · 5.4K likes · grade A/B.
- **Takeaways:**
  - Deliberately build in rewatchability.
  - YouTube weighs "valued" watch time, not just minutes.
  - A long-form is not a long Short: purpose-made beats chopped or glued.
  - Covers make the channel look professional.
- **Top-comment tips:** mostly thanks. One notes the 3-minute Shorts limit wasn't discussed.

### 5. The Fastest Way to 1,000 Subs in 2026 (vidIQ)
- **Stats:** 2026-05-04 · 167K views · 5.9K likes · grade B.
- **Data:**
  - 200K channels created in 2025 that reached 1K subs. Median uploads to 1K: long-form 46, Shorts-only 90, mixed without a content bridge 108.
  - vidIQ's own channel: 505 Shorts views per sub vs 106 long-form views per sub (4.7x).
  - Caveat: survivorship (only channels that reached 1K).
- **Top-comment tips:**
  - One creator reached 1K with 22 uploads, all Shorts.
  - Another reached 500 subs with 98% from Shorts.
  - Another moved Shorts to a second channel and their long videos improved.
  - Another posts long-form twice a week plus a Short cut from it the next day.

### 6. The New Rules of YouTube (2027) (Colin and Samir with Paddy Galloway)
- **Stats:** 2026-08-19 · 279K views · 5.7K likes · grade B.
- **Takeaways:**
  - TV is >50% of his clients' views.
  - Average long-form length is up 51% since 2020.
  - Channels are moving from formats to shows.
  - Returning viewers matter.
  - Milk your format before copycats do.
  - "Every ___" comprehensive formats feel complete.
  - He rates the long-form system as more refined than the Shorts one.
- **Top-comment tips:**
  - "The new shows feature makes episodic content even more viable."
  - Viewers skip videos with low view counts, so the public count matters socially.

### 7. I Studied 5,400 Shorts to CRACK the Algorithm (Marcus Jones, explaining the Galloway/Gileta data)
- **Stats:** 2023-06-09 · 716K views · 25K likes · grade B.
- **Takeaways:**
  - Viewed-vs-swiped under 40% rarely passes 10K views; hits sit at 70-90%.
  - Subs per 10K views: Shorts ~17, long-form ~22.
  - Shorts RPM ~$0.06.
  - Caveat: from before the 2025 view-count change, and correlational.
- **Top-comment tips:**
  - One creator got 80% of their subs from Shorts (100 → 750).
  - Another shortened their Shorts when viewers watched only 70%, and % viewed rose to 80%.
  - Ignore the comment promoting bought views.

### 8. Two Creator Insider updates
- **Videos:**
  - "Updates to Public View Counts & Engaged Views" (2026-08-21).
  - "Shorts Bonuses … Original Content" (2026-10-16).
- **Takeaways:**
  - The public view counter counts from the first frame since 24 Aug.
  - YPP and revenue use qualified (engaged) views.
  - The Shorts bonus pilot is YPP-only.
  - The originality update cuts reach for re-uploaders.
  - "Ask YouTube" search uses titles, descriptions and chapters, so long-form needs chapters.
- **Comments:** heavy creator pushback on the 10M threshold.

### Low value for us
- **Isaac, "I Blew Up a Shorts Channel in 7 Days" (702K):** entertainment. The only useful datapoint: fixing the hook and the payoff took one Short to 80% viewed and 96% retention.
- **Paddy Galloway, "How Beluga Gained 4M Subs" (2021, 6.9M):** recurring characters plus traffic from a bigger channel. Its audience skews young, which is a made-for-kids risk for us.

## 5. Sources

### Official (A)
- YouTube blog, qualified watch hours and Shorts views (12 Aug 2026): https://blog.youtube/news-and-events/youtube-monetization-qualified-watch-hours-shorts-views/
- Google blog, new ways to earn and YPP changes (Aug 2026): https://blog.google/intl/en-mena/product-updates/connect-communicate/new-opportunities-to-earn-and-changes-to-the-youtube-partner-program/
- YouTube Help, add a related video to Shorts: https://support.google.com/youtube/answer/14075157
- YouTube Help, where viewers clicked Subscribe (Subscription source): https://support.google.com/youtube/answer/9717879
- YouTube Help, YPP policies (repetitive and reused content): https://support.google.com/youtube/answer/1311392
- YouTube Help, Hype eligibility: https://support.google.com/youtube/answer/15509925
- Google blog, Made on YouTube 2026: https://blog.google/products-and-platforms/products/youtube/made-on-youtube-updates-2026/
- Creator Insider, YouTube Algorithm 2026 (Beaupré): https://www.youtube.com/watch?v=rHLjxrbXmmY
- Creator Insider, How to Grow Long-form with YouTube Shorts: https://www.youtube.com/watch?v=ywYL5uuFBNc
- Creator Insider, YouTube Shorts Algorithm Explained (Sherman): https://www.youtube.com/watch?v=n3jsYK_-aRU
- Creator Insider, Jenny Hoyos and Todd Sherman: https://www.youtube.com/watch?v=_tWy-_otnUc
- Creator Insider, Public View Counts and Engaged Views: https://www.youtube.com/watch?v=HI03HqWdX0k
- Creator Insider, Shorts Bonuses and Original Content: https://www.youtube.com/watch?v=SmT_pTMF2ms

### Analysts with data (B)
- vidIQ, The Fastest Way to 1,000 Subs in 2026: https://www.youtube.com/watch?v=A6nGdWlcdaE
- Colin and Samir with Paddy Galloway, The New Rules of YouTube (2027): https://www.youtube.com/watch?v=WyiGFFTnIS4
- Marcus Jones, I Studied 5,400 Shorts: https://www.youtube.com/watch?v=ryZt5pc2O5s
- Paddy Galloway, Shorts study thread (2023): https://threadreaderapp.com/thread/1646898356419981315.html
- vidIQ, Shorts and long-form watch histories separated (2022): https://vidiq.com/blog/post/youtube-shorts-long-form-viewers-algorithm/
- Metricool 2026 study, via Tubefilter: https://www.tubefilter.com/2026/08/03/youtube-shorts-long-form-study-metricool/

### Reporting (secondary)
- PPC Land, 2027 YPP and Shorts pay changes: https://ppc.land/youtube-cuts-shorts-pay-for-channels-under-10m-views-from-february-2027/
- PPC Land, what counts as a qualified view: https://ppc.land/shorts-watched-as-ads-do-not-count-toward-youtubes-20-million-view-bar/
- PPC Land, Beaupré interview write-up: https://ppc.land/subscribers-skip-90-of-uploads-in-their-feed-youtube-director-says/
- OutlierKit, the two 2027 clauses: https://outlierkit.com/resources/youtube-partner-program-changes-2027/
- TechCrunch, Shorts Series: https://techcrunch.com/2026/09/23/youtubes-new-short-series-feature-brings-episodic-viewing-to-shorts/
- 9to5Google, originality update: https://9to5google.com/2026/10/02/youtube-wont-recommend-unoriginal-shorts/
- 9to5Google, posts in the Shorts feed test: https://9to5google.com/2026/04/15/youtube-tests-showing-creator-posts-in-your-shorts-feed/
- Tubefilter, custom Shorts thumbnails: https://www.tubefilter.com/2026/07/24/youtube-shorts-custom-thumbnails-neal-mohan-feature-update/
- PPC Land, collaborators feature: https://ppc.land/youtube-launches-collaboration-feature-for-creator-partnerships/
- vidIQ, collaborations guide: https://vidiq.com/blog/post/youtube-collabs/
- TechCrunch, links disabled in Shorts (2023): https://techcrunch.com/2023/08/10/youtube-is-disabling-links-on-shorts-to-cut-down-on-spam
- Search Engine Journal, inauthentic-content clarification: https://www.searchenginejournal.com/youtube-clarifies-monetization-update-targeting-spam-not-reaction-channels/550123/

### Cited only as myths (C/D)
- https://virvid.ai/blog/turning-shorts-views-into-subscribers-2026
- https://subscribr.ai/p/convert-shorts-viewers-to-subscribers
- https://www.influencers-time.com/youtube-shorts-series-how-to-turn-viewers-into-subscribers/
- Isaac: https://www.youtube.com/watch?v=QXfugR3ZIAs
- Beluga breakdown: https://www.youtube.com/watch?v=c5-3gotpgz8

### Our data
- `research/data_2026-10-30.md`
- `research/reference_nefisims.md`
- `research/reference_satisfying2dsims.md`
- `research/breakout_formula.md`
- `<VIDEOS_DIR>\MochiAndBolt\compilations\compilation 1\MANIFEST.md`
