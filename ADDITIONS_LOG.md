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

Status: **scoring complete** in `Fantasy_Grimdark_Scale_v2_WIP.xlsx` — all 92 of 92 catalog works
rescored (see the v2 Rescoring Backlog section below for the full history). Not yet promoted to
the live site. The v1 file is preserved as
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
- [x] Märchen Crown — v2: **tier 6** (score 6.7875). Previously skipped for low confidence;
  resolved via a dedicated multi-language research pass (EN/ES/FR/DE/JA/PT — forums, reviews,
  industry news, retailer listings) since this is a still-ongoing, 16-month-old seinen manga
  (Akasaka/Kujira/Azychika, Weekly Young Jump since March 2025) without the accumulated critical
  consensus the rest of the catalog has. First pass landed tier 8 — an exact match for A Song of
  Ice and Fire's profile, the same uniform-high-value default that produced the earlier tier-5
  cluster, just one notch up. Corrected after checking each axis independently against the actual
  tier 6-9 ceiling data: Structural Despair, Limited Heroism, Moral Cynicism, Redemption
  Difficulty, and Narrative Acceptance of Injustice all pulled back from 3 to 2 (each had been set
  by the story's severe content — an on-page decapitation, attempted sexual assault, a systemic
  foot-mutilation terror campaign — without independent axis-specific justification); Structural
  Corruption (3, multiple separately corrupt kingdom authorities) and Explicit Darkness (4,
  central/recurring extreme content) held up under scrutiny. Lands just below Dark Souls
  I–III/The Stormlight Archive and appropriately well below Berserk — a 35-year genre landmark
  this reception-mixed newcomer shouldn't be matching. Lower confidence than the rest of this
  catalog; worth revisiting once the story's announced final arc concludes.
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
- [x] Ranking of Kings — v2: **tier 4** (unchanged from v1, score 4.875 — see re-audit note
  below). Went through four scoring passes before that — the first two contained real plot
  errors the user caught and corrected (fabricated Hiling poisoning Bojji when she's actually
  an innocent, protective mother who learned sign language for him and survives; missed that
  Bosse stole his own unborn son's strength via demonic pact, that Bojji's birth mother Sheena
  dies permanently shielding him in a coup, and the full scope of Miranjo's demon-pact-fueled
  plot).
