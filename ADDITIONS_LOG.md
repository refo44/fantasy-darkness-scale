# Additions Log

Tracks new works being added to the Fantasy Darkness Scale, one at a time, across sessions.
Process for each item: (1) research & score against the 7 weighted criteria in the xlsx
Methodology sheet, (2) add the row to `Evaluations` with live formulas matching the existing
rows, (3) recalc via LibreOffice to get cached values, (4) determine tier placement, (5) add
the entry to both `index.html` (EN) and `es/index.html` (ES), inserted into the right tier's
`<ul class="works">` in ascending-score order relative to the other works already there (not
appended at the end — the xlsx row order stays chronological/append-only, but the HTML display
order is sorted by score within each tier), (6) commit, push, deploy, verify live, (7) update
this log, (8) stop and ask before continuing.

## Methodology v2 (in progress)

The original (v1) scoring used centered rounding (`ROUND`) on a 0.05-increment continuous
scale per criterion. This caused two problems: (1) a work's displayed score often didn't
share its own tier's leading digit (e.g. a tier-2 work scoring 1.71 — 79 of 87 works had this
mismatch), and (2) 0.05 increments implied more precision than a human judgment can reliably
reproduce (verified: 92% of all criterion ratings were non-integer, most in a 0.05 grid — a
level of precision no rater, including the original one, could consistently repeat).

v2 changes:

- `Final Score = 1.5 + Weighted Internal Score × 2.25`, `Tier = FLOOR(Final Score)` — an
  interval scale instead of centered rounding, so the tier always matches the score's leading
  digit. Verified against all 87 v1 works: zero tier reassignments, since
  `FLOOR(x + 0.5) = ROUND(x)` is a mathematical identity — this is a display-layer fix, not a
  re-scoring.
- Each criterion is now scored as an integer 0-4 (5-point scale, one verbal anchor per level,
  see the v2 Methodology sheet) instead of 0.05 increments. Chosen over a 0-9 half-point scale
  because 7 criteria already compose into a fine-grained total even with coarse individual
  items, and 5 distinct verbal anchors per criterion are far more tractable to write and apply
  consistently than 10.
- Weights and the 7 criteria themselves are unchanged from v1.
- Cozy Fantasy / Hopepunk tags remain excluded from the formula for the same reason as v1 (see
  below) — confirmed still correct in testing (Avatar: The Last Airbender, tagged Hopepunk,
  moved up under v2 based on its actual war/genocide content, not down).

Status: in progress in `Fantasy_Grimdark_Scale_v2_WIP.xlsx`, rescored iteratively, one batch
at a time — 33 of 87 works done so far. The v1 file is preserved as
`Fantasy_Grimdark_Scale_Fully_Scored_DEPRECATED.xlsx` for comparison until v2 is complete and
promoted to replace the live site's data (`index.html` / `es/index.html` still reflect v1 and
haven't been touched yet).

## Cozy Fantasy / Hopepunk tagging criteria

Also documented in the xlsx Methodology sheet (rows 26-32). These columns are **descriptive
only** — excluded from the Weighted Internal Score / Calculated Score formula on purpose,
since genre stance toward darkness is not the same thing as amount of darkness (Avatar: The
Last Airbender is tagged Hopepunk but depicts real war and genocide).

- **Cozy Fantasy = Yes** requires genuinely belonging to that specific book-publishing genre
  (comfort-focused, low-stakes, community/found-family) — not just "has a cozy feeling."
  Anime films like Totoro don't qualify even though they're cozy in tone.
- **Hopepunk = Yes** requires fitting one of three variants — having a hopeful tone or happy
  ending alone is never sufficient:
  - *Gentle* — no real adversity needed; kindness/community/anti-cynicism as the default,
    deliberately-valued state of the world (Totoro, Legends & Lattes).
  - *Fierce* — real external/societal adversity (an oppressive system, empire, institution) +
    hope/kindness as active resistance to it (The House in the Cerulean Sea, Avatar TLA).
  - *Bittersweet* — real existential adversity (mortality, loss, time — not politically
    "resistable") + connection deliberately chosen anyway, knowing it costs grief later
    (Frieren).

## Criteria: theoretical constructs and polarities

Full writeup moved to `CRITERIA_THEORY.md` — what each criterion is a construct of, why six of
the seven correlate tightly (r > 0.96) while Explicit Darkness doesn't, and the low/high
polarity word for each (e.g. Structural Despair: Progress ↔ Decay). Also present as columns
H-J in the v2 Methodology sheet. Useful for resolving borderline calls during rescoring — when
a work's darkness doesn't fit neatly into the 0-4 anchors, asking "which pole is this closer
to" is often clearer than re-reading the literal anchor text.

## v2 Rescoring Backlog (54 of 87 pending)

Takes priority over the "add new works" queue below — these are existing catalog entries
still on the v1 methodology.

Process for each item: (1) score the 7 criteria on the v2 integer 0-4 scale using the anchors
in the v2 Methodology sheet, (2) compute Weighted Internal Score, Final Score, and resulting
tier, (3) **compare the new tier against the work's original v1 tier**, (4) if it differs,
re-examine the specific criteria that moved and decide, based on the actual content of the
work, whether the new tier makes sense — don't accept a tier change just because the formula
produced it (A Song of Ice and Fire and The First Law both needed this correction: initial v2
scores under-rated them relative to the original data, and the tier only came out right after
re-checking criteria against the source material), (4b) **whenever the tier changes, check the
score against neighbors on both sides**: does it sit comfortably among the works already
scored in its *new* tier (not a wild outlier), and does the comparison against its *former*
tier's neighbors still make sense (is it defensible that this work is now darker/lighter than
works it used to sit beside)? Both directions matter — checking only the new tier can miss
that a work no longer belongs with its old neighbors either (see The NeverEnding Story for the
full worked example), (4c) **check that the new tier's category name itself reads true** for
the work — not just the numeric neighbors but the qualitative label (e.g. "Fantasy in Gray
Tones" for The NeverEnding Story: not wholesome, not despairing, genuinely caught between real
loss and ultimate faith — the name fits, not just the number), (5) add the row to
`Fantasy_Grimdark_Scale_v2_WIP.xlsx`, (6) note the v1→v2 comparison decision (including the
neighbor and label checks, when the tier changed) here, (7) check this item off.

Already fully rescored under v2: tiers 1, 7, 8, 9, 10 (every work in those tiers is done — see
`Fantasy_Grimdark_Scale_v2_WIP.xlsx`). Grouped below by original (v1) tier, catalog order.

**Tier 2** (12 pending)
- [x] A Choir of Lies — v2: tier 3 (up from 2). Redemption Difficulty scored higher than the
  prequel (A Conspiracy of Truths, stays tier 2) since the protagonist here causes real
  financial ruin to real people and has to reckon with genuine guilt over it — makes sense as
  "bittersweet/melancholic" rather than "heroic fantasy."
- [x] The Chronicles of Narnia — v2: tier 2 (unchanged, 2.9625, just under the tier-3 line).
  Redemption Difficulty was the swing criterion (Aslan's sacrifice for Edmund could read as a
  2 or a 1) — settled on 1, since Edmund himself doesn't do the work of redemption, someone
  else pays the cost for him.
- [x] Dungeons & Dragons: Honor Among Thieves — v2: tier 2 (unchanged, 2.4). Clean case, no
  borderline calls — meaningfully lighter than Narnia (comedic tone, no on-screen sacrifice)
  even though both tied in the v1 scoring.
- [x] Harry Potter and the Chamber of Secrets — v2: tier 2 (unchanged, 2.625). Higher within
  the tier than Philosopher's Stone (2.062), matching the series' progressive darkening, but
  not enough to cross into tier 3.