- [x] The Dark Elf / Drizzt — v2: tier 5 (up from 4, score 5.55 — see re-audit note below).
  Scored against the saga broadly (Dark Elf trilogy plus the Companions of the Hall books).
  Menzoberranzan's institutional corruption drives the rise, but real, durable heroism (Mithral
  Hall reclaimed and held, Ten-Towns peace sustained) and an achievable central redemption arc
  (Wulfgar's recovery from addiction/PTSD, at real cost) keep it well short of tier 6. Label
  check: "Gloomy Fantasy" fits better than the former "Fantasy in Gray Tones" — Drizzt is
  unambiguously good and Menzoberranzan unambiguously evil, so this isn't morally gray the way
  Earthsea/Witch Hat Atelier are, just genuinely dark content inside a heroic-adventure register.
- [x] The Legend of Korra — v2: tier 5 (up from 4, score 5.325 — see re-audit notes below). Scored
  directly against Avatar: The Last Airbender's already-rescored v2 profile (tier 4, 4.65) per
  the v1 note's own framing ("heavier than its predecessor") — Limited Heroism rises on its own,
  independent evidence (Amon's defeat doesn't fix bender/non-bender inequality; Avatar's
  war-ending victory was more structurally complete), while Structural Corruption, Narrative
  Acceptance of Injustice, and Explicit Darkness all stay level with Avatar. Hopepunk = Yes
  (Fierce), matching Avatar's tag.
- [x] The Wheel of Time — v2: tier 5 (up from 4, score 5.55 — see re-audit note below). Scored
  against both LOTR and Dragonlance as close genre neighbors. The Seanchan Empire's a'dam
  slave-collar system for channelers (state law, not aberration, only a truce secured by
  series' end, never abolished) drives Narrative Acceptance of Injustice above LOTR, while
  Rand's cleansing of the taint on saidin — fixing the root cause of male channelers' madness,
  not just stopping the Dark One — keeps Limited Heroism as low as LOTR's. Explicit Darkness
  lands above both neighbors given the sheer accumulated volume of dark content across fourteen
  books (Trolloc massacres, Padan Fain's body horror, Compulsion).

  **Re-audit round 1 (Ranking of Kings, Drizzt, Korra, Wheel of Time), prompted by a user
  observation that six consecutive v2 rescores had all landed in tier 5:** re-derived each axis
  of all six recent tier-5-landing items (these four plus Princess Mononoke and Star vs. the
  Forces of Evil, both logged below) directly against the rubric anchor text, instead of
  "unchanged from the last-scored neighbor." Root cause: several axes had been set by copying a
  neighbor's value forward rather than independently re-deriving it. Result at this stage:
  Ranking of Kings dropped a full tier (5→4); Drizzt and Wheel of Time each had 1-2 axes
  corrected but stayed in tier 5; Korra and Mononoke/Star vs. the Forces of Evil looked unchanged
  after this first pass — but see round 2 below, where two more of these didn't hold up.

  **Re-audit round 2, prompted by extending the check to the entire tier roster (not just
  neighbors) on both the old and new tier, plus a genuine tier-label read:** comparing Korra and
  Star vs. the Forces of Evil against Fullmetal Alchemist: Brotherhood — a non-adjacent tier-4
  item centered on literal genocide and body-horror alchemy — surfaced that neither one should
  plausibly outscore it on Structural Despair/Limited Heroism/Narrative Acceptance of Injustice.
  Both had the same root cause: one single fact (Kuvira's on-screen regime for Korra; the
  finale's magic-destruction for Star vs. the Forces of Evil) had been used to justify bumps on
  two or three *different* constructs simultaneously — the same double-counting failure round 1
  was supposed to catch, just missed because round 1 only tested neighbor-adjacent comparisons.
  Star vs. the Forces of Evil drops a full tier (5→4, score 4.9875), landing back at its v1 tier
  with only the one well-evidenced Narrative Acceptance of Injustice bump surviving. Korra keeps
  its tier-5 placement (on Limited Heroism, which rests on genuinely separate evidence) but drops
  from 5.55 to 5.325 after its Explicit Darkness bump also didn't survive a frequency check
  against true multi-volume-saga peers (Wheel of Time, Drizzt). Label checks: "Fantasy in Gray
  Tones" fits Star vs. the Forces of Evil better than "Gloomy Fantasy" now — the show's dominant
  register stays comedic even in its darker seasons. Full per-axis reasoning for both is in
  SCORING_RECORD.md.
- [x] Princess Mononoke — v2: tier 5 (up from 4, score 5.55, matching Drizzt/Wheel of Time).
  Scored against the other Ghibli films already rescored (Spirited Away, Howl's, Boy & Heron) —
  clearly the most graphically violent of the four (on-screen decapitation, Ashitaka's curse
  forcing involuntary killing), and its refusal of a "virtue is rewarded" framework (Eboshi's
  ruthless pragmatism succeeds where the forest gods' righteous resistance doesn't) pushes Moral
  Cynicism and Narrative Acceptance of Injustice above its stablemates, even though Structural
  Corruption stays low — Irontown treats its own people, including outcasts, with genuine
  dignity; this is an external ecological war, not institutional exploitation. Checked against
  the full tier 4 and tier 5 rosters (not just neighbors) in both re-audit rounds — held up both
  times, including against Fullmetal Alchemist: Brotherhood, since each axis traces to distinct,
  specific film content rather than one fact reused across constructs.
- [x] Star vs. the Forces of Evil — v2: **tier 4** (unchanged from v1, score 4.9875, tied with
  Tales from Earthsea/Adventure Time — see re-audit round 2 above). Structural Corruption stays
  up (the Mewman monarchy's genocide history is independent, specific evidence) and Narrative
  Acceptance of Injustice stays up (the finale's specifically bleak critical reception), but
  Structural Despair and Limited Heroism both reverted to Avatar's level once it was clear they'd
  been inflated from that same finale fact rather than independent evidence.
- [x] The Legend of Vox Machina — v2: tier 4 (unchanged from v1, score 4.8375). Scored fresh
  against the rubric, then checked against the full tier 4/5 rosters. TV-MA content (confirmed
  gore, an on-screen torture scene, on-screen child deaths) pushes Explicit Darkness to 3, but
  the Briarwoods' tyranny is one contained, fully-corrected incident (not a recurring saga-wide
  condition like Menzoberranzan in Drizzt) and heroism is consistently, durably effective
  (Whitestone freed and held, all four Chroma Conclave dragons killed, Vecna stopped) — keeps
  every other axis at 1 except Percy's costly Orthax/revenge redemption arc (2). Sits just below
  Fullmetal Alchemist: Brotherhood, which it otherwise nearly matches, differing only on
  Structural Corruption (FMA's genocide is a deep institutional condition; Whitestone's
  usurpation is one corrected incident).

**Tier 5** (4 pending)
- [x] Final Fantasy VI — v2: tier 5 (unchanged from v1, score 5.6625, tied with The Kingkiller
  Chronicle). Distinguishing feature checked against the full tier 5/6 rosters: a literal,
  *completed* world-ending apocalypse mid-story (Kefka's Light of Judgement), not a looming
  threat or backstory — drives Structural Despair to 3 (precedented elsewhere in tier 6: FFXIV,
  FMA 2003, Mistborn, Dark Souls). Kept Limited Heroism and Narrative Acceptance of Injustice
  low (1 each) specifically to avoid double-counting that same apocalypse fact — the *final*
  battle against Kefka is fully decisive, and the plot actively works to reunite the party and
  end the Empire's program rather than leaving injustice unaddressed. Explicit Darkness capped
  at 2 despite real dark content (a suicide attempt, on-screen deaths) since 16-bit sprite-era
  depiction can't deliver the graphic detail the level-3 anchor requires.
- [x] Final Fantasy VII — v2: tier 5 (unchanged from v1, score 5.8875, tied with Harry Potter and
  the Order of the Phoenix/Half-Blood Prince). Shinra's entrenched, planet-wide extraction
  business model drives Structural Corruption to 3 (contrast HP Order of the Phoenix's Umbridge,
  capped at 2 as one year's aberration). Cross-checked against Harry Potter and the Deathly
  Hallows (tier 6): identical profile except Redemption Difficulty (1 vs. 3, Cloud's cleaner
  recovery vs. Snape's decades-long uncredited redemption) — that one well-justified gap accounts
  for the entire tier difference, a good sign the rest of the profile isn't just anchored to a
  convenient neighbor. Aerith's permanent, famous, never-undone death drives Narrative Acceptance
  of Injustice and Explicit Darkness.
- [x] Final Fantasy X — v2: tier 5 (unchanged from v1, score 5.8875, tied with Final Fantasy
  VII/Harry Potter and the Order of the Phoenix/Half-Blood Prince). Sin's thousand-year repeating
  destruction cycle, endured rather than improved for nearly all of Spira's history, drives
  Structural Despair to 3. Yevon's church-and-state fusion — founded on a lie, knowingly
  perpetuating an unnecessary death-cycle to sustain itself — drives Structural Corruption to 3,
  matching the precedent set by Shinra and the Deathly Hallows Ministry. Kept Limited Heroism and
  Narrative Acceptance of Injustice low (1 each): the party's victory is unusually *complete* —
  every prior summoner only achieved temporary calm, but this one permanently ends the cycle.
- [x] Final Fantasy XV — v2: tier 5 (unchanged from v1, score 5.8875, tied with Final Fantasy
  VII/X/Harry Potter and the Order of the Phoenix/Half-Blood Prince). First pass landed tier 6 by
  letting Ardyn's tragic betrayed-healer backstory inflate both Moral Cynicism *and* Narrative
  Acceptance of Injustice toward the same "unresolved" conclusion — corrected by keeping Narrative
  Acceptance of Injustice at 1, since the story's own central conflicts (occupation, the ten-year
  Long Night, Ardyn's threat) are all fully resolved by Noctis's sacrifice; only Ardyn's ancient
  personal grievance stays an unaddressed footnote, not the plot's organizing throughline. The
  Long Night itself (sustained societal near-collapse over a decade) drives Structural Despair to
  3, precedented by Final Fantasy VI/XIV, Mistborn, and Dark Souls.

**Tier 5 backlog complete (4/4).**

**Tier 6** (2 pending)
- [x] Clevatess — v2: tier 6 (unchanged from v1, score 6.1125). Lower-confidence entry than the
  mainstream franchises above (a less widely-covered manga/anime, story ongoing/unresolved) —
  scored partly from the existing summary already in this log rather than fresh primary-source
  detail. Explicit Darkness at 4 (a named character carries an official content warning for
  sustained physical/emotional/sexual abuse, plus infant trafficking and forced transformations)
  is the standout axis. Reconsidered Structural Corruption down to 2 from the v1-era note's
  implied higher weight — a corrupt cardinal reads as one bad actor within the church, not the
  whole institution being irrecoverable — flagged as the axis with the most real uncertainty.
  Redemption Difficulty stays low (1): Clevatess's found-family redemption is explicitly the
  story's more accessible arc, not a costly one.
- [x] Re:Zero − Starting Life in Another World — v2: tier 6 (unchanged from v1, score 6.1125,
  tied exactly with Clevatess). Return by Death — Subaru's genuinely graphic, repeated on-screen
  deaths — is a *central, recurring* structural feature of the entire narrative (Explicit
  Darkness 4, matching Goblin Slayer/Made in Abyss), not an occasional element. Kept Limited
  Heroism low (1): unlike Made in Abyss's Curse of the Abyss (permanent, irreversible harm no
  matter how many attempts), Re:Zero's loop mechanic lets Subaru genuinely undo failures and
  achieve real, lasting fixes — a specific, independent reason for that gap between two otherwise
  similar ED4 entries. Narrative Acceptance of Injustice stays at 2 rather than lower: even though
  the "final" timeline resolves most crises, Subaru alone carries the real, unresolved
  psychological weight of every failed loop.

**Tier 6 backlog complete (2/2).**

**v2 Rescoring Backlog: 100% complete** — all 92 of 92 catalog works are now scored under v2 (see
`Fantasy_Grimdark_Scale_v2_WIP.xlsx`). Märchen Crown, the last holdout (previously skipped for low
confidence), was resolved via a dedicated multi-language research pass — see its entry above.

## v2 promoted to the live site

`index.html` and `es/index.html` now display v2 tiers/scores for all 92 works, replacing the v1
data that had been live throughout this entire backlog pass. Mechanics of the promotion:

- Matched each of the 87 existing HTML list items to its v2 row by title, preserving all existing
  EN/ES title, medium, and creator text unchanged — only the tier placement and displayed score
  changed for these.
- Two v1 entries had been split into multiple v2 entries during the backlog (documented above):
  "Final Fantasy I, II & XII" → 3 separate entries, "Neverwinter Nights & Baldur's Gate I–III" → 4
  separate entries. These 7 needed new individual list items generated (EN/ES title, medium,
  creator) rather than a straight tier/score swap — video game titles kept identical across
  languages per the site's existing convention; Baldur's Gate III credited to Larian Studios alone
  (not the bundle's collective "BioWare & Black Isle & Larian" credit) since it's a genuinely
  different developer from the earlier games in the series.
- 87 - 2 (removed bundles) + 7 (their split replacements) = 92, reconciling exactly with the full
  catalog.
- Tier 7 dropped from 2 works (Tanya, Berserk) to 1 (Berserk only — Tanya's v2 rescore already
  landed it in tier 6) and now uses the "solo" single-item centered layout, matching tiers 9/10.
- Updated the "73 fantasy books" catalog-size mentions (4 each in the EN/ES `<meta>`/JSON-LD tags)
  to 92.
- Verified: exactly 92 works render per language, correctly distributed and sorted by score within
  each tier; no console errors; spot-checked the tier 6/7/8/10 boundaries and the Baldur's Gate/
  Final Fantasy split entries visually in-browser before committing.

## Post-promotion corrections

Fixes to already-live entries, found and corrected after the v2 promotion above.

**Berserk** — flagged by the user as looking too low (tier 7, 7.4625) once Attack on Titan was
added alongside it. The original score had **no documented reasoning at all** — just a bare list
of numbers in SCORING_RECORD.md, unlike every other entry — a strong sign it predated the
disciplined process used throughout the rest of this project, the same root cause that made The
Nightmare Before Christmas wrong. Re-derived from scratch: Limited Heroism revised 2→3 (Guts
never achieves a lasting structural win against Griffith/the God Hand across 40+ volumes) and
Narrative Acceptance of Injustice revised 2→3 (Casca's trauma stays unresolved for a massive
span of the story) — both on distinct, specific evidence, not a reflexive across-the-board bump.
Structural Corruption was tested at 3 (for the Holy See/Conviction arc) but held at 2 after
checking against A Song of Ice and Fire's own documented reasoning, which specifically requires
multi-institutional corruption ("the Iron Throne, the Faith, and the Great Houses are *all*
deeply compromised") — Berserk's corruption is real but concentrated in one arc. **Result: Tier
8 (Grimdark)**, score 8.1375, up from Tier 7 — moving Berserk out of Tier 7 and leaving Attack on
Titan alone there, back to the "solo" single-item layout. Full reasoning in SCORING_RECORD.md.

**Systematic sweep for the same signature.** Berserk's fix prompted a full search of
SCORING_RECORD.md for the same tell (bare numbers, zero explanatory text). Found 7 more: Kiki's
Delivery Service, Ponyo, and Warhammer 40,000 were confirmed *not* concerning (all-zero and
all-four floor/ceiling cases genuinely don't need reasoning — there's nothing to explain). The
other four were re-audited from scratch:

- **Dark Souls I–III** — this one already carried an explicit self-flag ("likely inconsistency
  ... compared against Elden Ring ... left as-is at the user's request"). Re-derived: Limited
  Heroism, Moral Cynicism, Structural Corruption, and Narrative Acceptance of Injustice all
  revised 2→3 on distinct, specific evidence (both endings are deliberately unsatisfying by
  design; Anor Londo's gods deceive their own citizens; at least two distinct corrupt
  institutions; neither ending resolves the cyclical doom). **Result: Tier 8**, score 8.25, up
  from Tier 6 (6.9).
- **Tales from Earthsea** — Explicit Darkness revised 2→3 (Arren's opening patricide, Therru's
  sustained visible abuse-scarring push past typical Ghibli restraint). **Result: Tier 5**, score
  5.2125, up from Tier 4 (4.988).
- **The Kingkiller Chronicle** — reviewed and held. Two revisions tested (Moral Cynicism for
  Ambrose's impunity; Limited Heroism for the frame narrative's implied future catastrophe),
  both rejected — the first doesn't overcome Kvothe's consistently-rewarded virtue as the
  dominant thread, the second would score based on an unwritten third book rather than the two
  published ones.
- **Grimgar: Ashes and Illusions** — reviewed and held. A Narrative Acceptance of
  Injustice/Redemption Difficulty trade tested and rejected — the two moves cancel out almost
  exactly, not worth the edit.

Full reasoning for all four in SCORING_RECORD.md.

## Post-promotion corrections (continued)

**The Stormlight Archive** — flagged by the user as suspiciously low once compared against
Attack on Titan. The original score only reflected content through roughly the early series
(caste system, Kaladin's depression, Dalinar's massacre); it didn't account for later-book
escalations: Oathbringer's reveal that the entire human presence on Roshar was built on
enslaving the native Singers (not just the caste system), Taravangian's hospital-murder
atrocities and eventual ascension to the setting's greatest power via ruthless pragmatism,
Teft's addiction/death in Rhythm of War, and Wind and Truth's ending — Dalinar dies, and Odium
is only driven off, not defeated, with the text explicit that Roshar must now "prepare for the
next conflict." Re-derived against the full 5-book published series: Limited Heroism revised
2→3 (the ending buys time rather than resolving the threat) and Narrative Acceptance of
Injustice revised 2→3 (the core conflict is textually deferred to an unwritten future era, not
resolved within this arc); Structural Corruption held at 3 but now much better-supported by the
slavery reveal. **Result: Tier 7 (Extreme Dark Fantasy)**, score 7.575, up from Tier 6 (6.9) —
joins Attack on Titan (7.8), ending that tier's "solo" layout.

Bundling check: considered splitting into 5 per-book entries (matching the Harry Potter
convention) since rough per-book estimates showed a real spread (roughly Tier 5 to Tier 7).
Rejected: the spread is non-monotonic (it dips back down at Rhythm of War rather than climbing
steadily book over book like Harry Potter does), and unlike Harry Potter there's no
"different audience" gap — even the first book (The Way of Kings) is already adult-register
dark fantasy (on-page regicide, slavery, suicidal ideation). Kept as one bundled entry, matching
the A Song of Ice and Fire / The First Law precedent for ongoing single-narrative series. Full
reasoning in SCORING_RECORD.md.

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
15. [x] Labyrinth (1986 film, dir. Jim Henson, David Bowie — a goblin king, a labyrinth, a stolen baby brother) — DONE, see Completed
16. [x] Pan's Labyrinth / El laberinto del fauno (2006 film, dir. Guillermo del Toro — a girl's dark fairy tale amid Falangist Spain) — DONE, see Completed
17. [x] Attack on Titan (Shingeki no Kyojin) — Hajime Isayama — Manga, Anime — DONE, see Completed
18. [x] Maleficent (2014 film, Angelina Jolie — Sleeping Beauty retold from the villain's side) — DONE, see Completed
19. [x] (Des)encanto / Disenchantment (2018 TV series, Matt Groening) — DONE, see Completed
20. [x] Calabozos y dragones / Dungeons & Dragons (1983 animated TV series) — DONE, see Completed
21. [x] The Magicians — Lev Grossman — Novels, TV series — DONE, see Completed
22. [x] House of the Dragon — DONE, see Completed
23. [x] A Knight of the Seven Kingdoms (Dunk & Egg) — George R. R. Martin — Novellas — DONE, see Completed
24. [x] Once Upon a Time (TV series) — DONE, see Completed
25. [x] The Shannara Chronicles — based on Terry Brooks' novels — TV series — DONE, see Completed
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
43. [ ] The Mighty Nein — Critical Role (Campaign 2) — TV series / D&D actual-play — Amazon's
    animated adaptation of Critical Role's second campaign, following on from The Legend of Vox
    Machina (Campaign 1, already in the catalog at Tier 4); a found-family of outcasts and
    monster hunters in a morally grayer, more politically complex setting than Campaign 1's,
    with trauma-centered arcs (Caleb's guilt over his role in his parents' deaths, Nott/Veth's
    identity and addiction arc)
44. [ ] Goblins — Thunt (Tarol Hunt) — Webcomic — https://www.goblinscomic.org/ — began as a
    joke inverting standard D&D "kill goblins for XP" tropes, following a goblin warband trying
    to survive being slaughtered by adventurers for loot; the tone shifts dramatically over its
    run into genuine tragedy (PTSD, addiction, on-page major character deaths), repeatedly
    questioning who the real "monsters" in the story actually are

## Completed

### 25. The Shannara Chronicles — Terry Brooks — TV series

- Tier 4 (Fantasy in Gray Tones), Final Score 4.875 (Weighted Internal Score 1.5) — an exact
  numeric tie with Final Fantasy IX, The Boy and the Heron, Ranking of Kings, and Fullmetal
  Alchemist: Brotherhood, via a genuinely different profile from each (see neighbor check
  below).
- Scores: Structural Despair 1, Limited Heroism 1, Moral Cynicism 1, Structural Corruption 2,
  Redemption Difficulty 1, Narrative Acceptance of Injustice 2, Explicit Darkness 3.
- Rationale: 2 seasons (MTV 2016, Spike/Paramount Network 2017) adapting the opening books of
  Terry Brooks' Shannara series, set in the post-apocalyptic far-future "Four Lands" (visible
  ruins of cars and helicopters mark the setting as Earth after an implied nuclear-era
  cataclysm, "the Great Wars"). Season 1 (The Elfstones of Shannara) ends with Amberle's full
  self-sacrifice — becoming the new Ellcrys tree to seal the demon army out — a complete,
  durable fix; Season 2 (loosely The Wishsong of Shannara) ends with Wil killing the Warlock
  Lord outright, another decisive resolution. Both season-level threats support the tier-4 norm
  of Limited Heroism 1 and Moral Cynicism 1 (classic quest-fantasy causality — critics
  specifically pitched the show as "epic, colourful... for those tired of the unrelenting
  grimness of Game of Thrones," despite real on-screen violence). Structural Corruption reaches
  2 on real institutional grounds distinct from Once Upon a Time's individually-anomalous
  corrupt rulers (also Tier 4, SC1): the Crimson is an organized, popularly-backed paramilitary
  force built specifically to hunt, intimidate, and kill magic-users out of institutionalized
  fear — a coherent persecution apparatus, not one usurper to be corrected. Narrative Acceptance
  of Injustice reaches 2 for a specific, documented reason: the show was cancelled after its
  season 2 finale (which doubled as the unplanned series finale) with no season 3, so while the
  season's direct villain (the Warlock Lord) is defeated, the deeper Crimson persecution
  thread only gets a tactical alliance ("join us against a common enemy"), never an actual
  reckoning with the underlying bigotry — an injustice left genuinely unresolved, not a
  narrative choice to leave it ambiguous. Explicit Darkness sits at 3 on reviewer-documented
  evidence: multiple critics called the swordplay "kind of gorey" and questioned why a TV-14
  rating applied rather than TV-MA, and the season 2 finale alone kills four major characters
  (Allanon, King Ander, Queen Tamlin, General Riga — the last by on-screen decapitation-style
  violence at the Warlock Lord's hands).
- Cozy Fantasy = No. Hopepunk = No: the Crimson is real institutional persecution, but the
  show's throughline is a love-triangle-and-quest coming-of-age story, not an oppressed group's
  organized resistance to that persecution (the Fierce Hopepunk shape, e.g. Avatar) — and the
  Crimson thread never gets the genuine reckoning that shape requires, partly because
  production ended first.
- Scored against both aired seasons in full, noting the cancellation openly rather than
  guessing at an unmade season 3's resolution.
- Neighbor check: compared against the four other works tied at exactly 4.875 — none share an
  identical per-axis profile (checked specifically after the Once Upon a Time session's
  FMA:B near-miss). Fullmetal Alchemist: Brotherhood's Redemption Difficulty 2 (Scar's and
  Mustang's costly, sustained guilt arcs) sits above this entry's Redemption Difficulty 1
  (Eretria's demon-blood struggle stays underdeveloped, again a casualty of cancellation) while
  this entry's Narrative Acceptance of Injustice 2 sits above FMA:B's 1 — a clean swap. Ranking
  of Kings' Redemption Difficulty 0 (a growth-and-earned-respect story, not a sinner-redeemed
  one) trades against its Structural Despair 2 vs. this entry's 1. Checked further against
  Once Upon a Time (4.20, Tier 4, added earlier this session): Shannara scores meaningfully
  higher specifically via Structural Corruption (2 vs. 1 — a real organized persecution militia
  vs. OUAT's individually-anomalous corrupt rulers) and Narrative Acceptance of Injustice (2 vs.
  1 — Shannara's persecution thread stays genuinely open; OUAT's finale resolves nearly
  everything), offset by Redemption Difficulty (1 vs. 2, OUAT's Regina/Rumpelstiltskin arcs are
  far more central and costly) and Moral Cynicism (1 vs. 0, OUAT's True Love's Kiss is a more
  explicit reward-mechanic than anything in Shannara) — a sensible, evidence-based ordering
  rather than a coincidence. Label check: "Fantasy in Gray Tones (high stakes, real losses, but
  still high hope)" fits — real character deaths and an unresolved persecution thread sit
  alongside a classic, decisively-won heroic quest structure.
- Added to xlsx row 104, and to tier 4 on both index.html and es/index.html, inserted
  immediately after The Legend of Vox Machina (4.84) and before Final Fantasy IX (4.88) per
  score order; title "The Shannara Chronicles" in EN, "Las crónicas de Shannara" in ES (the
  standard Latin American/Spain title); creator credited as "Terry Brooks" (the source novels'
  author, matching the House of the Dragon precedent of crediting the original literary IP for
  a TV adaptation entry); medium: "TV series" / "Serie de TV". Updated the Summary sheet's
  tier-4 count (17 → 18) and total-scored count (102 → 103 of 103). Updated the catalog-size
  mentions in both pages' meta/JSON-LD description tags (102 → 103).

### 24. Once Upon a Time — Edward Kitsis & Adam Horowitz — TV series

- Tier 4 (Fantasy in Gray Tones), Final Score 4.20 (Weighted Internal Score 1.2) — an exact
  numeric tie with The NeverEnding Story, via a genuinely different profile (see neighbor check
  below), not a copy.
- Scores: Structural Despair 1, Limited Heroism 1, Moral Cynicism 0, Structural Corruption 1,
  Redemption Difficulty 2, Narrative Acceptance of Injustice 1, Explicit Darkness 3.
- Rationale: 7 seasons (2011-2018) built around fairy-tale characters cursed into the small
  town of Storybrooke, with the show's own explicit mission statement — Henry's line "you're
  going to bring back the happy endings" — as close to a textual thesis statement as this scale
  has seen. Moral Cynicism sits at the scale's floor (0) on unusually strong textual grounds:
  True Love's Kiss is literal, explicit, consistently-applied in-universe magical law that
  breaks any curse, matching anchor 0's "goodness and cooperation are rewarded consistently and
  explicitly" almost exactly rather than the more general "acting well usually works out" of
  anchor 1. Redemption Difficulty is the profile's clear outlier at 2: virtually every major
  villain (Regina, Rumpelstiltskin, Hook, Zelena) gets a real redemption arc, and the show
  insists redemption is reachable "no matter how far you've fallen" — but reachable is not
  free. Regina's arc spans all 7 seasons with dramatized, specific costs (years without Henry's
  trust, eventually literally splitting off and destroying her own Evil Queen persona to purge
  her darkness), and Rumpelstiltskin backslides for 300 years before his arc resolves only in
  his own finale death — real loss/pain/renunciation, the anchor-2 bar, not just "genuine effort
  that succeeds" (anchor 1). Structural Corruption stays low (1): the various corrupt regimes
  across the show's many fairy-tale kingdoms (Cora's Wonderland, Zelena's Oz, King George's
  court) are each individually legitimate monarchies temporarily seized by an anomalous
  villain and then corrected — not one coherent institution built by design to oppress, so this
  stays a tier below the "notorious corruption in a central institution" bar of SC2. Explicit
  Darkness reaches 3 on real evidence, not just genre reputation: the Parents Television
  Council's own tracked count across sweep periods logged 37 deaths, 4 dismemberments, and 261
  acts of violence, and heart-ripping — literally tearing a beating heart from someone's chest
  to control or kill them — recurs as the show's single most central and frequently-used dark
  magical device across the entire run, plus a full season set in the literal Underworld.
- Cozy Fantasy = No. Hopepunk = No: unlike Avatar (also Tier 4, Hopepunk = Yes), Once Upon a
  Time's shape isn't an oppressed group mounting organized resistance to a systemic power — it's
  individual moral journeys and family reunion, which is why Structural Corruption stays low
  rather than reading as real institutional oppression.
- Scored against the complete 7-season series, source-consistent with the finale ("Leaving
  Storybrooke") giving nearly every character, including several redeemed former villains, an
  explicit happy ending.
- Neighbor check: initially derived to an identical per-axis match with Fullmetal Alchemist:
  Brotherhood (also Tier 4) — flagged as the exact uniform-default pattern this log warns
  against, and re-examined rather than accepted. On reflection, FMA:B's Structural Corruption 2
  reflects Amestris as one coherent nation built by a hidden cabal specifically to harvest its
  population, a much harder institutional-design case than Once Upon a Time's pattern of
  individually-legitimate kingdoms seized by anomalous usurpers — and FMA:B has no equivalent to
  True Love's Kiss's explicit reward-mechanic. Revised Structural Corruption 2 to 1 and Moral
  Cynicism 1 to 0 on that basis, landing instead on an exact tie with The NeverEnding Story
  (4.20) via a materially different shape: NES's Structural Despair 2 (the Nothing actively
  consuming Fantasia through most of the story) trades against this entry's Narrative Acceptance
  of Injustice 1 (recurring but individually-resolved injustices, rather than NES's fully-undone
  single threat), and NES's Structural Corruption 0 trades against this entry's Moral Cynicism
  0 — two independent, textually-grounded swaps landing on the same total, not a coincidence of
  identical inputs. Checked further against a tonally distant non-adjacent Tier 4 work, Star vs.
  the Forces of Evil (4.9875, near the tier ceiling): it out-scores this entry specifically via
  a real institutional-oppression backdrop (the Mewman genocide against Monsters, Structural
  Corruption 2) and a more unresolved ending (the Rumbling-adjacent "erase the system" finale,
  Narrative Acceptance of Injustice 2), while this entry compensates with higher Explicit
  Darkness (3 vs. 2) from its sustained on-screen violence — a sensible, non-arbitrary ordering.
  Label check: "Fantasy in Gray Tones (high stakes, real losses, but still high hope)" is a
  near-literal description of the show's own reputation and stated thesis.
- Added to xlsx row 103, and to tier 4 on both index.html and es/index.html, inserted
  immediately after The NeverEnding Story per score order (exact tie); title "Once Upon a Time"
  in EN, "Érase una vez" in ES (the standard Latin American/Spain title used since 2016); medium:
  "TV series" / "Serie de TV". Updated the Summary sheet's tier-4 count (16 → 17) and
  total-scored count (101 → 102 of 102). Updated the catalog-size mentions in both pages'
  meta/JSON-LD description tags (101 → 102).

### 23. A Knight of the Seven Kingdoms (Dunk & Egg) — George R. R. Martin — Novellas

- Tier 5 (Gloomy Fantasy), Final Score 5.2125 (Weighted Internal Score 1.65) — an exact numeric
  tie with Tales from Earthsea, landing as a new member of the tier's floor cluster (also
  Dragonlance, Harry Potter and the Goblet of Fire, Elantris, Baldur's Gate III), inserted
  immediately after Tales from Earthsea.
- Scores: Structural Despair 2, Limited Heroism 1, Moral Cynicism 1, Structural Corruption 2,
  Redemption Difficulty 1, Narrative Acceptance of Injustice 2, Explicit Darkness 3.
- Rationale: covers the three published novellas (The Hedge Knight, The Sworn Sword, The
  Mystery Knight), set ~90 years before A Song of Ice and Fire and following the hedge knight
  Ser Duncan the Tall and his squire Egg (the future King Aegon V, in disguise). Scored as a
  distinctly lighter corner of the same fictional universe as A Song of Ice and Fire (Tier 8,
  8.475) and House of the Dragon (Tier 7, 7.80), not a copy of either: Dunk's own heroism is
  genuinely effective and durable in all three stories — he wins his trial of seven outright
  (Limited Heroism, Moral Cynicism both 1), the Coldmoat water feud resolves via reconciliation
  rather than bloodshed, and the Whitewalls Blackfyre conspiracy is crushed before it can become
  a war — a cleaner record of structural fixes than either ASOIAF parent work, whose wars grind
  on or end only through mutual attrition. Set against that: the setting's justice system is
  literally trial-by-combat (a prince who maims a commoner performer faces the same violent
  contest as the hedge knight who struck him in her defense), and Bloodraven's fear-based rule
  (an impaled dissenter's head opens The Mystery Knight) is real, if contained, institutional
  corruption — Structural Corruption 2, not the multi-institution 3 that ASOIAF/House of the
  Dragon's Iron Throne-and-Faith-and-Great-Houses bar requires. Narrative Acceptance of
  Injustice sits at 2: the immediate plot crises each resolve, but the birth-based two-tier
  legal system and Aerion Brightflame's unpunished cruelty are never addressed by the text
  itself. Explicit Darkness reaches 3 on the strength of several distinct graphic on-page
  moments across the three novellas (Aerion breaking a puppeteer's finger and beating her, a
  laborer's face slashed open, Prince Baelor's skull caved in and his on-page death in Dunk's
  arms, Dunk himself beaten half to death) rather than one isolated beat.
- Cozy Fantasy = No. Hopepunk = No: Dunk's personal decency is real but the story never
  organizes around resisting the two-tier justice system as its throughline (unlike Fierce
  Hopepunk precedent such as Avatar/Korra) — he works within the system and wins personally
  rather than reforming it.
- Neighbor check: the exact-tie floor cluster (Tales from Earthsea, Dragonlance, Harry Potter
  and the Goblet of Fire, Elantris, Baldur's Gate III — all 5.2125) each differ from this
  profile on two axes that trade off in opposite directions (e.g. Earthsea's Structural
  Corruption 1/Redemption Difficulty 2 vs. this entry's 2/1 — Earthsea's corruption is
  "personal/mythic, not institutional" while Arren's patricide-recovery arc is a much costlier
  redemption than Eustace's), confirming a genuinely differentiated shape rather than a
  copy-paste default that happens to land on the same total. Checked further up the tier
  against a non-adjacent work, The Magicians (5.8875, the tier's ceiling): it out-scores this
  entry specifically on Limited Heroism, Moral Cynicism, and Redemption Difficulty (real
  depression/addiction themes, less decisive resolutions) while matching it on Structural
  Corruption and Explicit Darkness — a sensible within-tier ordering, since Dunk & Egg earns
  its place through contained heroic triumphs against a real institutional-injustice backdrop,
  while The Magicians earns its higher position through deeper psychological cynicism. Label
  check: "Gloomy Fantasy" fits — the tier's own definition ("a genuinely corrupt central
  institution... is the norm here, but most of these are still 'good triumphs' stories, the
  cost is real and visible") is close to a direct description of this entry's actual shape.
- Scored against the three published, collected novellas only (The Hedge Knight, The Sworn
  Sword, The Mystery Knight, as gathered in the *A Knight of the Seven Kingdoms* omnibus) — the
  fourth story, "The She-Wolves of Winterfell," remains unpublished as of this entry.
- Medium includes the HBO TV adaptation: Season 1 ("The Hedge Knight," 6 episodes) aired
  Jan 18 – Feb 22, 2026, and showrunner Ira Parker has stated the guiding rule is "I really
  wouldn't create story" — no reported content divergence that would change the darkness
  profile, so treated as the same content as the source novella rather than rescored
  separately, matching the precedent set for other novel-plus-faithful-adaptation entries
  (e.g. The Saga of Tanya the Evil, The Witcher). Season 2 (The Sworn Sword, with some
  Martin-approved expansion) is in production for an early-2027 release — not yet aired, so not
  factored in.
- Added to xlsx row 102, and to tier 5 on both index.html and es/index.html, inserted
  immediately after Tales from Earthsea per score order (exact tie, 5.21 displayed); title "A
  Knight of the Seven Kingdoms (Dunk & Egg)" in EN, "El caballero de los Siete Reinos (Dunk y
  Egg)" in ES (the official Spanish omnibus title, "Cuentos de Dunk y Egg: El caballero de los
  Siete Reinos"); medium: "Novellas, TV series" / "Novelas cortas, Serie de TV". Updated the
  Summary sheet's tier-5
  count (20 → 21) and total-scored count (100 → 101 of 101). Also corrected a stale "99 fantasy
  books" catalog-size mention in both pages' meta/JSON-LD description tags (last updated during
  the v2 promotion, not kept current through the two additions since) to 101.

### 22. House of the Dragon — George R. R. Martin — TV series

- Tier 7 (Extreme Dark Fantasy), Final Score 7.80 (Weighted Internal Score 2.8) — ties Attack
  on Titan exactly on total, via a genuinely different profile (differs on four of seven axes:
  Structural Despair, Limited Heroism, Structural Corruption, Narrative Acceptance of Injustice).
- Scores: Structural Despair 2, Limited Heroism 3, Moral Cynicism 3, Structural Corruption 2,
  Redemption Difficulty 3, Narrative Acceptance of Injustice 3, Explicit Darkness 4.
- Rationale: scored against the complete Dance of the Dragons history as GRRM wrote it in *Fire
  & Blood*, which the show is faithfully adapting (the TV series itself is still airing). The
  central throughline is A Song of Ice and Fire's own thesis in miniature: Rhaenyra's legally
  decreed, legitimate claim is stripped from her by ruthless court maneuvering (Otto and Alicent
  Hightower's coup while Viserys's body is still warm), not by any failure of virtue — a direct
  match to A Song of Ice and Fire's own "honor is systematically punished" reasoning, hence
  Moral Cynicism 3. Every character who tries to prevent the war (Viserys's decree, Rhaenyra's
  and Alicent's own late peace overture) fails, and the war "ends" through mutual attrition
  (both claimant lines gutted, dragons driven to near-extinction) rather than any structural fix
  — a stronger case for Limited Heroism 3 than Attack on Titan's LH2 (which achieves a genuine,
  lasting peace). Redemption is attempted but doesn't land: Alicent's late remorse comes too
  late to stop the war, and Daemon's Harrenhal reckoning doesn't durably change him — Redemption
  Difficulty 3. The core injustice (a father's explicit decree overridden by succession
  politics that favor a male claimant) is never resolved in-story; it stands as the seed of the
  Targaryen dynasty's further, already-chronicled decline — Narrative Acceptance of Injustice 3.
  Explicit Darkness sits at the ceiling: Aemma's forced, unanesthetized cesarean death in the
  premiere, Blood and Cheese's on-page child murder, and Lucerys/Arrax being devoured alive by
  Vhagar are graphic, shocking, and part of a sustained pattern, not incidental beats — matching
  Attack on Titan and A Song of Ice and Fire's own ED4 bar. Weighed against the full A Song of
  Ice and Fire (Tier 8, 8.475): this is a single dynasty's succession war, not a world where the
  Iron Throne, the Faith, and the Great Houses are *all* independently corrupt, and it lacks the
  Long Night's civilization-ending cosmology — Structural Despair and Structural Corruption both
  stay at 2 rather than 3, keeping it a clear tier below its parent work.
- Cozy Fantasy = No. Hopepunk = No: no work at Tier 6 or darker carries the tag on this scale,
  and this is a tragedy about power and succession, not kindness as an organizing response to
  adversity.
- Added to xlsx row 101, and to tier 7 on both index.html and es/index.html, appended after
  Attack on Titan per score order (tied at 7.80); title "House of the Dragon" in EN, "La Casa
  del Dragón" in ES (the official HBO Max Latino title); medium: "TV series" / "TV". Updated the
  Summary sheet's tier-7 count (2 → 3) and total-scored count (99 → 100 of 100).

### 21. The Magicians — Lev Grossman — Novels, TV series

- Tier 5 (Gloomy Fantasy), Final Score 5.8875 (Weighted Internal Score 1.95) — ties Harry Potter
  and the Half-Blood Prince/Order of the Phoenix and Final Fantasy VII/X/XV.
- Scores: Structural Despair 1, Limited Heroism 2, Moral Cynicism 2, Structural Corruption 2,
  Redemption Difficulty 2, Narrative Acceptance of Injustice 2, Explicit Darkness 3.
- Rationale: an explicit subversion of Narnia-style portal fantasy — magic and power don't cure
  Quentin's depression, and real trauma (Julia's rape by the trickster god Reynard; Martin
  Chatwin's implied childhood sexual abuse, which turns him into the story's central monster)
  lands on good characters without narrative justification. Weighed against that: Brakebills
  itself is a basically legitimate institution (not corrupt by design), heroism achieves real,
  lasting wins (the Beast is defeated, Fillory is saved), and the novels resolve toward genuine
  hope (a new magical realm, lasting peace) even though the TV adaptation deliberately refuses
  that same closure for Quentin. Bundling check: estimated the novels and the Syfy TV series
  separately (~Tier 5 vs. ~Tier 6) given their real tonal divergence, but the gap is only 1 tier —
  smaller than the 2+ tier gaps that drove the Final Fantasy I/II/XII, Baldur's Gate, and
  Fullmetal Alchemist splits — so kept as one bundled entry.
- Cozy Fantasy = No. Hopepunk = No.
- Added to xlsx row 100, and to tier 5 on both index.html and es/index.html, appended after the
  existing 5.89 cluster (Harry Potter Half-Blood Prince/Order of the Phoenix, Final Fantasy
  VII/X/XV) per score order; title "The Magicians" in EN, "Los Magos" in ES (the established
  Spanish-language publisher title); medium: "Novels, TV series" / "Novelas, Serie de TV".

### 20. Dungeons & Dragons (1983) — Marvel Productions / TSR — TV Series

- Tier 2 (Bright Fantasy), Final Score 2.7375 (Weighted Internal Score 0.55) — matches A
  Conspiracy of Truths exactly. Title carries a "(1983)" suffix to distinguish it from
  "Dungeons & Dragons: Honor Among Thieves" (2023 film, already in the catalog at Tier 2).
- Scores: Structural Despair 0, Limited Heroism 1, Moral Cynicism 0, Structural Corruption 0,
  Redemption Difficulty 0, Narrative Acceptance of Injustice 2, Explicit Darkness 1.
- Rationale: classic, restrained Saturday-morning-cartoon content on every axis except one — the
  show's defining, often-remarked-on quality is that its central promise (getting the six kids
  home) is never fulfilled, since the series was cancelled before a planned resolution could
  air. Episode-level conflicts against Venger resolve cleanly each time, but that core injustice
  never does, driving Narrative Acceptance of Injustice to 2 while every other axis stays at
  genre-typical low values.
- Cozy Fantasy = No. Hopepunk = No.
- Added to xlsx row 19, and to tier 2 on both index.html and es/index.html (title: "Calabozos y
  Dragones" in ES, the established Latin American title — "Dungeons & Dragons (1983)" in EN;
  medium: "TV").

### 19. Disenchantment (2018) — Matt Groening — TV Series

- Tier 4 (Fantasy in Gray Tones), Final Score 4.3125 (Weighted Internal Score 1.25) — matches
  Witch Hat Atelier/Baldur's Gate II: Shadows of Amn.
- Scores: Structural Despair 1, Limited Heroism 1, Moral Cynicism 1, Structural Corruption 2,
  Redemption Difficulty 1, Narrative Acceptance of Injustice 1, Explicit Darkness 2.
- Rationale: real institutional darkness (Zog's cruel, incompetent monarchy; Dagmar's
  manipulative secret society scheming across the whole series) and genuine dark content
  (Elfo's on-screen death, elf-blood-harvesting for immortality potions, Dagmar's
  stone-transformation), all softened by Groening's fundamentally comedic, satirical register
  and exaggerated animation style — real but not graphic, and mostly resolved with effort
  rather than left permanent.
- Cozy Fantasy = No. Hopepunk = No.
- Added to xlsx row 44, and to tier 4 on both index.html and es/index.html (title:
  "(Des)encanto" in ES, the Latin American title — "Disenchantment" in EN; medium: "TV").

### 18. Maleficent (2014) — Robert Stromberg — Film

- Tier 3 (Moderately Bright Fantasy), Final Score 3.3 (Weighted Internal Score 0.8) — matches
  Cormyr/Dungeon Meshi.
- Scores: Structural Despair 0, Limited Heroism 0, Moral Cynicism 1, Structural Corruption 1,
  Redemption Difficulty 1, Narrative Acceptance of Injustice 1, Explicit Darkness 2.
- Rationale: a contained personal betrayal/revenge/redemption story rather than a broader
  societal decline — the resolution is genuinely complete (the two kingdoms are united under
  Aurora's rule, arguably stronger than the pre-conflict status quo). Stefan's betrayal
  (mutilating the woman who loved him for a crown) and his subsequent paranoid tyranny are real
  but isolated, fully corrected by the ending. The wing-mutilation scene (widely read as a
  sexual-assault allegory) carries real thematic weight but stays within Disney/PG depiction
  restraint, keeping Explicit Darkness at 2 rather than 3.
- Cozy Fantasy = No. Hopepunk = No — a personal betrayal/redemption arc, not a
  resistance-to-oppression or mortality-themed shape.
- Added to xlsx row 28, and to tier 3 on both index.html and es/index.html, inserted alongside
  Cormyr/Dungeon Meshi (title: "Mal&#233;fica" in both EN and ES pages' ES version — the same
  title is used in both Spain and Latin America; medium: "Pel&#237;cula" / "Film").

### 17. Attack on Titan (Shingeki no Kyojin) — Hajime Isayama — Manga / Anime

- **Update:** Berserk was re-audited shortly after this entry and moved to Tier 8 (see its own
  entry below) — tier 7 is now solo again with Attack on Titan alone, not the grid layout
  described below at the time.
- Tier 7 (Extreme Dark Fantasy), Final Score 7.8 (Weighted Internal Score 2.8) — at the time,
  joined Berserk, which returned tier 7 to the standard grid layout (no longer a "solo"
  single-item tier).
- Scores: Structural Despair 3, Limited Heroism 2, Moral Cynicism 3, Structural Corruption 3,
  Redemption Difficulty 3, Narrative Acceptance of Injustice 2, Explicit Darkness 4.
- Rationale: first pass landed tier 8 (an exact profile match for A Song of Ice and Fire) by
  defaulting to maximum severity across every axis — the same trap caught before in Märchen
  Crown. Corrected by checking each axis against real tier 6-8 precedent: Limited Heroism and
  Narrative Acceptance of Injustice both pulled back from 3 to 2, since the ending achieves a
  genuine, hard-won structural peace (the Rumbling stopped, real diplomatic reform, cross-ethnic
  reconciliation) rather than "even the biggest wins are insufficient" — matching Berserk/Dark
  Souls/Stormlight's profile shape on those two axes rather than A Song of Ice and Fire's. The
  axes that held up under scrutiny (Structural Despair 3, Moral Cynicism 3, Redemption
  Difficulty 3, Explicit Darkness 4) all have specific, distinct textual support, not a uniform
  default. Structural Corruption 3 — two distinct, thoroughly corrupt institutions (Marley's
  genocide-apparatus of ghettos/branding/child soldiers, and Eldia's own memory-erasure
  brainwashing of its people) — is specifically what pushes this above Berserk, whose evil is
  more cosmic/personal than institutional; the two profiles are otherwise identical.
- Cozy Fantasy = No. Hopepunk = No — matches precedent; no work at tier 6 or darker carries the
  tag on this scale.
- Added to xlsx row 91, and to tier 7 on both index.html and es/index.html, inserted above
  Berserk by score (title: "Ataque a los Titanes" in ES, the standard Latin American title —
  "Attack on Titan" in EN; medium: "Manga, Anime").

### 16. Pan's Labyrinth (2006) — Guillermo del Toro — Film

- Tier 6 (Dark Fantasy), Final Score 6.45 (Weighted Internal Score 2.2) — tied exactly with
  Made in Abyss. Scored directly under v2 methodology (no v1 predecessor).
- Scores: Structural Despair 2, Limited Heroism 2, Moral Cynicism 2, Structural Corruption 3,
  Redemption Difficulty 0, Narrative Acceptance of Injustice 3, Explicit Darkness 4.
- Rationale: Captain Vidal's Francoist military apparatus is thoroughly corrupt (torture,
  extrajudicial killing of innocents, a commander who views his own wife purely as a vessel
  for a male heir), and the film is among the most graphically intense in the catalog (the
  bottle-torture/murder scene, the Pale Man's child-eating horror, Vidal's unflinching
  self-surgery). Against that: Ofelia's moral integrity — refusing to harm her infant brother
  even under lethal threat — is the film's real thematic center, not despair for its own sake,
  and the story deliberately keeps Moral Cynicism ambiguous rather than committing to a purely
  cynical reading (her death is framed, in the mythic register, as meaningful rather than
  senseless). Checked against Berserk (Tier 7): Pan's Labyrinth's lower Moral Cynicism and
  Redemption Difficulty (0, since no wrongdoer here earns back moral standing — Vidal never
  redeems, and Ofelia isn't a wrongdoer needing repair) keep it a full tier below, appropriately
  — a tightly-constructed single film with a clear redemptive payoff, not an open-ended
  chronicle of escalating despair.
- Cozy Fantasy = No. Hopepunk = No — Ofelia's disobedience-as-virtue doesn't fit Fierce
  (no organized resistance she's part of) or Bittersweet (her death isn't framed as an
  existential-mortality theme chosen knowingly, the way Frieren's is) cleanly enough to tag.
- Added to xlsx row 80, and to tier 6 on both index.html and es/index.html, inserted right
  before Made in Abyss's former position, now sharing its exact score (title: "El laberinto del
  fauno" in ES, the standard title in both Spain and Latin America — "Pan's Labyrinth" in EN;
  medium: "Película" / "Film").

### 15. Labyrinth (1986) — Jim Henson — Film

- Tier 2 (Bright Fantasy), Final Score 2.2875 (Weighted Internal Score 0.35) — tied exactly with
  Castle in the Sky, inserted right after it. First entry added under v2 methodology directly
  (no v1 predecessor score to compare against).
- Scores: Structural Despair 0, Limited Heroism 0, Moral Cynicism 0, Structural Corruption 0,
  Redemption Difficulty 1, Narrative Acceptance of Injustice 0, Explicit Darkness 2.
- Rationale: a contained, personal rite-of-passage quest rather than a story about a wider
  world or institution — Sarah's defiance of Jareth ("You have no power over me") fully and
  permanently resolves the threat to Toby, and her own arc (working through real selfishness/
  immaturity, since her impulsive wish is what endangers her brother in the first place) is the
  story's only real cost, kept moderate rather than severe. Explicit Darkness carries real
  weight — the Bog of Eternal Stench, the Junk Lady's crushing imagery, and Jareth's
  often-noted uncomfortably seductive dynamic with a teenage Sarah — but the register stays
  dreamlike/surreal rather than genuinely graphic, distinct from Legend or The Nightmare Before
  Christmas (both Explicit Darkness 3).
- Cozy Fantasy = No. Hopepunk = No — a personal coming-of-age quest, not a resistance-to-
  oppression (Fierce) or mortality-themed (Bittersweet) shape, and no real adversity-free
  default kindness either (Gentle).
- Added to xlsx row 12, and to tier 2 on both index.html and es/index.html, inserted right
  after Castle in the Sky (title: "Laberinto" in ES — the official Latin American title,
  distinct from Spain's "Dentro del laberinto" — "Labyrinth" in EN; medium: "Película" / "Film").

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
- **v2 correction (post-promotion):** this entry's early v2 conversion (done before the more
  disciplined process used throughout the rest of the backlog) had Explicit Darkness capped at 2
  — flagged by the user as underscored once live. Revised to 3, matching this very entry's own
  documented content list above (Sally's recurring self-dismemberment, Oogie Boogie's sadism, the
  shooting-down sequence). v2: tier 2 (unchanged), score 2.5125, tied exactly with Legend.
- **v2 correction round 2 (post-relabel):** the user asked directly whether "Bright Fantasy"
  (Tier 2's post-relabel name) is really the right fit. Tested pushing Redemption Difficulty and
  Narrative Acceptance of Injustice up — would have crossed into Tier 3 — and rejected both: this
  film is in fact the specific citation `CRITERIA_THEORY.md` uses to explain why Explicit
  Darkness is allowed to diverge from the other six criteria, so a low structural profile with a
  high Explicit Darkness is its *intended* shape, not an inconsistency. One smaller refinement
  applied: Moral Cynicism 0→1 (Sally's warnings are repeatedly dismissed until vindicated). v2:
  tier 2 (unchanged), score 2.85, now tied with Willow instead of Legend. See SCORING_RECORD.md
  for full reasoning.

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