- [ ] The Hobbit
- [x] The Hobbit — v2: tier 3 (up from 2, score 3.6375). Same profile shape as LOTR (already
  tier 3) minus one point of Structural Despair — Smaug's threat is contained, not
  world-scale like Sauron's. Thorin's deathbed reconciliation and the melancholic closing note
  about gold push it past "Heroic Fantasy."
- [x] Castle in the Sky — v2: tier 2 (unchanged, 2.2875). Resolves decisively with no lingering
  melancholy, unlike The Hobbit/LOTR — stays in "Heroic Fantasy" territory.
- [x] Spirited Away — v2: tier 3 (up from 2, score 3.6375). Personal liberation within a
  system (Yubaba's bathhouse) that keeps running unchanged is bittersweet, not a clean heroic
  win — matches The Hobbit's neighborhood rather than Castle in the Sky's.
- [x] Final Fantasy III & V — v2: tier 2 (unchanged, 2.175). First pass wrongly landed tier 1
  (Explicit Darkness scored 2) — corrected to 3 after review: Galuf's on-page death plus
  near-constant combat matches level 3's "muerte explícita, con frecuencia" better than
  level 2's "sin detalle grafico extremo." Not a gap in the criteria, just under-scored on the
  one axis that actually carries this game's content — same pattern as ASOIAF/First Law.
- [x] Slayers — v2: tier 2 (unchanged, 2.175). Applied the FF III & V lesson proactively:
  comedic tone almost masked genuinely apocalyptic-scale content (city-leveling magic,
  recurring near-world-ending threat) — Explicit Darkness scored 3, not a lower number, based
  on content/frequency rather than overall tone.
- [x] The Legend of Zelda — v2: tier 2 (unchanged, 2.9625, same score as Narnia — right at the
  edge). Real weight from fallen-kingdom imagery (Breath of the Wild) and the eternal
  reincarnation cycle, but stays heroic-adventure rather than crossing into bittersweet.
- [x] The Little Prince — v2: tier 2 (unchanged, 2.625). Genuine judgment call: the book's
  poignancy concentrates almost entirely into one significant ending rather than sustained
  thematic darkness across criteria, unlike Spirited Away/The Hobbit — stays under the tier-3
  line despite its reputation for sadness.
- [x] Legend — v2: tier 2 (unchanged, 2.5125). The genuinely scary villain (Tim Curry's Lord
  of Darkness) gets captured entirely through Explicit Darkness (3) without needing to inflate
  the structural/thematic axes — clean good-vs-evil story with full restoration, just strong
  atmosphere.
- [x] The NeverEnding Story — v2: tier 4 (up two tiers from 2, score 4.2). Biggest single jump
  so far. Checked against neighbors: lands as the lightest member of tier 4 (below FMA:
  Brotherhood, Earthsea, Avatar), and edges past its former tier-3 peers (LOTR, Frieren) only
  because its darkness runs across three axes at once (active world-destruction, Bastian's
  personal corruption arc, Artax's death) rather than spiking on one. Weighted toward the
  novel's harsher, more permanent memory-loss ending over the film's softer one, since the
  catalog entry covers both.
- [x] Willow — v2: tier 2 (unchanged, 2.85). Label check caught an error: tier 3 has two
  sub-options ("Balanced" vs. "Bittersweet/Melancholic"), and initial scoring wrongly tested
  only against the second. Willow's darkness (infanticide premise, transformations) exists to
  raise stakes for a dominant heroic tone, not to create genuine tonal balance — reconsidered
  Structural Corruption from 2 down to 1 (Bavmorda is an anomaly the story corrects, not
  evidence institutions normally work this way), which brought it back to tier 2 and "Fierce
  Hopepunk & Heroic Fantasy," a much better fit.

**Tier 2 backlog complete (14/14).**

**Tier 3** (13 pending)
- [x] Black Clover — v2: tier 3 (unchanged, 3.975, exactly matching LOTR/Frieren). Flagged
  real tension: numerically matches but tonally lighter than its tier-mates — kept at tier 3
  on the strength of the caste-system oppression being genuinely sustained and central, not
  background texture, similar to how Avatar's hopeful tone didn't reduce its genocide content.
  User confirmed tier 3 is the right call.
- [x] DanMachi — v2: tier 2 (down from 3, score 2.9625). Same shape as Willow: dark plot
  elements (Ishtar/Soma Familias' exploitation) raise stakes for heroism then get dismantled,
  rather than creating sustained tonal darkness. Label check confirms "Fierce Hopepunk &
  Heroic Fantasy" (tier 2) fits better than "Bittersweet/Melancholic" (tier 3) — overall
  register stays upbeat/comedic throughout.
- [x] Dragonlance — v2: tier 5 (up two tiers from 3, score 5.2125). Checked against neighbors:
  lands as the lightest of tier 5 (below Kingkiller Chronicle, Goblin Slayer, Skyrim) —
  reasonable, it's a genuine war epic with sustained occupation and named-character death.
  Label ("Gloomy Fantasy") fits. Leaving Black Clover/LOTR behind at tier 3 is defensible:
  Dragonlance has *sustained* warfare/occupation, not a threat that gets stopped once, plus
  Raistlin's largely unresolved power-hungry arc. User confirmed.
- [x] Dungeon Meshi — v2: tier 3 (unchanged, 3.3). Label "Balanced" fits well — comedy and
  horror are genuinely interwoven simultaneously (eating monsters is funny and unsettling at
  once), unlike Willow/DanMachi where darkness only existed to raise heroic stakes. Sits
  comfortably between Choir of Lies/Mushishi and The Hobbit/Spirited Away.
- [x] Howl's Moving Castle — v2: tier 3 (unchanged, 3.6375, matching The Hobbit/Spirited
  Away). Label "Bittersweet/Melancholic" fits genuinely — centrally about war, aging, and
  erosion of humanity balanced against real love and hope.
- [x] The Boy and the Heron — v2: tier 4 (up from 3, score 4.875, exactly matching FMA:
  Brotherhood). Label "Fantasy in Gray Tones" fits — resolves into neither heroic triumph nor
  pure melancholy (unresolved grief, a world that dissolves rather than gets saved, but real
  warmth too). Leaving Howl's/Hobbit/Spirited Away behind makes sense — those have cleaner
  resolutions than a world that simply ends and a loss explicitly never undone.
- [x] Final Fantasy IV — v2: tier 3 (unchanged, 3.525). Cecil's costly Dark-Knight-to-Paladin
  redemption plus permanent losses (Rydia's mother, destroyed villages) fit "Bittersweet." Sits
  just above Dungeon Meshi, below Hobbit/Spirited Away/Howl's — reasonable placement.
- [x] Final Fantasy IX — v2: tier 4 (up from 3, score 4.875, matching FMA: Brotherhood and
  The Boy and the Heron). Black Mages' disposable engineered lifespans and Vivi's unresolved
  mortality (he dies of old age by the end, never fixed) fit "Fantasy in Gray Tones." Leaving
  FF IV/Dungeon Meshi behind makes sense — the "disposable created life" theme is more
  structurally embedded than FF IV's contained corrupted-king narrative.
- [x] Harry Potter and the Prisoner of Azkaban — v2: tier 4 (up from 3, score 4.5375). The
  Dementors' explicit psychological-horror design (Harry repeatedly reliving his mother's
  death) plus the unresolved systemic justice failure (Sirius never cleared within this book)
  fit "Fantasy in Gray Tones" — the point where the series first gets genuinely heavier. User
  confirmed.
- [x] Harry Potter and the Goblet of Fire — v2: tier 5 (up two tiers from 3, score 5.2125,
  matching Dragonlance at the tier-5 floor). Self-corrected mid-scoring: first pass landed
  5.8875, above Goblin Slayer/Kingkiller — didn't survive the neighbor check for a YA book, so
  Structural Despair and Limited Heroism were pulled back to reflect that the disaster (war,
  Voldemort's return) is just beginning within this book, not sustained. Label "Gloomy
  Fantasy" fits — Cedric's permanent death plus institutional denial mark the series' pivot to
  genuinely somber.
- [x] Earthsea — v2: tier 4 (up from 3, score 4.65, matching Avatar/Grimgar). Label "Fantasy in
  Gray Tones" is an exceptionally good fit — the series is famous specifically for its muted,
  philosophical, Taoist-influenced tone. Comparable weight to Avatar's genocide backstory and
  Grimgar's real grief: cult indoctrination (Tombs of Atuan) plus Ged's permanent loss of
  magic as the cost of saving the world.
- [x] Witch Hat Atelier — v2: tier 4 (up from 3, score 4.3125). The witching society's brutal,
  rigid punishment (erasing faces regardless of intent, which harmed an innocent — Coco's
  mother) plus her still-unresolved guilt fit "Fantasy in Gray Tones." Sits between
  NeverEnding Story and Prisoner of Azkaban — reasonable company.
- [x] Adventure Time — v2: tier 4 (up from 3, score 4.9875, matching Tales from Earthsea).
  Label "Fantasy in Gray Tones" is an exceptionally good fit — the classic example of a show
  that looks bright/silly on the surface while carrying genuine darkness underneath
  (post-apocalyptic setting, Simon/Ice King's decades-long tragedy).
- [x] Record of Lodoss War — v2: tier 3 (unchanged, 3.975, matching LOTR/Frieren/Black
  Clover). Bundling check: kept as one entry (novels + anime) — no real content-darkness
  difference between adaptations, same core story. Explicit Darkness brought down from an
  initial 3 to 2 after comparing to Dragonlance: Lodoss War is classic "heroes vs. invading
  army" without Dragonlance's sustained civilian-suffering-under-occupation quality. Label
  "Balanced" fits — Ashram/Pirotess's tragedy is genuinely interwoven with heroic fantasy, not
  darkness raising stakes for a clean triumph.

**Tier 3 backlog complete (14/14).**

**Tier 4** (19 pending)
- [x] Cormyr — v2: tier 3 (down from 4, score 3.3, matching Dungeon Meshi). Standard political
  intrigue — real corruption/assassination plots but cleanly resolved, without the sustained
  visceral content (body horror, psychological horror, lasting institutional brutality) of its
  former tier-4 neighbors. Label "Balanced" fits.
- [x] Elantris — v2: tier 5 (up from 4, score 5.2125, matching Dragonlance/HP Goblet of Fire).
  The decade-long body-horror premise (unhealing wounds, unrelenting pain/hunger, described in
  real detail) plus state-sanctioned abandonment of the afflicted fits "Gloomy Fantasy."
- [x] The Stormlight Archive — v2: tier 6 (up two tiers from 4, score 6.9, matching Dark
  Souls I–III). Sustained, explicit depiction of Kaladin's clinical depression/suicidal
  ideation (unusually direct for mainstream epic fantasy) plus Dalinar's on-page mass-casualty
  war crime and the lighteyes/darkeyes caste system's foundational discrimination. Label "Dark
  Fantasy" fits — genuinely heavy without being nihilistic.
- [x] The Silmarillion & Great Tales — v2: tier 5 (up from 4, score 5.325, near Skyrim). Went
  through significant back-and-forth (first pass landed tier 7, alongside Berserk — rejected).
  Corrected in two stages: (1) Explicit Darkness pulled from 3 to 2 — Tolkien's mythic,
  chronicle-style prose lacks the graphic detail the higher anchor requires even though the
  content (kinslaying, incest, suicide) is real; (2) Limited Heroism and Narrative Acceptance
  of Injustice pulled down specifically because of Tolkien's own theory of eucatastrophe — a
  deliberate structural "turn" toward unearned grace at the level of the overarching story
  (Eärendil's plea causing Morgoth's defeat, Beren's return from death), which is a citable
  literary fact about this text, not just a vibe. Individual tragedies (Túrin, Fëanor) don't
  get this grace and stayed scored at full severity — this wasn't a blanket lightening.
- [x] Final Fantasy I, II & XII — **split into 3 separate entries**, not kept bundled. Rough
  per-game estimates showed a 3-tier spread (I≈tier 1, II≈tier 3, XII≈tier 4) — much larger
  than the Lodoss War bundling case, where the adaptations genuinely told the same story at
  the same intensity. One number would have badly misrepresented at least two of the three.
  Catalog total is now 89 works, not 87.
  - [x] Final Fantasy I — v2: tier 1 (score 1.725). Virtually no narrative content; four Light
    Warriors restore corrupted Crystals, minimal characterization, clean good-vs-evil.
  - [x] Final Fantasy II — v2: tier 3 (score 3.975, matching LOTR/Frieren/Black Clover/Lodoss
    War). Real war against imperial conquest, Josef's on-page death, Leon's costly fall to
    darkness and redemption after being corrupted/resurrected by the Emperor.
  - [x] Final Fantasy XII — v2: tier 4 (score 4.65, matching Avatar/Grimgar/Earthsea). Real
    imperial conquest (Dalmasca occupied, king killed), Basch wrongfully imprisoned for
    regicide he didn't commit (same injustice shape as Sirius Black), nethicite
    weapons-of-mass-destruction themes, Reddas's sacrifice.
- [x] Final Fantasy XIV — v2: tier 6 (up two tiers from 4, score 6.225, matching The Witcher).
  Real structural outlier worth noting: every other tier-6 work has Limited Heroism at 2-3,
  FFXIV is the only one at 1 (the Warrior of Light is unusually, consistently effective —
  repeatedly stops apocalypses outright). Tested whether that should pull the tier down;
  lowering Structural Despair to compensate didn't hold up (the construct is explicitly
  "independent of character choices," and the world has a demonstrated history of repeated
  civilizational collapse regardless of any hero), and the other honest correction (Moral
  Cynicism up for the millennium of systemic deception) pushed the score up, not down.
  Conclusion: FFXIV reaches tier-6 severity via a different combination than its neighbors
  (lower heroism-futility/cynicism, higher despair/corruption/explicit content) rather than
  matching them axis-by-axis — the multi-criteria system working as intended, not a flaw.
- [x] Harry Potter and the Order of the Phoenix — v2: tier 5 (up from 4, score 5.8875, near
  the top of tier 5). Applied the Goblet of Fire lesson proactively — capped Structural
  Corruption at 2 rather than 3 (Umbridge's tyranny is framed as one year's aberration under a
  bad actor, overturned by book's end, not a permanently embedded condition), which kept it
  out of tier 6's adult-fantasy company (Witcher/FFXIV) while still registering as a real
  escalation from Goblet of Fire's tier-5 floor — Sirius's permanent death and the sustained
  blood-quill torture vs. one scene in GoF. User confirmed.
- [x] Harry Potter and the Half-Blood Prince — v2: tier 5 (up from 4, score 5.8875, exact
  parity with Order of the Phoenix). Considered bumping Limited Heroism to 3 given the book
  ends in outright loss (Dumbledore's death) rather than victory, but that anchor is about
  undercut wins, not losses — kept at 2, held the line at tier 5 rather than tier 6. User
  accepted.
- [x] Harry Potter and the Deathly Hallows — v2: tier 6 (up two tiers from 4, score 6.5625,
  matching FMA 2003/Claymore/Tanya/FFXVI). The one HP book that genuinely earns tier 6 rather
  than being capped at 5 like OotP/HBP — Voldemort's full Ministry takeover is a categorically
  different situation from Umbridge (complete regime change committing genocide-adjacent
  persecution vs. one petty tyrant), justifying Structural Corruption at 3 where OotP was
  capped at 2.
- [ ] Märchen Crown — **skipped for now**, not done. Flagged low confidence: considerably less
  mainstream than everything else in the backlog, and knowledge of specific plot details isn't
  solid enough to score honestly without risking a confident-sounding but shaky breakdown.
  Needs either the user's direct input or a return pass later.
- [x] Mistborn — v2: tier 6 (up two tiers from 4, score 6.5625, matching Deathly Hallows/FMA
  2003/Claymore/Tanya/FFXVI). The Final Empire's millennium-long, foundational Skaa slavery
  plus Hemalurgy's murder-based magic system justify the company.
- [x] Nausicaä of the Valley of the Wind — v2: tier 3 (down from 4, score 3.975, matching
  LOTR/Frieren/Black Clover/Lodoss War/FF II). A dead world and real war balanced against
  genuine hope — Nausicaä's quasi-resurrection lands as an uplifting grace-note, not despair.
- [x] Neverwinter Nights & Baldur's Gate I–III — **split into 4 separate entries**. Rough
  per-game estimates showed a real 2-tier spread (NWN/BG1≈tier 3, BG2≈tier 4, BG3≈tier 5) —
  smaller than the FF I/II/XII case but still genuine, especially between the older games and
  BG3 specifically. Catalog total is now 92 works.
  - [x] Neverwinter Nights — v2: tier 3 (score 3.075). Aribeth's fall to evil after her
    lover's death, a moderate political conspiracy, fully resolved by the end.
  - [x] Baldur's Gate I — v2: tier 3 (score 3.4125). Inherited-evil themes (the protagonist's
    Bhaalspawn heritage), Sarevok's betrayal and iron-crisis conspiracy, Gorion's death.
  - [x] Baldur's Gate II: Shadows of Amn — v2: tier 4 (score 4.3125). Irenicus's monstrous
    experiments, Underdark slaver operations, Bodhi's vampiric cruelty, the protagonist's
    divine murderous heritage intensifying.
  - [x] Baldur's Gate III — v2: tier 5 (score 5.2125). The clear outlier — illithid body
    horror, extensive mature content, multiple companions with genuinely difficult trauma/
    redemption arcs (Astarion's abuse history, Gale's self-destructive addiction), notably
    more explicit than its predecessors.
- [x] Ranking of Kings — v2: **tier 5** (up from 4, score 5.55, matching the gap between
  Baldur's Gate III and Kingkiller Chronicle). Went through four passes — the first two
  contained real plot errors the user caught and corrected (fabricated Hiling poisoning Bojji
  when she's actually an innocent, protective mother who learned sign language for him and
  survives; missed that Bosse stole his own unborn son's strength via demonic pact, that
  Bojji's birth mother Sheena dies permanently shielding him in a coup, and the full scope of
  Miranjo's demon-pact-fueled plot). The third pass over-scored Redemption Difficulty at 2,
  reasoning fans debated whether Miranjo's redemption was "earned" — corrected on the fourth
  pass: the actual controversy is the opposite, fans are unhappy about the "total lack of
  narrative consequences for perpetrators" (complete forgiveness without proportionate cost),
  which is a *low*-difficulty redemption, not a high one — brought down to 1. Final scoring:
  Structural Despair 2, Limited Heroism 1, Moral Cynicism 2, Structural Corruption 2,
  Redemption Difficulty 1, Narrative Acceptance of Injustice 2 (Sheena's death stays
  permanent, a separate axis from perpetrator-consequences), Explicit Darkness 3. Worth
  remembering for future low-confidence titles: ask for a plot check before scoring, not
  after — this one needed four rounds to get right.
- [x] The Dark Elf / Drizzt — v2: tier 5 (up from 4, score 5.325, tied with Skyrim/Silmarillion).
  Scored against the saga broadly (Dark Elf trilogy plus the Companions of the Hall books).
  Menzoberranzan's institutional corruption and inverted moral physics (treachery rewarded over
  virtue) drive the rise, but real, durable heroism (Mithral Hall reclaimed and held, Ten-Towns
  peace sustained) and an achievable central redemption arc (Wulfgar's recovery from addiction/
  PTSD) keep it well short of tier 6. Label check: "Gloomy Fantasy" fits better than the former
  "Fantasy in Gray Tones" — Drizzt is unambiguously good and Menzoberranzan unambiguously evil,
  so this isn't morally gray the way Earthsea/Witch Hat Atelier are, just genuinely dark content
  inside a heroic-adventure register.
- [x] The Legend of Korra — v2: tier 5 (up from 4, score 5.325, tied with Skyrim/Silmarillion/
  The Dark Elf & Drizzt). Scored directly against Avatar: The Last Airbender's already-rescored
  v2 profile (tier 4, 4.65) per the v1 note's own framing ("heavier than its predecessor") —
  Limited Heroism and Structural Corruption rise (Amon/Kuvira's defeats don't fix the root
  political inequality they exploit; Kuvira's fascist state gets sustained on-screen depiction
  TLA's Fire Nation never did), while Moral Cynicism, Redemption Difficulty, Narrative
  Acceptance of Injustice and Explicit Darkness stay level with Avatar — the story still
  resolves toward genuine hope (New Spirit Age) rather than leaving injustice permanent.
  Hopepunk = Yes (Fierce), matching Avatar's tag.
- [x] The Wheel of Time — v2: tier 5 (up from 4, score 5.2125, tied with Dragonlance/Elantris).
  Scored against both LOTR and Dragonlance as close genre neighbors. The Seanchan Empire's
  a'dam slave-collar system for channelers (state law, not aberration, never abolished by
  series' end) drives Structural Corruption and Narrative Acceptance of Injustice above LOTR,
  while Rand's cleansing of the taint on saidin — fixing the root cause of male channelers'
  madness, not just stopping the Dark One — keeps Limited Heroism as low as LOTR's. Explicit
  Darkness lands above both neighbors given the sheer accumulated volume of dark content across
  fourteen books (Trolloc massacres, Padan Fain's body horror, Compulsion).
- [x] Princess Mononoke — v2: tier 5 (up from 4, score 5.55, matching Ranking of Kings). Scored
  against the other Ghibli films already rescored (Spirited Away, Howl's, Boy & Heron) — clearly
  the most graphically violent of the four (on-screen decapitation, Ashitaka's curse forcing
  involuntary killing), and its refusal of a "virtue is rewarded" framework (Eboshi's ruthless
  pragmatism succeeds where the forest gods' righteous resistance doesn't) pushes Moral Cynicism
  and Narrative Acceptance of Injustice above its stablemates, even though Structural Corruption
  stays low — Irontown treats its own people, including outcasts, with genuine dignity; this is
  an external ecological war, not institutional exploitation.
- [x] Star vs. the Forces of Evil — v2: tier 5 (up from 4, score 5.6625, tied with The Kingkiller
  Chronicle). Scored directly against the already-rescored Avatar TLA (tier 4, 4.65) and Legend
  of Korra (tier 5, 5.325) profiles given the shared "oppressed group + reconciliation" shape —
  matches Korra axis-for-axis except one point higher on Narrative Acceptance of Injustice,
  since the finale's total destruction of the magic dimension (rather than reforming the
  Mewman/Monster caste system) is specifically read by critics/fans as a bleak, ambiguous
  resolution rather than the more triumphant endings Avatar/Korra get. Not a claim this show is
  darker across the board than Korra — just one narrow, evidenced differentiator.
- [ ] The Legend of Vox Machina

**Tier 5** (4 pending)
- [ ] Final Fantasy VI
- [ ] Final Fantasy VII
- [ ] Final Fantasy X
- [ ] Final Fantasy XV

**Tier 6** (2 pending)
- [ ] Clevatess
- [ ] Re:Zero − Starting Life in Another World

## Queue

1. [x] El Principito (The Little Prince) — Antoine de Saint-Exupéry — Book — DONE, see Completed
2. [x] Adventure Time — DONE, see Completed
3. [x] Star vs. las fuerzas del mal (Star vs. the Forces of Evil) — DONE, see Completed
4. [x] Clevatess (Majū no Ō to Akago to Shikabane no Yūsha) — Yūji Iwahara — Manga — DONE, see Completed
5. [x] Saga de Tanya the Evil (The Saga of Tanya the Evil) — DONE, see Completed
6. [x] Re:Zero − Starting Life in Another World — DONE, see Completed
7. [x] Legend (1985 film, dir. Ridley Scott, Tom Cruise — a dark lord hunting the last unicorns) — DONE, see Completed
8. [x] La historia sin fin (The NeverEnding Story) — DONE, see Completed
9. [x] Shin Sekai Yori (From the New World) — DONE, see Completed
10. [x] Mushishi — DONE, see Completed
11. [x] Record of Lodoss War — DONE, see Completed
12. [x] The Legend of Vox Machina — DONE, see Completed
13. [x] The Nightmare Before Christmas — DONE, see Completed
14. [x] Willow (1988) — DONE, see Completed
15. [ ] Labyrinth (1986 film, dir. Jim Henson, David Bowie — a goblin king, a labyrinth, a stolen baby brother)
16. [ ] Pan's Labyrinth / El laberinto del fauno (2006 film, dir. Guillermo del Toro — a girl's dark fairy tale amid Falangist Spain)
17. [ ] Attack on Titan (Shingeki no Kyojin) — Hajime Isayama — Manga, Anime
18. [ ] Maleficent (2014 film, Angelina Jolie — Sleeping Beauty retold from the villain's side)
19. [ ] (Des)encanto / Disenchantment (2018 TV series, Matt Groening)
20. [ ] Calabozos y dragones / Dungeons & Dragons (1983 animated TV series)
21. [ ] The Magicians — Lev Grossman — Novels, TV series
22. [ ] House of the Dragon — George R. R. Martin (A Song of Ice and Fire prequel) — TV series
23. [ ] A Knight of the Seven Kingdoms (Dunk & Egg) — George R. R. Martin — Novellas
24. [ ] Once Upon a Time (TV series)
25. [ ] The Shannara Chronicles — based on Terry Brooks' novels — TV series
26. [ ] Dirk Gently's Holistic Detective Agency — Douglas Adams — Novels, TV series
27. [ ] Dark Sun — TSR / Wizards of the Coast — Tabletop (D&D campaign setting) — post-apocalyptic desert world Athas, magic that kills plant life to power spells, widespread slavery, tyrannical sorcerer-kings draining their own kingdoms' life force; deliberately created as a grim subversion of standard D&D high fantasy
28. [ ] Alice in Wonderland — Lewis Carroll — Novel — whimsical, surreal children's fantasy with unsettling undertones (the Queen of Hearts' "off with their heads," nonsensical/threatening logic, identity/growing-up themes), but generally light in overall register
29. [ ] The Wizard of Oz — L. Frank Baum (novel), 1939 film — classic adventure, real peril (the Wicked Witch, flying monkeys) but a fundamentally heartwarming, hopeful children's classic
30. [ ] Wicked — Gregory Maguire (novel), stage musical — revisionist Oz told from Elphaba's perspective; real political oppression (the Wizard's totalitarian regime, persecution of sentient Animals as a genocide/civil-rights allegory), Elphaba's tragic arc as a misunderstood activist villainized by history — notably darker and more morally complex than the original Oz material
27. [ ] The Sandman — Neil Gaiman — Comics, TV series
28. [ ] Supernatural (TV series)
29. [ ] Charmed (1998 TV series)
30. [ ] The Dark Crystal (1982 film, Jim Henson & Frank Oz)
31. [ ] The Dark Crystal: Age of Resistance (2019 TV series)
32. [ ] His Dark Materials — Philip Pullman — Novels, TV series
33. [ ] The Dresden Files — Jim Butcher — Novels, TV series
34. [ ] The Grim Company — Luke Scull — Novels
35. [ ] The Dark Tower — Stephen King — Novels
36. [ ] Eragon (the Inheritance Cycle) — Christopher Paolini — Novels
37. [ ] The Princess Bride — William Goldman — Novel, Film
38. [ ] Fourth Wing / Iron Flame / Onyx Storm (Empyrean series) — Rebecca Yarros — Novels — score each, bundle into one entry if they land in the same tier
39. [ ] Sweet Tooth — Jeff Lemire — Comics, TV series
40. [ ] Arcane — Riot Games — TV series
41. [ ] Percy Jackson & the Olympians — Rick Riordan — Novels, TV series
42. [ ] Devilman Crybaby (2018) — Masaaki Yuasa (based on Go Nagai's Devilman manga) — Anime

## Completed

### 14. Willow (1988) — Ron Howard / George Lucas — Film

- Tier 2, Calculated Score 1.85 (Weighted Internal Score 0.3775) — tied
  on the rounded display with Castle in the Sky, inserted right before it.
- Scores: Structural Despair 0.45, Limited Heroism 0.3, Moral Cynicism 0.3,
  Structural Corruption 0.45, Redemption Difficulty 0.25, Narrative
  Acceptance of Injustice 0.3, Explicit Darkness 0.7
- Rationale: Queen Bavmorda's decree to imprison every pregnant woman in
  the land, driven by a prophecy of her downfall, is genuinely severe
  institutional cruelty — pushing Structural Corruption above the Narnia/
  Castle-in-the-Sky cluster it otherwise resembles. Airk dies in battle, a
  real named-character loss. Against that: Willow's comic-tinged
  transformation-magic mishaps, Sorsha's clean and successful defection/
  redemption arc, and Bavmorda's almost ironic, self-inflicted defeat keep
  the register close to classic 80s heroic-fantasy peers rather than
  pushing toward Legend's more visceral horror-villain intensity.
- Cozy Fantasy = No. Hopepunk = No — an "evil ruler overthrown" plot shape
  like Narnia/D&D Honor Among Thieves/Castle in the Sky, all of which
  decline the tag; reserved elsewhere on this scale for entries with a
  more sustained, explicit found-family/resistance throughline.
- Added to xlsx row 88, and to tier 2 on both index.html and es/index.html
  (title: "Willow en la tierra del encanto" in ES — the official Latin
  American title, notably more elaborate than a literal translation —
  "Willow" in EN).

### 13. The Nightmare Before Christmas — Tim Burton / Henry Selick — Film

- Tier 2, Calculated Score 1.71 (Weighted Internal Score 0.3175) — the new
  tier-2 floor, just below Harry Potter and the Philosopher's Stone (1.78).
- Scores: Structural Despair 0.25, Limited Heroism 0.25, Moral Cynicism
  0.2, Structural Corruption 0.15, Redemption Difficulty 0.2, Narrative
  Acceptance of Injustice 0.2, Explicit Darkness 1.3
- **Corrected after initial placement.** First scored at tier 1 (1.46,
  Explicit Darkness 0.7) on the reasoning that the plot resolves safely
  and Halloween Town is fundamentally a kind community — true, but it
  underweighted how much of the film is spent in genuinely macabre,
  disturbing visual territory: skeleton/monster designs throughout,
  Sally's repeated self-dismemberment, Oogie Boogie sadistically
  gambling with Santa's life, children traumatized by monstrous gifts,
  the military shooting down Jack's sleigh. The user flagged the tier-1
  placement as inconsistent with that tier's own "Very Bright Fantasy"
  register, which was the right call — Explicit Darkness alone justifies
  the move, even with every other axis staying low.
- Cozy Fantasy = No. Hopepunk = No — revised down from Gentle: once
  Oogie Boogie's menace is weighted properly, "no real adversity needed"
  no longer fits as cleanly as it seemed to at the lighter score.
- Added to xlsx row 87, and to tier 2 on both index.html and es/index.html,
  inserted as the new first entry (title: "El extraño mundo de Jack" in
  ES — the official Latin American dub title, notably different from a
  literal translation — "The Nightmare Before Christmas" in EN).

### 12. The Legend of Vox Machina — Critical Role — TV

- Tier 4, Calculated Score 3.75 (Weighted Internal Score 1.22) — tied on
  the rounded display with Star vs. the Forces of Evil, inserted right
  after it.
- Scores: Structural Despair 1.3, Limited Heroism 1.1, Moral Cynicism 1.25,
  Structural Corruption 1.3, Redemption Difficulty 0.95, Narrative
  Acceptance of Injustice 1.0, Explicit Darkness 1.85
- Rationale: the Amazon animated adaptation of the Critical Role D&D
  campaign is TV-MA — confirmed gore, a torture scene, on-screen child
  deaths, and heavy drinking/crude-humor content push Explicit Darkness
  above most of this tier, closer to Harry Potter and the Deathly Hallows
  than to its more family-friendly tier-4 neighbors. Percy's
  demon-fueled (Orthax) revenge arc after the Briarwoods massacre his
  family, and Vax'ildan's permanent death — paying his soul to the Raven
  Queen to save his sister — are real, sustained personal darkness. Against
  that: heroism is consistently effective (Whitestone is liberated, Percy
  overcomes his darkness, the party wins every major arc), and the
  found-family bond and crude comedy keep hope structurally dominant
  throughout, in the same register as Korra/Stormlight/Wheel of Time.
- Cozy Fantasy = No. Hopepunk = No: the Briarwoods' tyranny over
  Whitestone, actively overthrown by the party, has real Fierce-shaped
  bones, but the show's dominant tonal register (raunchy TV-MA comedy)
  doesn't match the earnest kindness-as-organizing-value quality the tag
  has consistently required elsewhere — a closer call than most declines
  logged here, worth another look if a future pass disagrees.
- Added to xlsx row 86, and to tier 4 on both index.html and es/index.html,
  inserted immediately after Star vs. the Forces of Evil (title kept in
  English on both pages — Amazon's official Latin American release uses
  the same English title even with Spanish dub audio; medium: "TV").

### 11. Record of Lodoss War — Ryo Mizuno — Novels / Anime

- Tier 3, Calculated Score 2.74 (Weighted Internal Score 0.775) — between
  Howl's Moving Castle (2.73) and Dragonlance (2.755).
- Scores: Structural Despair 0.9, Limited Heroism 0.75, Moral Cynicism 0.7,
  Structural Corruption 0.85, Redemption Difficulty 0.6, Narrative
  Acceptance of Injustice 0.6, Explicit Darkness 1.15
- Rationale: the foundational D&D-inspired anime/novel epic — closest
  thematic sibling on this scale is Dragonlance, and it lands right beside
  it. The Marmo invasion of Lodoss costs both warring kings their lives,
  and the party loses its dwarf, Ghim, in the OVA's finale (killed freeing
  a possessed companion's soul); the Grey Witch Karla's whole operating
  principle — centuries spent secretly orchestrating wars across Lodoss's
  history to keep any one nation from dominating — is real, sustained
  Structural Corruption. Against that: the heroes still win a clean,
  restorative victory, keeping it well short of tier 4's heavier war
  epics.
- Cozy Fantasy = No. Hopepunk = No — a classic "war happens, heroes defend
  home and win" shape rather than resistance to a specific oppressive
  institution, same reasoning as Dragonlance/LOTR.
- Added to xlsx row 85, and to tier 3 on both index.html and es/index.html,
  inserted between the same two neighbors (title and medium kept identical
  in EN/ES: "Record of Lodoss War" / "Novels, Anime").

### 10. Mushishi — Yuki Urushibara — Manga / Anime

- Tier 2, Calculated Score 2.05 (Weighted Internal Score 0.4675) — between
  A Conspiracy of Truths (1.98) and The NeverEnding Story (2.11).
- Scores: Structural Despair 0.7, Limited Heroism 0.4, Moral Cynicism 0.25,
  Structural Corruption 0.2, Redemption Difficulty 0.3, Narrative Acceptance
  of Injustice 0.6, Explicit Darkness 1.0
- Rationale: an anthology of folk-tale-style encounters between Ginko (a
  wandering Mushi scholar) and Mushi, primordial life-forms that cause
  strange, often tragic afflictions when they interact with people.
  Unlike almost everything else on this scale, there's no villain, no war,
  no institution to critique — every score on the institutional/heroism
  axes (Limited Heroism, Structural Corruption) stays low because there's
  no "wider structure" for heroism to fail to change. What earns real
  weight is Explicit Darkness and Narrative Acceptance of Injustice: many
  episodes end in genuine, irreversible loss (a mother dying trying to
  save her daughter, a character permanently losing an arm, lasting grief
  from a fatal accident), and Ginko doesn't always succeed — the show's
  whole philosophy is accepting impermanence as natural rather than
  something to defeat.
- Cozy Fantasy = No. Hopepunk = Yes (Bittersweet) — arguably the purest fit
  for this tag on the entire scale. Where prior close calls (The
  NeverEnding Story, Clevatess, Re:Zero) were declined because mortality
  was a framing device or the darkness too pervasive, Mushishi's entire
  structure, episode after episode, is "loss is real and often permanent,
  and connection/care persist anyway" — exactly the Frieren-shaped
  Bittersweet criterion, just at a much gentler overall darkness level
  (which is fine: the tag measures stance toward darkness, not amount of
  darkness, per the Methodology sheet's own note).
- Added to xlsx row 84, and to tier 2 on both index.html and es/index.html,
  inserted between the same two neighbors (title and medium kept identical
  in EN/ES: "Mushishi" / "Manga, Anime").

### 9. Shin Sekai Yori (From the New World) — Yusuke Kishi — Novel / Anime

- Tier 8, Calculated Score 8.41 (Weighted Internal Score 3.295) — second
  only to A Song of Ice and Fire (8.43), above Dark Souls (8.40).
- Scores: Structural Despair 3.3, Limited Heroism 3.4, Moral Cynicism 3.1,
  Structural Corruption 3.5, Redemption Difficulty 3.1, Narrative Acceptance
  of Injustice 3.3, Explicit Darkness 3.4
- Rationale: an apparently idyllic 1,000-years-future society turns out to
  be built on a secret eugenics program — children flagged as
  psychologically "unstable" are killed and memory-wiped from the
  community (one protagonist's close friend becomes such a case and takes
  his own life; another is killed by trained animals for poor class
  performance) — and on the slavery and periodic extermination of the
  Queerats, revealed to be humanity's own left-behind, devolved kin. This
  is about as institutionally embedded as injustice gets on this scale, so
  Structural Corruption sits at the top of the tier. Limited Heroism is
  similarly severe: the ending is explicit that the protagonists achieve
  only a tactical win (stopping the immediate crisis) while "fundamentally
  fail[ing] to dismantle oppression" — the totalitarian apparatus persists
  completely unchanged, with only a vague, personal hope that the next
  generation might do better from within the same power structure.
- Cozy Fantasy = No. Hopepunk = No.
- Added to xlsx row 83, and to tier 8 on both index.html and es/index.html,
  inserted between Dark Souls and A Song of Ice and Fire (title and medium
  kept identical in EN and ES: "Shin Sekai Yori (From the New World)" /
  "Novel, Anime").

### 8. The NeverEnding Story — Michael Ende — Novel / Film

- Tier 2, Calculated Score 2.11 (Weighted Internal Score 0.4925) — the new
  tier-2 ceiling, above A Conspiracy of Truths (1.98).
- Scores: Structural Despair 0.6, Limited Heroism 0.45, Moral Cynicism 0.5,
  Structural Corruption 0.3, Redemption Difficulty 0.5, Narrative Acceptance
  of Injustice 0.3, Explicit Darkness 0.95
- Rationale: scored against the full Michael Ende novel, not just the 1984
  film — an important distinction, since the film only adapts the book's
  first half. That first half alone (Artax's death in the Swamp of Sadness,
  Gmork's nihilism, the Nothing consuming Fantastica) would likely land
  close to Legend or the Hobbit/Spirited Away cluster (~1.8). The book's
  second half pushes it higher: once Bastian is granted AURYN and unlimited
  wishes, that power corrupts him — he grows cruel and tyrannical, nearly
  loses his own memories and identity, and strains his friendship with
  Atreyu to the breaking point — a real "even the purest heart is
  corrupted by absolute power" throughline the film omits entirely, which
  is why Moral Cynicism, Limited Heroism and Redemption Difficulty all sit
  above the typical tier-2 range. Structural Corruption stays low since
  this is personal/individual corruption, not an institutional one.
- Cozy Fantasy = No. Hopepunk = No: considered Bittersweet, given Bastian's
  grief over his mother's death and the ending's choice of his father's
  real, mortal love over infinite wish-granting power — but that theme
  frames the story rather than sustaining it the way it does for Frieren,
  so it doesn't clear the bar.
- Added to xlsx row 82, and to tier 2 on both index.html and es/index.html,
  inserted as the new final entry (title: "La historia sin fin" in ES,
  matching the queue's own phrasing; medium: "Novela, Película" / "Novel,
  Film").

### 7. Legend (1985) — Ridley Scott — Film

- Tier 2, Calculated Score 1.91 (Weighted Internal Score 0.405) — between
  The House in the Cerulean Sea (1.90) and A Choir of Lies (1.95).
- Scores: Structural Despair 0.5, Limited Heroism 0.3, Moral Cynicism 0.35,
  Structural Corruption 0.3, Redemption Difficulty 0.3, Narrative Acceptance
  of Injustice 0.35, Explicit Darkness 0.9
- Rationale: a mythic fairy tale, not an institutional one — there's no
  political system or empire to critique, so Structural Corruption stays
  low, and heroism is completely decisive (Jack single-handedly banishes
  Darkness). What pulls it above the Narnia/Zelda/Castle-in-the-Sky cluster
  is Explicit Darkness: Tim Curry's Lord of Darkness is genuinely
  atmospheric gothic horror (widely cited as one of practical-effects
  fantasy's most frightening villain designs), the unicorn stallion's death
  is a real emotional gut-punch driving the whole plot, and there's an
  on-screen decapitation (the swamp hag Meg Mucklebones). Lili's vanity
  enables the unicorn's death, but the story frames this as innocence
  exploited by Darkness's manipulation rather than genuine culpability, and
  her arc resolves cleanly — keeping Redemption Difficulty and Moral
  Cynicism moderate rather than heavy.
- Cozy Fantasy = No. Hopepunk = No: no institutional adversity for a Fierce
  read, and while the Director's Cut ending is wistful (Lili and Jack can't
  stay together), it's a classic bittersweet romantic beat rather than an
  existential meditation on mortality/time, so it doesn't clear the
  Bittersweet bar either.
- Ridley Scott's film exists in multiple cuts (US theatrical, European,
  and the 2002 Director's Cut) with different scores and slightly different
  ending tone; scored against the Director's Cut, generally regarded as the
  most complete version, though the differences are mostly editing/music
  rather than plot.
- Added to xlsx row 81, and to tier 2 on both index.html and es/index.html
  (title: "Leyenda" in ES, the standard Spanish title; medium: "Película" /
  "Film").

### 6. Re:Zero − Starting Life in Another World — Tappei Nagatsuki — Light Novels / Manga / Anime

- Tier 6, Calculated Score 5.82 (Weighted Internal Score 2.14) — the new
  lowest-scoring entry in tier 6, just below Clevatess (5.85).
- Scores: Structural Despair 2.3, Limited Heroism 1.8, Moral Cynicism 2.1,
  Structural Corruption 2.3, Redemption Difficulty 1.9, Narrative Acceptance
  of Injustice 1.8, Explicit Darkness 3.1
- Rationale: Subaru's "Return by Death" makes every failure a genuine,
  often graphically brutal on-screen death that he alone remembers —
  arguably the most sustained psychological-horror content on this scale,
  which is why Explicit Darkness sits at the top of this tier. But the
  loops are also the mechanism by which heroism *actually works*: each arc
  (the Sanctuary curse, the White Whale, Petelgeuse) gets solved, at
  enormous personal cost but with real, lasting effect on the wider world —
  so Limited Heroism and Narrative Acceptance of Injustice sit low relative
  to peers, since the story's whole engine is Subaru refusing to accept a
  bad outcome as final. Real prejudice exists (Emilia's discrimination for
  resembling the reviled Witch, demi-human oppression in the Sanctuary arc,
  the Witch Cult's fanaticism), but the found-family throughline is
  genuinely restorative rather than merely aspirational, keeping Moral
  Cynicism and Redemption Difficulty moderate rather than severe.
- Cozy Fantasy = No. Hopepunk = No — same reasoning as recent tier 6+
  entries: the found-family/growth-through-adversity shape has real
  hopepunk texture, but no tier-4-or-darker work gets the tag here once the
  explicit content is this heavy.
- Scored against the story through the arcs most widely adapted/translated
  (roughly Arcs 1–6). A Season 4 anime (covering later arcs) began airing
  April 2026 and is still mid-run as of this entry — noted here in case a
  future session needs to revisit once it concludes.
- Added to xlsx row 80, and to tier 6 on both index.html and es/index.html,
  inserted as the new first entry in the tier (title: "Re:Zero: Empezar de
  cero en un mundo diferente" in ES — the official Latin American Spanish
  dub title — "Re:Zero − Starting Life in Another World" in EN).

### 5. The Saga of Tanya the Evil — Carlo Zen — Light Novels / Manga / Anime / Film

- Tier 7, Calculated Score 7.30 (Weighted Internal Score 2.8) — the tier's
  second work, just below Berserk (7.31); tier 7 switched from the "solo"
  single-item centered layout to the standard grid on both HTML pages.
- Scores: Structural Despair 2.5, Limited Heroism 2.8, Moral Cynicism 3.1,
  Structural Corruption 2.7, Redemption Difficulty 2.8, Narrative Acceptance
  of Injustice 2.7, Explicit Darkness 3.1
- Rationale: a reincarnated corporate salaryman becomes Tanya Degurechaff, a
  ruthlessly effective officer in a magic-augmented WWI-that-never-ended.
  Scored against Berserk on a per-axis basis rather than assumed to be
  lighter just because it's less viscerally graphic: Structural Despair and
  Explicit Darkness sit *below* Berserk's (this is bleak, satirical total
  war, not Berserk's cosmic body-horror), but Limited Heroism, Moral
  Cynicism, Redemption Difficulty and Narrative Acceptance of Injustice sit
  *above* it — there's no Guts-equivalent making heroism a functioning
  force, the entire thesis is that cynical pragmatism outperforms idealism,
  and Tanya never redeems or meaningfully changes (confirmed: she stays
  fundamentally the same cold pragmatist throughout, with no found-family/
  healing throughline the way Berserk has with Casca). The two profiles net
  out to nearly identical overall severity.
- Cozy Fantasy = No. Hopepunk = No — about as far from hopepunk as this
  scale gets; no hope-driven resistance, no redemption arc.
- Scored against the story through Season 1, the 2019 film, and the
  currently-translated light novels/manga. A Season 2 anime premiered July
  2026 (right around when this entry was added) — too recent to have
  factored into this score; a future session may need to revisit if it
  meaningfully changes the story's trajectory.
- Added to xlsx row 79, and to tier 7 on both index.html and es/index.html,
  inserted before Berserk (title: "Saga de Tanya the Evil" in ES, matching
  the queue's own phrasing; medium: "Novelas ligeras, Manga, Anime,
  Película" / "Light Novels, Manga, Anime, Film").

### 4. Clevatess — Yūji Iwahara — Manga / Anime

- Tier 6, Calculated Score 5.85 (Weighted Internal Score 2.155)
- Scores: Structural Despair 2.1, Limited Heroism 1.9, Moral Cynicism 2.2,
  Structural Corruption 2.4, Redemption Difficulty 1.7, Narrative Acceptance
  of Injustice 2.0, Explicit Darkness 3.1
- Rationale: after the Beast King Clevatess wipes out a kingdom in
  retaliation for a failed assassination attempt, he's left to raise a
  human infant — and the found-family bond that follows is what keeps him
  from following through on annihilating humanity. That's a genuinely strong
  redemption throughline (lower Redemption Difficulty than most of this
  tier) inside a otherwise severe world: infant trafficking and
  experimentation by bandits/antagonists, a named character (Nell) with an
  official content warning for sustained physical, emotional and sexual
  abuse, brutal forced transformations, and expanding political corruption
  (a cardinal secretly serving a demon lord) push Explicit Darkness and
  Structural Corruption above most tier-6 peers. Net effect lands it just
  below Goblin Slayer (5.96) — comparably dark source material, but with a
  more central and more successful redemption arc softening the total.
- Cozy Fantasy = No. Hopepunk = No: the found-family-defying-hierarchy shape
  echoes Fierce Hopepunk, but no work at tier 4 or darker has been tagged
  Hopepunk=Yes on this scale — at this severity the dark content dominates
  enough page-time that "kindness as the organizing response to adversity"
  isn't the right frame, so staying consistent with that precedent.
- Scored against the story as currently published (manga ongoing since 2020,
  anime adaptation aired mid-2025) — later arcs may shift this if the story
  resolves very differently.
- Added to xlsx row 78, and to tier 6 on both index.html and es/index.html,
  inserted as the new lowest-scoring entry in the tier (just below Goblin
  Slayer); title "Clevatess" kept as-is in both EN and ES.

### 3. Star vs. the Forces of Evil — Daron Nefcy — TV / Comics

- Tier 4, Calculated Score 3.75 (Weighted Internal Score 1.2225)
- Scores: Structural Despair 1.3, Limited Heroism 1.15, Moral Cynicism 1.0,
  Structural Corruption 1.5, Redemption Difficulty 1.0, Narrative Acceptance
  of Injustice 1.2, Explicit Darkness 1.5
- Rationale: the later seasons are built around centuries of Mewman genocide
  against Monsters — Star's own ancestor Solaria "the Monster Carver"
  literally engineered a spell meant to exterminate them, and the Mewman/
  Monster caste divide is the throughline Star spends the show trying to
  dismantle. The series finale ("Cleaved") resolves the final genocidal-army
  threat not by reforming the system but by Star destroying the magic
  dimension and her own powers outright — widely read by critics/fans as a
  bleak, ambiguous "solution" rather than a clean victory, which is why
  Structural Despair and Narrative Acceptance of Injustice sit above most
  tier-4 peers. Weighed against that: the show's early seasons are
  broad, silly monster-of-the-week comedy, heroism does stop the immediate
  threat, and Star's arc is toward reconciliation rather than cynicism —
  keeping it well short of Korra (3.81), the tier's heaviest entry, while
  landing above Discworld/Elantris and alongside Stormlight/Wheel of Time.
- Cozy Fantasy = No. Hopepunk = No: the oppressed-Monsters-plus-active-
  resistance shape resembles Fierce Hopepunk (cf. Avatar), but the ending
  isn't hope triumphing over the oppressive structure — it's the structure
  (and the magic underpinning it) being erased as a last resort — so it
  doesn't clear the bar.
- Added to xlsx row 77, and to tier 4 on both index.html and es/index.html,
  inserted between Ranking of Kings (3.69) and Final Fantasy I, II & XII
  (3.76) per score order (title: "Star vs. las fuerzas del mal" in ES —
  standard Latin American Spanish title — "Star vs. the Forces of Evil" in
  EN; medium: "TV, Cómics" / "TV, Comics").

### 2. Adventure Time — Pendleton Ward — TV / Comics

- Tier 3, Calculated Score 2.68 (Weighted Internal Score 0.745)
- Scores: Structural Despair 0.85, Limited Heroism 0.75, Moral Cynicism 0.6,
  Structural Corruption 0.85, Redemption Difficulty 0.55, Narrative Acceptance
  of Injustice 0.6, Explicit Darkness 1.15
- Rationale: set in the Land of Ooo roughly a thousand years after the
  Mushroom War, an implied nuclear apocalypse — a heavier structural backdrop
  than most tier-3 peers, and the show is unusually willing to show surreal
  horror/body-horror imagery (post-war wastelands, the Lich's true rotting
  form, GOLB) for something aimed at kids. Institutions across Ooo (Ice
  Kingdom, Flame Kingdom, Candy Kingdom under PB) skew more authoritarian
  than most tier-3 peers too. Against that: heroism is consistently
  effective (Finn & Jake decisively win, including against the Lich and
  GOLB), the show's core tone is warm and unfailingly kind rather than
  cynical, and redemption is a major recurring thread (Simon/Ice King,
  Marceline and her father) even where it takes the whole series to land.
  Net effect lands it just below Avatar (2.71) and alongside Dungeon Meshi
  (2.69) and Final Fantasy IV (2.68) — comparable "balanced/melancholic"
  company.
- Cozy Fantasy = No (not part of that book-publishing genre). Hopepunk = No:
  considered Bittersweet given Ice King/Simon's tragic loss of self and the
  show's recurring meditations on memory, mortality and time (comparable to
  Frieren), but unlike Frieren that theme isn't the throughline of the whole
  work — it's one strand in a largely episodic adventure-comedy — so it
  doesn't clear the bar the log has been enforcing strictly (see
  clarifications above).
- Added to xlsx row 76, and to tier 3 on both index.html and es/index.html
  (title: "Hora de aventura" in ES — the standard Latin American Spanish
  dub title — "Adventure Time" in EN; medium: "TV, Cómics" / "TV, Comics").

### 1. The Little Prince (El Principito) — Antoine de Saint-Exupéry — Book

- Tier 2, Calculated Score 1.83 (Weighted Internal Score 0.37)
- Scores: Structural Despair 0.3, Limited Heroism 0.5, Moral Cynicism 0.2,
  Structural Corruption 0.2, Redemption Difficulty 0.4, Narrative Acceptance
  of Injustice 0.2, Explicit Darkness 1.0
- Rationale: gentle, fundamentally hopeful fable (satirizes adult vanity/greed
  rather than rewarding it, no despairing world-structure, no institutional
  injustice). The one real weight is the prince's death near the end, treated
  with poignant restraint rather than graphic darkness — comparable in
  register to Narnia's Aslan (also tier 2, 1.82).
- Added to xlsx row 75, and to tier 2 on both index.html and es/index.html
  (title: "El Principito" in ES, medium: "Libro" in ES / "Book" in EN).
- Widened Summary sheet COUNTIF/AVERAGEIF ranges from $74 to $200 to
  accommodate future additions without re-editing those formulas each time.
