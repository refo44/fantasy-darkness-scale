# Additions Log

Tracks new works being added to the Fantasy Darkness Scale, one at a time, across sessions.

**Genre gate, before scoring anything:** first confirm the candidate is genuinely fantasy, or
at least a real fantasy hybrid — magic, mythical/supernatural beings, gods, or other genre-
fantasy trappings have to be a real, central element of the work, not just a surface label or
an adjacent aesthetic. Don't confuse this with "the Fantastique" (the French/literary tradition
of ambiguous, uncanny, or supernatural-tinged realism) or other neighboring-but-distinct genres
(pure science fiction, pure horror with no fantastical element, magical realism used as a
literary device rather than a genre) — none of those qualify on their own just because they
touch the uncanny or the strange. Weird/genre-blending fantasy can still qualify, but only when
it actually reads as fantasy in practice, not merely because it's unconventional — verify with
a quick, explicit genre check when a candidate's classification isn't obvious (e.g. Violence
Jack, confirmed as "post-apocalyptic dark fantasy" with a direct demonic-mythos tie to Devilman,
not pure post-apocalyptic sci-fi, before it was scored).

Process for each item: (1) research & score against the 7 weighted criteria in the xlsx
Methodology sheet, (2) add the row to `Evaluations` with live formulas matching the existing
rows, (3) recalc via LibreOffice to get cached values, (4) determine tier placement, (5) add
the entry to both `index.html` (EN) and `es/index.html` (ES), inserted into the right tier's
`<ul class="works">` in ascending-score order relative to the other works already there (not
appended at the end — the xlsx row order stays chronological/append-only, but the HTML display
order is sorted by score within each tier), (6) commit, push, deploy, verify live, (7) update
this log AND `SCORING_RECORD.md` (add a condensed `## Title` entry there too — every 7-criteria
score plus its rationale, in the format already used by that file's existing entries — every
single time a work is completed here, not just occasionally; this file and SCORING_RECORD.md
fell out of sync for 22 entries between "House of the Dragon" and "Arcane" because this step was
skipped repeatedly, and the user had to catch and backfill it — don't let that happen again),
(8) stop and ask before continuing.

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
26. [x] Dirk Gently's Holistic Detective Agency — Douglas Adams — Novels, TV series — DONE, see
    Completed
27. [x] Dark Sun — TSR / Wizards of the Coast — Tabletop (D&D campaign setting) — post-apocalyptic desert world Athas, magic that kills plant life to power spells, widespread slavery, tyrannical sorcerer-kings draining their own kingdoms' life force; deliberately created as a grim subversion of standard D&D high fantasy — DONE, see Completed
28. [x] Alice in Wonderland — Lewis Carroll — Novel — whimsical, surreal children's fantasy with unsettling undertones (the Queen of Hearts' "off with their heads," nonsensical/threatening logic, identity/growing-up themes), but generally light in overall register — DONE, see Completed
29. [x] The Wizard of Oz — L. Frank Baum (novel), 1939 film — classic adventure, real peril (the Wicked Witch, flying monkeys) but a fundamentally heartwarming, hopeful children's classic — DONE, see Completed
30. [x] Wicked — Gregory Maguire (novel), stage musical — revisionist Oz told from Elphaba's perspective; real political oppression (the Wizard's totalitarian regime, persecution of sentient Animals as a genocide/civil-rights allegory), Elphaba's tragic arc as a misunderstood activist villainized by history — notably darker and more morally complex than the original Oz material — DONE, see Completed
31. [x] The Sandman — Neil Gaiman — Comics, TV series — DONE, see Completed
32. [x] Supernatural (TV series) — DONE, see Completed
33. [x] Charmed (1998 TV series) — DONE, see Completed
34. [x] The Dark Crystal (1982 film, Jim Henson & Frank Oz) — DONE, see Completed
35. [x] The Dark Crystal: Age of Resistance (2019 TV series) — DONE, see Completed
36. [x] His Dark Materials — Philip Pullman — Novels, TV series — DONE, see Completed
37. [x] The Dresden Files — Jim Butcher — Novels, TV series — DONE, see Completed
38. [x] The Grim Company — Luke Scull — Novels — DONE, see Completed
39. [x] The Dark Tower — Stephen King — Novels — DONE, see Completed
40. [x] Eragon (the Inheritance Cycle) — Christopher Paolini — Novels — DONE, see Completed
41. [x] The Princess Bride — William Goldman — Novel, Film — DONE, see Completed
42. [x] Fourth Wing / Iron Flame / Onyx Storm (Empyrean series) — Rebecca Yarros — Novels — score each, bundle into one entry if they land in the same tier — DONE, see Completed
43. [x] Sweet Tooth — Jeff Lemire — Comics, TV series — DONE, see Completed
44. [x] Arcane — Riot Games — TV series — DONE, see Completed
45. [x] Percy Jackson & the Olympians — Rick Riordan — Novels, TV series — DONE, see Completed
46. [x] Devilman Crybaby (2018) — Masaaki Yuasa (based on Go Nagai's Devilman manga) — Anime — DONE, see Completed
47. [x] The Mighty Nein — Critical Role (Campaign 2) — TV series / D&D actual-play — Amazon's
    animated adaptation of Critical Role's second campaign, following on from The Legend of Vox
    Machina (Campaign 1, already in the catalog at Tier 4); a found-family of outcasts and
    monster hunters in a morally grayer, more politically complex setting than Campaign 1's,
    with trauma-centered arcs (Caleb's guilt over his role in his parents' deaths, Nott/Veth's
    identity and addiction arc) — DONE, see Completed
48. [ ] Goblins — Thunt (Tarol Hunt) — Webcomic — https://www.goblinscomic.org/ — began as a
    joke inverting standard D&D "kill goblins for XP" tropes, following a goblin warband trying
    to survive being slaughtered by adventurers for loot; the tone shifts dramatically over its
    run into genuine tragedy (PTSD, addiction, on-page major character deaths), repeatedly
    questioning who the real "monsters" in the story actually are
49. [ ] Twilight (Crepúsculo) — Stephenie Meyer — Novels, Films — the vampire-romance saga
    (Twilight, New Moon, Eclipse, Breaking Dawn); consider the werewolf/vampire treaty politics,
    the Volturi as a governing vampire institution, and Bella's transformation/mortality themes
50. [ ] Wednesday — Netflix TV series (2022– ), created by Alfred Gough & Miles Millar — a
    reimagining centered on Wednesday Addams at Nevermore Academy; murder mystery, monster-hunt,
    and outcast-persecution themes distinct in tone from the classic Addams Family properties
51. [ ] The Addams Family — TV series — the classic macabre-but-loving sitcom family (note:
    multiple TV incarnations exist — the 1964 live-action original, the 1973 animated series,
    the 1992 animated series — decide scope/bundling when scored)
52. [ ] The Addams Family — Films — the Barry Sonnenfeld films (The Addams Family, 1991; Addams
    Family Values, 1993) and the animated films (The Addams Family, 2019; Addams Family 2, 2021)
53. [ ] Chrono Trigger — Square (1995) — Video Game — time-travel JRPG; Lavos's apocalyptic
    destruction of the world in 1999 (the game's default future ending unless averted), the
    genocidal Mystic/Human war, Frog's tragic backstory, and multiple alternate endings ranging
    from full prevention to leaving Lavos's threat unresolved
54. [ ] Forgotten Realms — TSR / Wizards of the Coast — Tabletop (D&D campaign setting), Novels —
    D&D's flagship, most mainstream high-fantasy setting (Faerûn), generally more heroic/optimistic
    in default tone than Dark Sun or Ravenloft, but with genuinely dark corners worth weighing:
    Menzoberranzan's slaveholding, torture-based drow matriarchy under Lolth (R.A. Salvatore's
    Drizzt novels), the Baldur's Gate games' Bhaalspawn-murder-god plot, the Zhentarim/Cult of the
    Dragon as recurring corrupt/villainous institutions, and Icewind Dale's bleaker frontier
    survival stories; decide scope (core setting + Drizzt novels vs. also the CRPGs) when scored
55. [ ] Alice in Wonderland (2010) / Alice Through the Looking Glass (2016) — dir. Tim Burton —
    Films — not a retelling of Carroll's plot but an original "return to Underland" story where
    an adult Alice must slay the Jabberwocky in an actual war between the Red and White Queens'
    courts; confirmed real violence (repeated ocular trauma, severed/rotting heads floating in
    the Red Queen's moat) absent from the source novels, scored separately from the "Alice in
    Wonderland" novels entry (Tier 2) per the same logic that kept Wicked separate from The
    Wizard of Oz
56. [ ] American McGee's Alice (2000) / Alice: Madness Returns (2011) — video games — psychological
    horror reimagining: Alice's family dies in a house fire, she's institutionalized and
    suicidal, and "Wonderland" becomes an explicit, hostile metaphor for her fractured psyche
    (the Mad Hatter as her doctor, the Jabberwock as her survivor's guilt); graphic violence
    throughout, likely several tiers darker than the novels — kept separate rather than bundled,
    same logic that split Final Fantasy I, II & XII apart instead of forcing one score on a wide
    severity spread
57. [ ] Return to Oz — dir. Walter Murch (1985) — Film — based on Baum's 2nd/3rd Oz novels (The
    Marvelous Land of Oz, Ozma of Oz), not the first book; confirmed genuinely disturbing —
    opens with Dorothy about to undergo electroshock therapy in an asylum to "cure" her of
    believing in Oz, features a hall of living disembodied heads, and depicts a transformed,
    near-post-apocalyptic Oz ruled by the unsettling Wheelers; multiple retrospectives call it
    "the most terrifying Disney movie ever made" — kept separate from the original Wizard of Oz
    entry (Tier 2) for the same reason Wicked stayed separate from it
58. [x] Violence Jack — Go Nagai — Manga — DONE, see Completed
59. [x] Devilman Lady — Go Nagai — Manga — DONE, see Completed

## Completed

### 47. The Mighty Nein — Critical Role — TV series / D&D actual-play

- Tier 6 (Dark Fantasy), Final Score 6.225 (Weighted Internal Score 2.10) — a three-way exact
  numeric tie with The Witcher and Final Fantasy XIV.
- Scores: Structural Despair 1, Limited Heroism 2, Moral Cynicism 2, Structural Corruption 3,
  Redemption Difficulty 2, Narrative Acceptance of Injustice 2, Explicit Darkness 3.
- Scope: scored against the complete, finished tabletop campaign (141 episodes, 2018-2021), not
  just the still-airing Amazon TV adaptation (Season 1, 8 episodes, November 2025, which has
  only aired the opening arc so far) — matching the precedent used for House of the Dragon and
  A Knight of the Seven Kingdoms, where a finished source history is scored even while its
  adaptation is still airing.
- Rationale: Structural Corruption (3) is grounded in Caleb Widogast's confirmed backstory — the
  Cerberus Assembly, a sitting body of the Dwendalian Empire's government, groomed him and two
  other teens under Trent Ikithon (Archmage of Civil Influence), manipulated their memories into
  believing their own parents were traitors, and ordered them to kill their parents as a "final
  trial"; Caleb set his parents' house on fire and broke only when he heard them screaming
  inside — state-sponsored psychological manipulation of children into parricide, a real,
  named, government-level institution enabling atrocity. Redemption Difficulty (2) is carried
  by Veth: cursed into goblin form after her family was captured and she was deliberately
  tortured and drowned ("make Veth suffer"), she became an alcoholic coping with the trauma, and
  was only cured and reunited with her husband and son through her friends' sustained effort — a
  real, costly, ultimately successful recovery. Explicit Darkness (3) reflects confirmed content
  beyond Vox Machina's own already-elevated bar: Molly, a beloved main character, is killed and
  then resurrected — but as Lucien, a completely different original personality with no memory
  of Molly at all, who tells the party "Mollymauk means nothing to him," a real identity-horror
  arc, on top of Caleb's parents' immolation and sustained war content. Limited Heroism and
  Narrative Acceptance of Injustice both land at 2: real victories are achieved (Veth's curse
  reversed, the war between the Empire and Xhorhas ending), but the war's peace is explicitly
  doubted within the story itself (Essek believes it won't last), keeping this short of a clean
  resolution.
- Cozy Fantasy = No. Hopepunk = No: matches precedent (no work at Tier 6 or darker carries the
  tag).
- Neighbor check: exact WIS match (2.10) with The Witcher (SD2/SC2 instead of this entry's
  SD1/SC3 — The Witcher's despair is spread evenly across its world, while this entry's severity
  concentrates specifically in one institutional villain against a less generally-despairing
  backdrop) and Final Fantasy XIV (SD3/LH1/MC1 instead of this entry's SD1/LH2/MC2). Checked
  further against a non-adjacent tier-6 work, Supernatural (6.90, near the tier's ceiling,
  SD2/LH2/MC3/SC3/RD2/NAI2/ED3): the 0.15 gap resolves on Structural Despair and Moral Cynicism
  — Supernatural's monster-of-the-week format sustains a bleaker baseline world-state and harsher
  moral physics than this entry's found-family-centered story. Label check: "Dark Fantasy" fits —
  genuinely heavy institutional and personal trauma, but real recovery (Veth) and a real, if
  fragile, peace keep it short of Tier 7's harder-edged register.
- Added to xlsx row 128, and to tier 6 on both index.html and es/index.html, appended after The
  Witcher (exact score tie, existing-entries-first ordering); title kept in English on both
  pages, matching The Legend of Vox Machina's own precedent (Amazon's official releases use the
  same English title regardless of dub language); medium: "TV series / D&D actual-play" /
  "Serie de TV / Actual play de D&D".

### 59. Devilman Lady — Go Nagai — Manga

- Tier 6 (Dark Fantasy), Final Score 6.1125 (Weighted Internal Score 2.05) — an exact numeric
  tie with Clevatess, Re:Zero, The Sandman, and The Dresden Files, via a genuinely different
  profile.
- Scores: Structural Despair 1, Limited Heroism 2, Moral Cynicism 3, Structural Corruption 3,
  Redemption Difficulty 1, Narrative Acceptance of Injustice 1, Explicit Darkness 4.
- Scope: scored against the manga (1997-2000), confirmed more violent and sexually explicit
  than its own anime adaptation.
- Rationale: Structural Despair (1) reflects a real outlier for this franchise — the ending
  explicitly reveals the Devil-Beast transformation sweeping humanity is its next evolutionary
  stage, reframed as a natural, positive change rather than decline, closing on protagonist Jun
  Fudo watching children with tails playing peacefully. Structural Corruption (3) is grounded in
  the Human Alliance, a clandestine military unit working with world governments specifically to
  hunt down and kill anyone with "Devil Beast Syndrome" while keeping the public in the dark — a
  real, confirmed multi-government persecution apparatus targeting an emergent class later
  revealed to be no threat at all. Moral Cynicism (3) reflects extensive depicted torture and
  rape of innocent characters along the way, including the loss of Kazumi, a girl Jun grows
  close to, who dies saving her. Redemption Difficulty and Narrative Acceptance of Injustice
  both stay low (1) since the story's own resolution explicitly validates and resolves the
  central conflict rather than leaving it open. Explicit Darkness reaches the ceiling (4) on
  confirmed graphic torture, rape, and dismemberment throughout.
- Cozy Fantasy = No. Hopepunk = No: matches precedent (no work at Tier 6 or darker carries the
  tag).
- Genre check: confirmed fantasy/horror, not science fiction — demonic possession, supernatural
  transformation, and an entire "Devil-Beast" evolutionary mythos are central and load-bearing,
  not incidental dressing.
- Added to xlsx row 127, and to tier 6 on both index.html and es/index.html, appended after The
  Dresden Files (exact score tie, existing-entries-first ordering).

### 58. Violence Jack — Go Nagai — Manga

- Tier 8 (Grimdark), Final Score 8.1375 (Weighted Internal Score 2.95) — an exact numeric tie
  with Berserk, via a genuinely different profile (Structural Corruption 3/Narrative Acceptance
  of Injustice 2 here vs. Berserk's 2/3).
- Scores: Structural Despair 3, Limited Heroism 3, Moral Cynicism 3, Structural Corruption 3,
  Redemption Difficulty 3, Narrative Acceptance of Injustice 2, Explicit Darkness 4.
- Rationale: a post-apocalyptic dark fantasy set after an earthquake and volcanic eruption level
  the Kanto region, ruled by warlords and biker gangs; the giant, near-unstoppable Jack wanders
  the wasteland in an ongoing conflict with the tyrant Slum King. Structural Despair and Limited
  Heroism both land at 3: Jack does defeat Slum King in their final confrontation, but the wider
  anarchic collapse depicted across the series' many side-stories isn't shown reversed by that
  one victory. Structural Corruption (3) is reinforced by the story's own supernatural framing —
  Slum King was literally created by Satan (Ryo Asuka) out of self-punishment for killing Akira
  Fudo, tying the warlord's entire rule directly to the Devilman mythos rather than organic
  human collapse alone. Redemption Difficulty (3) rests on a confirmed failed case: Slum Queen
  chooses to rebel against her husband and is killed with her own whip for it. Explicit Darkness
  reaches the ceiling (4) on the series' own reputation — "particularly infamous for... large
  amounts of sex and gory violence," notorious even within Go Nagai's catalog.
- Cozy Fantasy = No. Hopepunk = No: matches precedent (no work at Tier 6 or darker carries the
  tag).
- Genre check: confirmed post-apocalyptic dark fantasy, not pure sci-fi — Jack is directly tied
  to the Devilman demon mythos (in the main continuity he's revealed to be a revived Akira Fudo),
  and Satan is a key element of the narrative, not just a wasteland-survival premise.
- Neighbor check: exact WIS match (2.95) with Berserk (Structural Corruption 2/Narrative
  Acceptance of Injustice 3 there vs. this entry's 3/2 — Berserk's evil is concentrated in one
  arc (the Godhand/Eclipse) rather than a pervasive ruling structure, per that entry's own
  established reasoning, while this entry's warlord rule is the setting's entire governing
  structure and is explicitly demon-created; trading against Berserk's own core injustice never
  being addressed at all by its still-ongoing story, vs. this entry's top-level tyrant actually
  being defeated). Label check: "Grimdark" fits — a demon-tied warlord wasteland with graphic,
  pervasive violence, matching the tier's register.
- Added to xlsx row 126, and to tier 8 on both index.html and es/index.html, appended after
  Berserk (exact score tie, existing-entry-first ordering).

### 46. Devilman Crybaby — Go Nagai — Manga, Anime

- Tier 9 (Extreme Grimdark), Final Score 9.825 (Weighted Internal Score 3.70) — an exact
  numeric tie with The First Law, via a swapped profile (Structural Corruption 3/Narrative
  Acceptance of Injustice 4 here vs. The First Law's 4/3).
- Scores: Structural Despair 4, Limited Heroism 4, Moral Cynicism 4, Structural Corruption 3,
  Redemption Difficulty 3, Narrative Acceptance of Injustice 4, Explicit Darkness 4.
- **Bundle decision:** kept the original manga and the 2018 Netflix anime (dir. Masaaki Yuasa)
  as one entry, not split — the anime is explicitly the first adaptation to bring the manga's
  own ending to screen (near-total human extinction, Earth destroyed outright by God), so the
  two tell the same story at the same intensity, matching the bundling precedent already used
  for Record of Lodoss War and The Saga of Tanya the Evil rather than the split used for Final
  Fantasy I/II/XII. The earlier, considerably softer 1970s TV anime is excluded as not moving
  the needle, same pattern as any other lighter adaptation on this scale.
- Rationale: Structural Despair (4) and Limited Heroism (4) both reach the ceiling on the
  series' own confirmed ending: God's angel army annihilates the remaining demons and
  devilmen (including Akira, the protagonist, whose body is left bifurcated), and God then
  destroys the entire Earth outright, reducing it to a molten ball — not an averted threat but
  the story's actual, on-page conclusion, with Akira's entire struggle to retain his humanity
  while gaining demon power ultimately saving no one. Moral Cynicism (4) reflects the series'
  central thesis that humanity's own fear and paranoia (a global broadcast revealing "demons
  look like ordinary humans") destroys it faster than any external threat — Miki Makimura, an
  innocent, kind character, is killed by a mob specifically for her association with Akira
  (lacerated, dismembered, her body parts paraded on sticks before her house is burned), while
  cruelty goes systemically unpunished until Akira's own retaliatory violence. Narrative
  Acceptance of Injustice (4) reflects that none of this is corrected or addressed by the
  story's own end — the closing image of a lifeless Earth eventually re-forming is a minimal,
  ambiguous coda, not a resolution of anything depicted. Structural Corruption stays at 3, not
  4: the mob violence is societal collapse rather than a functioning institution, and while
  God's own disproportionate, punitive destruction of the entire planet is a real institutional-
  authority case, it's a singular cosmic judgment rather than an ongoing exploitative apparatus.
  Redemption Difficulty stays at 3, not 4: Ryo/Satan's love for Akira is real, if it arrives
  only after Akira's death — a clear failure case, but a genuine, felt attempt at redemption
  (the story's own "Crybaby" thematic core), distinguishing it from a setting where redemption
  isn't even attempted anywhere. Explicit Darkness reaches the ceiling (4): Miki's death scene
  is widely cited as among the most graphic single scenes in mainstream anime, on top of
  extensive gore, sexual content, and self-mutilation running throughout the series.
- Cozy Fantasy = No. Hopepunk = No: matches precedent (no work at Tier 6 or darker carries the
  tag).
- Neighbor check: exact WIS match (3.70) with The First Law (SC4/NAI3 instead of this entry's
  SC3/NAI4 — The First Law's severity is grounded in its setting's institutions (SC4), this
  entry's in its confirmed apocalyptic ending (NAI4) — a legitimate different route to the same
  total). No other Tier 9 work exists for a non-adjacent same-tier check, so checked instead
  against the full Tier 8 spread: the gap resolves exactly on named axes against all six
  entries — Berserk's manga is ongoing with a real found-family thread and no confirmed
  extinction ending (0.75 gap); Dark Souls' cyclical curse is ambiguous across multiple possible
  endings, some implying real change (0.70 gap); A Song of Ice and Fire is unfinished, with no
  confirmed ultimate resolution (0.60 gap); Elden Ring's multiple endings include real paths
  toward restoration that this entry's fixed ending lacks (0.55 gap); and against Fire Punch/
  Dark Sun (0.45 gap each, the only two where this entry doesn't lead on every axis), this
  entry still comes out ahead specifically on Structural Despair, Limited Heroism, and
  Narrative Acceptance of Injustice — the expected trade-off between a totalizing-institution
  story and a totalizing-extinction one. Checked against Tier 10 (Warhammer 40,000, all 4s,
  Weighted Internal Score 4.0): the gap holds specifically on Redemption Difficulty (3 vs. 4) —
  Warhammer's setting has no redemption ever attempted anywhere across the franchise, while this
  entry's entire thematic core is a real, if failed, act of love and grief. Label check:
  "Extreme Grimdark" fits — total extinction and a planet destroyed outright, distinguished from
  Tier 10's totalizing, hopeless-by-design register by remaining one complete story with a real
  (if failed) emotional core.
- Added to xlsx row 125, and to tier 9 on both index.html and es/index.html, appended after The
  First Law (exact score tie, existing-entry-first ordering); removed the "solo" CSS class from
  the tier-9 section on both pages now that it holds two works, matching the precedent set when
  Attack on Titan joined Berserk at Tier 8/left it solo again.

### 45. Percy Jackson & the Olympians — Rick Riordan — Novels, TV series

- Tier 3 (Moderately Bright Fantasy), Final Score 3.6375 (Weighted Internal Score 0.95) — an
  exact numeric tie with The Hobbit and Howl's Moving Castle, via a genuinely different profile.
- Scores: Structural Despair 0, Limited Heroism 0, Moral Cynicism 1, Structural Corruption 2,
  Redemption Difficulty 2, Narrative Acceptance of Injustice 0, Explicit Darkness 2.
- Scope: scored against the original 5-book series (The Lightning Thief, The Sea of Monsters,
  The Titan's Curse, The Battle of the Labyrinth, The Last Olympian) and the Disney+ TV
  adaptation, which closely follows the books. The later series (The Heroes of Olympus, The
  Trials of Apollo) are out of scope.
- Rationale: Limited Heroism and Narrative Acceptance of Injustice both bottom out at 0 on the
  same specific textual basis — the series doesn't just defeat its villain (Kronos), it resolves
  the story's real underlying institutional problem: the Olympian gods' recurring neglect of
  their demigod children. Percy's climactic act is forcing the entire pantheon to change how it
  treats its children — an explicit, structural, pantheon-wide reform, not just a threat
  removed. Structural Corruption (2) is grounded in that same neglect being framed as systemic
  across the gods generally, not an isolated bad parent, strong enough to require a forced,
  universal rule change to fix. Redemption Difficulty (2) is carried by Luke: he genuinely
  betrays the gods and becomes Kronos's vessel, then sacrifices his own life in the finale to
  stop Kronos from within — a real, costly, successful redemption. Explicit Darkness (2) reflects
  the series' real, recurring named-character deaths (Zoë Nightshade poisoned and then crushed by
  her own Titan father; Bianca di Angelo's self-sacrifice; Charles Beckendorf dying to complete a
  suicide mission; Silena Beauregard dying in atonement) — genuine loss across the series, but
  confirmed by parent-review sources to stay short of graphic detail (monsters disintegrate to
  dust rather than leaving gore).
- Cozy Fantasy = No. Hopepunk = No: adventure-and-found-family driven, not organized specifically
  around resisting oppression or bittersweet mortality-acceptance.
- Neighbor check: exact WIS match (0.95) with The Hobbit and Howl's Moving Castle (both
  SD1/LH1/MC0/SC1 instead of this entry's SD0/LH0/MC1/SC2) — a clean trade-off, since the
  Hobbit's Battle of Five Armies leaves real, unrecovered losses (Thorin, Fíli, and Kíli all die)
  that this entry's clean systemic-reform ending doesn't carry, while this entry's institutional
  godly-neglect problem is a stronger, more explicit "central institution" case than the Hobbit's
  more isolated dragon-hoarding conflict. Checked further against a non-adjacent tier-3 work,
  Nausicaä of the Valley of the Wind (3.975, near the tier's ceiling, SD2/LH1/MC1/SC1/RD0/NAI1/
  ED2): the 0.15 WIS gap resolves cleanly — Nausicaä's environmental-apocalypse backdrop and war
  outweigh this entry's higher Structural Corruption/Redemption Difficulty (institutional neglect
  plus Luke's costly redemption vs. Nausicaä having no real redemption arc). Label check:
  "Moderately Bright Fantasy" fits — real death and betrayal exist, but the found-family Camp
  Half-Blood setting and the ending's genuine institutional fix keep it well short of Tier 4's
  heavier "real losses, still high hope" register.
- Added to xlsx row 124, and to tier 3 on both index.html and es/index.html, inserted after
  Howl's Moving Castle (exact score tie, existing-entries-first ordering); title "Percy Jackson &
  the Olympians" in EN, "Percy Jackson y los dioses del Olimpo" in ES (the official Spanish
  series title); medium: "Novels, TV series" / "Novelas, Serie de TV".

### 44. Arcane — Riot Games — TV series

- Tier 6 (Dark Fantasy), Final Score 6.7875 (Weighted Internal Score 2.35) — an exact 7-axis
  profile match with Fourth Wing and The Grim Company (see extended neighbor check below).
- Scores: Structural Despair 2, Limited Heroism 2, Moral Cynicism 2, Structural Corruption 3,
  Redemption Difficulty 2, Narrative Acceptance of Injustice 2, Explicit Darkness 4.
- Scope: scored against both seasons (2021, 2024) as a complete story.
- Rationale: Structural Corruption (3) rests on Piltover's explicit, state-run discrimination
  against Zaun — an Enforcer police force and border checkpoints enforcing a real institutional
  class divide, not just informal prejudice; this is one government running two distinct
  discriminatory practices (matching Fourth Wing's precedent for what keeps Structural
  Corruption at 3 rather than the scale's ceiling — a single institution, not the multi-
  institution "all independently corrupt" pattern that earns A Song of Ice and Fire's 3 its own
  more totalizing framing). Redemption Difficulty (2) is carried by Viktor: his "Glorious
  Evolution" arc ends with him choosing to destroy his own life's work (and likely himself) to
  stop the forced assimilation he set in motion — a genuine success, but only at real, possibly
  fatal cost. Explicit Darkness (4) reflects the show's TV-MA reputation for sustained, graphic
  on-screen violence: named-character deaths shown directly (the Council bombing, war
  casualties), a visible shimmer-addiction crisis, and body-horror transformation (Vander into
  Warwick) running throughout, not as isolated beats. Narrative Acceptance of Injustice (2)
  reflects that Piltover's checkpoints are literally dismantled by the finale — real, visible
  structural change — but the show frames this as fragile and unresolved rather than a clean
  fix (discrimination is "paused," and the closing scene has Vi and Caitlyn "committed to a
  future fight," not a settled peace).
- Cozy Fantasy = No. Hopepunk = No: matches precedent (no work at Tier 6 or darker carries the
  tag).
- Neighbor check, extended given the exact profile match: checked Redemption Difficulty
  specifically against The Grim Company's own documented precedent (that entry originally
  over-scored RD to 3 to break a tie with Märchen Crown, then corrected back to 2 after finding
  no confirmed failure/partial-success pattern in the text) — applied the same scrutiny here and
  found Viktor's arc is a genuine, textually clear success at cost, at least as solid a case for
  RD2 as Grim Company's own anchor, so it wasn't inflated just to differentiate the tie. The
  4-way score cluster at 6.7875 isn't a single default shape: The Dark Crystal: Age of
  Resistance sits at the same total via a genuinely different profile (Structural Despair 3,
  Redemption Difficulty 0, Narrative Acceptance of Injustice 3), confirming this is a real,
  independently-reachable coordinate. Non-adjacent check against The Dresden Files (6.1125,
  bottom of the tier, SD1/LH2/MC2/SC2/RD2/NAI2/ED4): the 0.30 WIS gap resolves cleanly on two
  named axes — Structural Corruption (3 vs. 2: Piltover's checkpoints are explicit state-run
  discrimination against an entire underclass, a stronger institutional case than Dresden's
  corrupt-but-not-governmental supernatural factions) and Structural Despair (2 vs. 1: an
  escalating war/oppression arc vs. Dresden's more episodic structure). Label check: "Dark
  Fantasy" fits — genuinely heavy content (terrorism, war, addiction, body horror), but
  Piltover's government actually dismantles its own discriminatory checkpoints by the end, a
  real institutional reform that keeps this short of Tier 7-8's "no institution is safe, nothing
  gets fixed" register (Dark Tower, House of the Dragon, A Song of Ice and Fire).
- Added to xlsx row 123, and to tier 6 on both index.html and es/index.html, appended after
  Fourth Wing (exact score tie, existing-entries-first ordering).

### 30. Wicked — Gregory Maguire — Novel

- Tier 7 (Extreme Dark Fantasy), Final Score 7.575 (Weighted Internal Score 2.70) — an exact
  numeric tie with The Stormlight Archive, via a genuinely different profile.
- Scores: Structural Despair 3, Limited Heroism 3, Moral Cynicism 3, Structural Corruption 3,
  Redemption Difficulty 1, Narrative Acceptance of Injustice 3, Explicit Darkness 3.
- Scope: scored via the novel (Wicked: The Life and Times of the Wicked Witch of the West,
  1995) as the darker, definitive version. The stage musical (2003) and the 2024/2025 films,
  which follow the musical rather than the book, were checked and confirmed significantly
  softer: Doctor Dillamond is merely removed from his teaching post and silenced rather than
  assassinated, Elphaba fakes her death and escapes with Fiyero rather than dying, and the
  story ends on reconciliation (Glinda and Elphaba's friendship restored, Glinda taking power)
  rather than the book's unresolved tragedy. A rough parallel estimate for the musical alone
  (SD1/LH1/MC1/SC2/RD1/NAI1/ED1, WIS ~1.15) lands around Tier 4 — roughly a 3-tier gap — so it
  doesn't move this entry, the same pattern already used for Eragon's film and Sweet Tooth's
  show. Not split into a separate entry (unlike Wicked's own relationship to The Wizard of Oz,
  which is a genuinely different, morally complex retelling of the same events and so earned
  its own catalog slot): the musical isn't a different story, just a much softer telling of the
  same one.
- Rationale: Structural Despair (3) reflects that Animal rights are actively worsening across
  the novel under the Wizard's laws, with no counterbalancing improvement shown by the book's
  end. Moral Cynicism (3) is carried by Doctor Dillamond's murder specifically to suppress the
  scientific evidence he was gathering against the regime's discriminatory laws — the one
  character producing inconvenient truth is killed for it, while the actual moral actor
  (Elphaba) is the one history mythologizes as evil. Structural Corruption (3) rests on two
  distinct central institutions built on oppression: the Wizard's regime (enforced via Madame
  Morrible's assassination of dissidents and legal stripping of an entire sentient population's
  rights) and, later in the novel, Nessarose's own tyrannical rule of Munchkinland. Redemption
  Difficulty (1) is notably low for this tier because the axis isn't strongly engaged here —
  Elphaba isn't a wrongdoer working toward redemption, she's a sympathetic figure misjudged by
  history, a different dynamic than the criterion is built to measure. Narrative Acceptance of
  Injustice (3) reflects that both core injustices (Animal oppression and Elphaba's false
  legacy) are explicitly left unresolved: she dies believing everyone hated her, and the myth of
  her wickedness is what survives, not the truth. Explicit Darkness (3) covers a graphic
  assassination (throat slit) and Elphaba's own fiery death, plus confirmed sexual content (an
  affair with Fiyero, described "in some detail but never in lurid terms") — real and frequent,
  short of the tier's extreme ceiling.
- Cozy Fantasy = No. Hopepunk = No: matches precedent (no work at Tier 6 or darker carries the
  tag).
- Neighbor check: exact WIS match (2.70) with The Stormlight Archive (SD2/MC2/RD3 instead of
  this entry's SD3/MC3/RD1 — Stormlight's severity is carried by Kaladin and Dalinar's costly,
  sustained redemption arcs, where Wicked's is carried by an actively worsening political
  situation and a regime that kills for the truth). Sits comfortably above His Dark Materials
  (7.4625, WIS 2.65, lower on SD/MC despite ED4) and Fourth Wing/Supernatural (6.79/6.90, both
  WIS 2.35-2.4, a clear gap). Sits just below the four 7.80 works (Attack on Titan, House of the
  Dragon, The Dark Tower, Sweet Tooth) — each clears either Explicit Darkness 4 (sustained
  graphic content, vs. this entry's real-but-not-sustained ED3) or Redemption Difficulty 3 (a
  real, costly redemption arc, which this entry doesn't have), or both. Label "Extreme Dark
  Fantasy" fits.
- Added to xlsx row 122, and to tier 7 on both index.html and es/index.html, inserted after The
  Stormlight Archive (exact score tie, existing-entry-first ordering).

### 29. The Wizard of Oz — L. Frank Baum — Novel, Film

- Tier 2 (Bright Fantasy), Final Score 2.625 (Weighted Internal Score 0.5) — a three-way,
  profile-distinct tie with Harry Potter and the Chamber of Secrets and The Little Prince.
- Scores: Structural Despair 0, Limited Heroism 0, Moral Cynicism 0, Structural Corruption 2,
  Redemption Difficulty 0, Narrative Acceptance of Injustice 0, Explicit Darkness 2.
- Scope: scored as the 1900 novel (The Wonderful Wizard of Oz) + the 1939 film, bundled — the
  film keeps the book's content essentially intact (even its beatings and slavery), just
  visually intensifying the peril. Checked and excluded the rest of Baum's 14-book Oz series:
  individual later books do have real dark beats (Rinkitink in Oz's invasion and enslavement of
  an entire island; the Tin Woodman's origin, revealed in book 12, involving a cursed axe that
  repeatedly severs his limbs), but critical consensus is that the series as a whole "stays
  playful" even at its highest stakes, and if anything trends more utopian over time (later Oz
  establishes its inhabitants can't even die) — not severe or distinct enough to move this
  entry or justify its own slot, unlike Return to Oz (1985, queued separately as #57), which
  draws on the same later books but is confirmed as a genuinely different, disturbing register.
- Rationale: Limited Heroism bottoms out at 0 on a thorough, durable victory — both witches
  killed or deposed, the enslaved Winkies freed, the fraudulent Wizard exposed, and Dorothy's
  companions installed as legitimate new rulers of two regions. Structural Corruption lands at
  2, not lower, on specific, sourced content: the Wicked Witch of the West conquered Winkie
  Country using the Golden Cap's army and enslaved the native Winkies, forcing them "to labor
  night and day" and, on failure, beating them "well with a strap" — a real institution built
  on forced labor, not a symbolic threat, though confined to one region (Glinda's Quadling
  Country governs legitimately, keeping this short of a totalizing 3-4). Explicit Darkness
  lands at 2 on real, visible danger without graphic detail: critics and retrospectives
  consistently cite the flying-monkey attack as among the most frightening scenes in children's
  cinema, on top of the on-page beatings and Dorothy's own captivity as a slave.
- Cozy Fantasy = No. Hopepunk = No: adventure-driven peril-and-triumph, not kindness/community
  positioned as a deliberate value against real adversity.
- Neighbor check: exact WIS match (0.5) with Harry Potter and the Chamber of Secrets (SC1/NAI1
  instead of this entry's SC2/NAI0 — HP's central injustice, the attacks on Muggle-born
  students, is only partially resolved by book's end, while Oz's slavery and fraud are both
  fully undone) and The Little Prince (SD1/MC1 instead of SC2 — a wholly different kind of
  gentle melancholy rather than institutional exploitation). Sits above Legend (2.5125, SC0 —
  no institutional corruption, just one dark lord) and below A Conspiracy of Truths (2.7375,
  which adds SD1 on top of a comparable SC1/ED1). Label "Bright Fantasy" fits.
- Added to xlsx row 121, and to tier 2 on both index.html and es/index.html, inserted after
  Harry Potter and the Chamber of Secrets (exact score tie, existing-entries-first ordering).

### 28. Alice in Wonderland — Lewis Carroll — Novels

- Tier 2 (Bright Fantasy), Final Score 2.0625 (Weighted Internal Score 0.25) — an exact profile
  match with Harry Potter and the Philosopher's Stone (identical on all seven criteria), not
  just a numeric tie.
- Scores: Structural Despair 0, Limited Heroism 0, Moral Cynicism 0, Structural Corruption 1,
  Redemption Difficulty 0, Narrative Acceptance of Injustice 0, Explicit Darkness 1.
- Scope: scored as the duology — Alice's Adventures in Wonderland (1865) and Through the
  Looking-Glass (1871) — as commonly published and read together under this title; adaptations
  (1951 Disney, 2010 Tim Burton, etc.) weren't consulted since the queue item specified the
  novel(s).
- Rationale: Structural Despair, Limited Heroism, Moral Cynicism, Redemption Difficulty, and
  Narrative Acceptance of Injustice all bottom out at 0 for the same underlying reason — the
  entire adventure is explicitly a dream, resolved completely and instantly the moment Alice
  wakes, with nothing carrying real consequence. Even the story's ostensible central threat is
  confirmed toothless within the text itself: the Gryphon tells Alice "It's all her fancy: she
  executes nobody, you know," and the King of Hearts secretly pardons everyone the Queen
  condemns — cruelty is systematically undercut, not rewarded (Moral Cynicism 0), and Alice's
  single assertive act at the climax ("You're nothing but a pack of cards!") ends the entire
  conflict outright (Limited Heroism 0). Structural Corruption lands at 1, not 0, because the
  Queen genuinely is a capriciously tyrannical ruler on her face, even though confirmed
  toothless — an anomaly rather than a functioning exploitative system. Explicit Darkness
  similarly lands at 1 on real, specific, if bloodless content: the "Walrus and the Carpenter"
  poem (Through the Looking-Glass, recited by Tweedledum/Tweedledee) has the pair flatter and
  lure trusting oysters before eating them, playing genuine betrayal and predation for
  whimsical effect; the Duchess violently jostles her baby while singing "Speak roughly to your
  little boy, and beat him when he sneezes"; and the executioner's debate over whether the
  Cheshire Cat's disembodied head can be beheaded without a body is a real, if comic, grotesque
  image — enough for "occasional tension, no graphic violence" but no higher.
- Cozy Fantasy = No: doesn't belong to the modern cozy-fantasy publishing genre (comfort-focused,
  low-stakes, found-family) any more than Totoro does despite a similarly gentle surface tone.
  Hopepunk = No: doesn't fit any of the three variants — Wonderland's nonsense-logic isn't kindness
  or community positioned as a deliberate value.
- Neighbor check: exact profile match with Harry Potter and the Philosopher's Stone (SD0 LH0 MC0
  SC1 RD0 NAI0 ED1 on both) — different stories, same shape: both have a nominal villain whose
  threat proves non-lethal/contained (Quirrell/Voldemort vs. the Queen of Hearts), no real
  stakes, and only mild unsettling imagery. Sits comfortably below The House in the Cerulean
  Sea, Final Fantasy III & V, and Slayers (all 2.175, WIS 0.3) — those clear a full criterion
  point higher on at least one axis (Cerulean Sea's SD1; FFIII&V's and Slayers' ED3 from actual
  on-screen combat/death). Clear of Tier 1's true zero-conflict cluster (Totoro, Ponyo, Kiki's
  Delivery Service, Legends & Lattes, all WIS 0) precisely because of the handful of real, if
  bloodless, unsettling beats above. Label "Bright Fantasy" fits.
- Added to xlsx row 120, and to tier 2 on both index.html and es/index.html, inserted
  immediately after Harry Potter and the Philosopher's Stone (exact score tie, existing-entry-
  first ordering matching precedent).

### 27. Dark Sun — TSR / Wizards of the Coast — Tabletop (D&D campaign setting), Novels

- Tier 8 (Grimdark), Final Score 8.8125 (Weighted Internal Score 3.25) — an exact numeric tie
  with Fire Punch, via a genuinely different profile (see neighbor check below).
- Scores: Structural Despair 3, Limited Heroism 3, Moral Cynicism 3, Structural Corruption 4,
  Redemption Difficulty 3, Narrative Acceptance of Injustice 3, Explicit Darkness 4.
- **Bundle-vs-split decision, addressed explicitly per this session's brief:** scored as one
  bundled entry, anchored on the AD&D 2nd Edition campaign setting (1991, the version this
  queue item itself describes, and the one the brand's own reputation rests on) plus the Prism
  Pentad novels (Troy Denning, 5 books, 1991-95) as co-primary sources — same era, same canon,
  mutually reinforcing rather than divergent. Checked, and excluded from separate scoring,
  three other candidates: (1) the 4th Edition revival (2010) — a contemporary EN World review
  found it "stuck to the vast majority of both the content and tone of the original," so it
  doesn't move any axis, matching how this session already handles adaptations lighter/no
  different than their source (Eragon's film, Sweet Tooth's show); (2) the Shattered Lands
  (1993) and Wake of the Ravager (1994) CRPGs — their plot (escaped gladiator-slaves, a
  sorcerer-king planning to mass-sacrifice entire cities, an apocalyptic monster) tracks the
  same severity, so nothing here contradicts the score, but as niche SSI games with far less
  cultural weight than the novels or the setting itself, and no story distinct enough to
  warrant their own slot (unlike Age of Resistance or The Mighty Nein), they're excluded as not
  relevant enough to the catalog on their own; (3) 3rd edition/d20 material — never officially
  published, only unofficial third-party content, excluded as non-canonical; and the announced
  2027 5th Edition books — unreleased, out of scope like any unreleased work.
- Rationale: Structural Corruption reaches the ceiling (4) on the setting's defining feature —
  every city-state in the Tyr region is ruled by a sorcerer-king whose power is drawn directly
  from draining his own population's life-force via "defiler" magic; there is no legitimate
  ruling institution shown anywhere on Athas, a more totalizing case than the more common
  "corrupt faction among functioning institutions" pattern (e.g. A Song of Ice and Fire's SC3,
  which still has some aspirational/functioning institutions like the Night's Watch). Explicit
  Darkness also reaches the ceiling (4) on specific, sourced content: the Dragon of Tyr
  (Borys) demands a tithe of 1,000 sacrificial slaves *per year, from every city-state*,
  harvested for their life energy to keep the setting's original threat (Rajaat) imprisoned —
  not a one-off atrocity but the setting's literal, recurring operating mechanism for
  centuries before the Pentad's climax — plus "defiler" magic that visibly withers all plant
  life to ash with every casting, and confirmed body-horror mutation in magic-scarred zones.
  WotC's own 2027 relaunch is explicitly D&D's first-ever 18+ rated setting, with a stated
  content warning for slavery, nudity, and violence — the current publisher's own read
  corroborates this as an outlier in graphic content, not just theme. Structural Despair and
  Limited Heroism both land at 3, not 4, on a specific distinction: unlike settings where
  nothing is ever resolved, the Prism Pentad's heroes don't just free Tyr locally — they
  destroy Borys and end Rajaat's threat outright, a real cosmic-scale victory. That's why
  ordinary city-state tyranny persisting elsewhere on Athas keeps this at "improvement is the
  exception, not the norm" rather than "no improvement alters the trajectory." Moral Cynicism
  (3) reflects that the setting's power structure explicitly rewards atrocity — Rajaat's
  champions became immortal sorcerer-kings *as payment* for committing genocide against entire
  non-human races (the "Cleansing Wars") — without going all the way to 4, since the Pentad's
  own heroes do succeed through genuine cooperation, not universal punishment of virtue.
  Redemption Difficulty (3) rests on Tithian: he backs the revolution against Kalak, is
  installed as Tyr's new king, then immediately schemes to become a sorcerer-king himself —
  becoming exactly what he helped overthrow — and ends the Pentad permanently exiled to
  another dimension, never redeemed; Sadira's more flexible use of defiler-coded magic for
  good ends (she survives, gains power, helps end Rajaat) shows redemption/grace isn't
  foreclosed for everyone, keeping this short of the 4 ceiling. Narrative Acceptance of
  Injustice (3) reflects that Tyr's own injustice is resolved within this story, but ordinary
  tyranny across the rest of Athas is left explicitly ongoing, addressed only across many later
  novels outside this entry's scope — a structural condition, not something this story resolves
  or simply leaves permanently unaddressed.
- Cozy Fantasy = No. Hopepunk = No: matches precedent (no work at Tier 6 or darker carries the
  tag).
- Neighbor check: Fire Punch (also 8.8125) has the identical Weighted Internal Score via a
  swapped profile — Moral Cynicism 4 / Structural Corruption 3, vs. this entry's Moral Cynicism
  3 / Structural Corruption 4 — everything else on both entries matches exactly. Below this
  entry, Elden Ring (8.59, Structural Despair 4 but Structural Corruption/Explicit Darkness
  only 3) and A Song of Ice and Fire (8.475, an identical SD3/LH3/MC3/RD3/NAI3/ED4 profile but
  Structural Corruption only 3, per the institutional-legitimacy distinction above) both sit
  below on specific, named axes. Above this entry, the tier-9 floor (The First Law, Weighted
  Internal Score 3.7, Structural Despair/Limited Heroism/Moral Cynicism/Structural Corruption
  all at the 4 ceiling) sits a full 0.45 WIS clear — not a close call — consistent with Dark
  Sun's own Structural Despair/Limited Heroism staying at 3 rather than 4 for the specific
  reason given above (a real cosmic-scale threat does get resolved here, unlike The First Law).
  Label "Grimdark" fits at the tier's upper end.
- Added to xlsx row 119, and to tier 8 on both index.html and es/index.html, appended after
  Fire Punch (exact score tie, existing-entry-first ordering matching the Attack on
  Titan/House of the Dragon/Dark Tower/Sweet Tooth precedent at Tier 7).

### 43. Sweet Tooth — Jeff Lemire — Comics, TV series

- Tier 7 (Extreme Dark Fantasy), Final Score 7.80 (Weighted Internal Score 2.8) — an exact
  numeric tie with Attack on Titan, House of the Dragon, and The Dark Tower, via a genuinely
  different profile from each (see neighbor check below).
- Scores: Structural Despair 3, Limited Heroism 3, Moral Cynicism 3, Structural Corruption 3,
  Redemption Difficulty 2, Narrative Acceptance of Injustice 2, Explicit Darkness 4.
- Rationale: scored against Jeff Lemire's 2009-2013 Vertigo comic (40 issues, 6 volumes) as the
  darker, defining version — the 2021-2024 Netflix adaptation is real but confirmed by multiple
  sources to be substantially gentler ("the show does not assume the overtly nihilistic tone of
  the comics," "the comic is particularly misanthropic, with nearly all human characters being
  monsters," vs. the show's "hopeful melancholy"), so it doesn't move any axis, matching how
  this session already handled other adaptation-lighter-than-source cases (Eragon's film, The
  Shannara Chronicles' and The Dresden Files' TV adaptations). Structural Despair (3) is
  grounded in the comic's completed ending: humanity goes fully extinct as a species over the
  following generations, succeeded entirely by the hybrids — not an averted threat but the
  story's actual, confirmed outcome. Limited Heroism (3) follows directly: Gus's personal
  journey succeeds completely (he survives, learns the truth, raises a thriving lineage), but no
  individual heroism changes or prevents the species-level outcome — matching "even the biggest
  victories are insufficient" precisely, since the extinction happens regardless of what any
  character does. Moral Cynicism (3) reflects the comic's specifically documented misanthropy —
  critics describe "nearly all human characters" as antagonistic or self-serving, Jepperd
  himself begins the story by selling Gus out for his own gain, and multiple distinct human-run
  operations (the Preserve's child dissection/experimentation, separate camps described as
  running "prostitution rings" using captive children) show predation on hybrid children as
  something closer to a norm than an aberration across the shattered post-plague world — a
  stronger, more pervasive "cruelty is rewarded/expected" case than a single corrupt faction.
  Structural Corruption (3) is carried by those same distinct exploitative operations. Redemption
  Difficulty (2) is Jepperd's arc: begins as, per multiple sources, "an amoral killer," becomes
  a genuine father figure, and dies protecting Gus — a real, costly, but ultimately *successful*
  redemption (his death is the price, not a failure), matching "exacts a real sacrifice" rather
  than RD3's "most fail" bar. Narrative Acceptance of Injustice (2) reflects that the story
  doesn't leave humanity's fate as an unresolved crisis to keep fighting — it's narratively
  accepted and even ritually honored (the elderly Gus tells the story to new generations,
  visiting the Precursors' burial site yearly) as history rather than an ongoing injustice,
  which is why this stays at 2 rather than 3 despite the underlying event's severity. Explicit
  Darkness reaches the ceiling (4) on specific, sourced content: children are "captured, abused,
  dissected, and killed," camps hold captive children for "prostitution rings," and reviewers
  describe "gory bullets to heads" and sustained graphic violence as a defining, not occasional,
  feature of the series.
- Cozy Fantasy = No. Hopepunk = No: matches precedent (no work at Tier 6 or darker carries the
  tag) — the completed story's own critical framing as "ultimately hopeful" applies to its
  long-term thematic resolution (life continues, just not as humans), not to found-family
  kindness organized as resistance to an institution.
- Scored against the complete, finished comic (all 40 issues); the Netflix show's own ending
  (season 3, 2024) is separately complete but, as established, tonally gentler throughout and
  doesn't affect any axis here.
- Neighbor check: none of the three other works tied at 7.80 share an identical per-axis
  profile. Attack on Titan's Limited Heroism 2 (a genuine, lasting diplomatic peace is achieved)
  sits below this entry's 3 (nothing reverses humanity's extinction), trading against this
  entry's Redemption Difficulty 2 vs. Titan's 3 (Jepperd's arc succeeds at cost; Titan's
  multiple redemption arcs are explicitly rare-and-partial). House of the Dragon's Structural
  Despair 2 and Structural Corruption 2 (a contained, single-dynasty succession war) both sit
  below this entry's 3 and 3 (a full species-level outcome and multiple distinct exploitative
  operations are more totalizing), trading against HotD's Redemption Difficulty 3 and Narrative
  Acceptance of Injustice 3 vs. this entry's 2 and 2 (HotD's core injustice is never resolved at
  all; Sweet Tooth's is resolved via succession, then ritually accepted). The Dark Tower's Moral
  Cynicism 2 sits below this entry's 3 (Dark Tower's antagonist force is cosmic/entropic rather
  than a pervasive "humans as monsters" thesis), trading against Dark Tower's Structural
  Corruption 2 vs. this entry's 3 (multiple distinct human-run exploitative operations here vs.
  one central institution there). Label check: "Extreme Dark Fantasy" fits at the tier's upper
  end — systemic cruelty toward children and a confirmed species-level extinction sit at a
  severity matching Titan, HotD, and Dark Tower, while the story's own quiet, generations-later
  acceptance keeps it just short of Tier 8's more totalizing bleakness.
- Added to xlsx row 118, and to tier 7 on both index.html and es/index.html, appended after The
  Dark Tower per score order (four-way tie at 7.80); title "Sweet Tooth" kept identical in EN
  and ES (no distinct Spanish-language title found — the Netflix release retains the English
  title in Latin American markets); medium: "Comics, TV series" / "Cómics, Serie de TV".
  Updated the Summary sheet's tier-7 count (5 → 6) and total-scored count (116 → 117 of 117).
  Updated the catalog-size mentions in both pages' meta/JSON-LD description tags (116 → 117).

### 42. Fourth Wing (The Empyrean) — Rebecca Yarros — Novels

- Tier 6 (Dark Fantasy), Final Score 6.7875 (Weighted Internal Score 2.35) — an exact numeric
  tie with Märchen Crown and The Grim Company (see the extended neighbor-check note below —
  this one is worth reading in full given the session's recent self-correction).
- Scores: Structural Despair 2, Limited Heroism 2, Moral Cynicism 2, Structural Corruption 3,
  Redemption Difficulty 2, Narrative Acceptance of Injustice 2, Explicit Darkness 4.
- **Bundle decision, per this queue item's own instruction to score each book and bundle only if
  they land in the same tier:** all three published books (Fourth Wing, Iron Flame, Onyx Storm)
  were assessed for tier consistency. The core institutional critique — Basgiath War College's
  lethal culling system and Navarre's centuries-long cover-up about the true nature of the war
  — is established by the end of Fourth Wing and simply escalates (not tonally shifts) across
  Iron Flame and Onyx Storm: more brutal tests, a deepening conspiracy, Xaden's venin-corruption
  arc. No book introduces a different register the way, say, Harry Potter's early volumes do
  relative to its finale; this is continuous escalation within one register, matching the
  reasoning already applied to Eragon earlier this session. Bundled as one entry.
- Rationale: Structural Corruption (3) is grounded in two distinct, textually-confirmed
  practices, not reviewer inference alone — (1) Basgiath's death-culling system, where an
  average 15% of conscripts die on the very first day (71 candidates in Fourth Wing's opening),
  only a quarter of Riders Quadrant cadets reach graduation, and cadets are permitted to kill
  each other during training; and (2) Navarre's leadership has "been lying to its citizens for
  hundreds of years" about the true enemy, willing "to sacrifice everyone on the borders... to
  stay safe" — an explicit, plot-confirmed centuries-long cover-up maintained "to maintain
  control." Two distinct corrupt practices administered by one government, not multiple
  independently-corrupt institutions (the Church-plus-Crown-plus-nobility pattern that earns
  ASOIAF's Structural Corruption 3 its own "irrecoverable" framing) — kept this short of the
  scale's ceiling anchor ("institutions exist, in practice, to sustain exploitation") since nothing
  in the confirmed text states the culling system's *purpose* is population control, only that
  reviewers read it that way. Redemption Difficulty (2) is carried by Xaden's arc: he begins
  turning venin at the end of Iron Flame, an active, ongoing corruption Violet is still fighting
  to reverse as of Onyx Storm — scored as a real, costly, in-progress struggle (matching "exacts
  a real sacrifice") rather than assuming either an unconfirmed success or an unconfirmed
  failure, since the series isn't finished. Explicit Darkness reaches the ceiling (4) on the
  sheer, sustained volume of named on-page cadet deaths documented across all three books, a
  structural and recurring feature of the series rather than an occasional beat.
- Cozy Fantasy = No. Hopepunk = No: matches precedent (no work at Tier 6 or darker carries the
  tag).
- Scored against the three published novels only (Fourth Wing 2023, Iron Flame 2023, Onyx Storm
  2025); the series is confirmed unfinished (5 books planned total, with book 4 in progress and
  a separate non-numbered Empyrean release announced for September 2026), so nothing from
  unpublished material is assumed either way.
- **Neighbor check, addressed at length given the session's recent Grim Company correction:**
  this profile landed as an *exact* per-axis match with Märchen Crown, and — after correcting
  Grim Company's Redemption Difficulty back to 2 earlier this session — with Grim Company too,
  producing a three-way exact match. Given the standing lesson (collision-avoidance must never
  be the reason a score changes), each axis was re-scrutinized independently before accepting or
  rejecting the match, not reflexively adjusted to escape it. Structural Corruption was tested
  at both 2 (matching House of the Dragon's "concentrated in one court" reasoning, since
  Navarre's corruption is administered by one government) and 4 (matching the "institutions
  exist to sustain exploitation" ceiling anchor, since reviewers explicitly read the culling
  system as serving population control) before settling on 3: SC2 undersold the specific,
  plot-confirmed centuries-long war-truth cover-up, and SC4 over-relied on a reviewer's
  interpretive reading rather than a textually explicit in-story claim about the culling
  system's purpose. Redemption Difficulty was tested at 3 (matching Grim Company's post-
  correction reasoning) but rejected: Xaden's arc is confirmed in-progress with real effort
  being spent on a cure, not confirmed to fail or land only partially the way RD3 requires. No
  axis survived re-scrutiny with a different, better-evidenced value, so the three-way tie
  stands as a legitimate coincidence — three genuinely different stories (a fairy-tale-court
  horror, a fading-magic revolution-cycles-into-tyranny epic, and a lethal war-college
  political-conspiracy romantasy) that happen to land at comparable severity on all seven
  independently-measured axes, not a sign any of the three was under-examined. Checked further
  against a non-adjacent Tier 6 work, The Sandman (6.1125): Sandman's Redemption Difficulty 3
  (Dream's cost is total and confirmed) sits above this entry's 2 (Xaden's cost is real but
  still being actively fought, not yet confirmed total), a clean, evidence-based gap. Label
  check: "Dark Fantasy... genuinely heavy without tipping into nihilism" fits — mass, sanctioned
  cadet death and a centuries-long government lie sit inside a story that still centers
  found-family, romance, and hard-won heroism.
- Added to xlsx row 117, and to tier 6 on both index.html and es/index.html, inserted
  immediately after The Grim Company per score order (exact tie); title "Fourth Wing (The
  Empyrean)" in EN, "Alas de Sangre (Empíreo)" in ES (the Spanish title of the first novel and
  the Spanish series name); medium: "Novels" / "Novelas". Updated the Summary sheet's tier-6
  count (19 → 20) and total-scored count (115 → 116 of 116). Updated the catalog-size mentions
  in both pages' meta/JSON-LD description tags (115 → 116).

### 41. The Princess Bride — William Goldman — Novel, Film

- Tier 2 (Bright Fantasy), Final Score 2.9625 (Weighted Internal Score 0.65) — an exact
  numeric tie with The Chronicles of Narnia and The Legend of Zelda, via a genuinely different
  profile from each (see neighbor check below).
- Scores: Structural Despair 0, Limited Heroism 0, Moral Cynicism 1, Structural Corruption 1,
  Redemption Difficulty 0, Narrative Acceptance of Injustice 1, Explicit Darkness 2.
- Rationale: covers William Goldman's 1973 novel and the beloved 1987 Rob Reiner film. The
  story itself resolves about as cleanly and triumphantly as this scale scores anything — Westley
  and Buttercup escape together, Inigo avenges his father by killing Count Rugen, Humperdinck's
  war-mongering murder plot is foiled — supporting the floor on Structural Despair, Limited
  Heroism, and Redemption Difficulty (there's no personal-corruption arc for any major
  character; Humperdinck is defeated and humiliated, not redeemed). Moral Cynicism and
  Narrative Acceptance of Injustice sit at 1 rather than 0 on a specific, textual basis
  distinct from the plot itself: Goldman's novel is framed as his own restoration of "the good
  parts" his father skipped when reading it to him as a child, built around an explicit,
  repeated thematic thesis — "life isn't fair... it's just fairer than death" — that directly
  argues against the "good guys always win, bad guys always get their comeuppance" worldview a
  simpler fairy tale would present uncomplicated. Goldman even appends a real aside musing that
  the characters likely didn't get an unambiguously happy ending long-term. That's a meta-level
  complication of pure just-world causality this scale doesn't usually see in otherwise-clean
  Tier 2 stories, even though the *told* story (the one Goldman actually chooses to narrate) is
  itself a full, unambiguous triumph. Explicit Darkness (2) reflects real, if
  comedically-framed, intensity: Westley's torture on The Machine, the "to the pain" speech
  (a vividly detailed mutilation threat), Buttercup's suicide attempt, and Inigo's father's
  murder are all genuine dark beats, but none are lingered on in a sustained, horror-coded way
  the way Willow/Legend's dedicated scary-villain aesthetics are — closer to "real danger,
  without extreme graphic detail" than a horror-adjacent register.
- Cozy Fantasy = No. Hopepunk = No: Humperdinck's scheme is one prince's individual plot rather
  than a systemic institutional critique (the Fierce shape doesn't fit), there's no
  adversity-free default-kindness world (Gentle doesn't fit), and the "life isn't fair" theme is
  a framing aside rather than an organizing meditation on mortality (Bittersweet doesn't fit).
- Neighbor check: neither of the two other works tied at 2.9625 shares an identical per-axis
  profile. Narnia's Structural Despair 1 (the White Witch's hundred-year winter, a real
  declining-world backdrop) and Redemption Difficulty 1 (Edmund's betrayal-and-forgiveness arc)
  both sit above this entry's 0 and 0 — Princess Bride has neither an ongoing world-decline
  premise nor a personal-redemption throughline — trading against this entry's Moral Cynicism 1
  and Narrative Acceptance of Injustice 1 vs. Narnia's 0 and 0 (Narnia's Christian-allegory
  just-world structure doesn't carry Goldman's meta-narrative "life isn't fair" complication).
  The Legend of Zelda's Structural Despair 1 and Limited Heroism 1 (each game's world requires
  saving from an active, recurring threat) sit above this entry's 0 and 0, trading against this
  entry's Moral Cynicism 1 and Narrative Acceptance of Injustice 1 vs. Zelda's 0 and 0 (episodic
  video-game heroics don't carry any equivalent authorial complication of the just-world
  premise). Label check: "Bright Fantasy" fits — a warm, comedic, triumphant fairy-tale
  adventure with a few genuinely dark beats and a knowing wink that real happy endings are
  rarer than stories pretend, without ever undermining its own told story's triumph.
- Added to xlsx row 116, and to tier 2 on both index.html and es/index.html, inserted between
  The Legend of Zelda and DanMachi per score order (exact tie); title "The Princess Bride" in
  EN, "La Princesa Prometida" in ES (the standard Spanish translation title); medium: "Novel,
  Film" / "Novela, Película". Updated the Summary sheet's tier-2 count (17 → 18) and
  total-scored count (114 → 115 of 115). Updated the catalog-size mentions in both pages'
  meta/JSON-LD description tags (114 → 115).

### 40. Eragon (The Inheritance Cycle) — Christopher Paolini — Novels, Film

- Tier 5 (Gloomy Fantasy), Final Score 5.2125 (Weighted Internal Score 1.65) — an exact numeric
  tie with the tier's floor cluster (Tales from Earthsea, A Knight of the Seven Kingdoms,
  Dragonlance, Harry Potter and the Goblet of Fire, Elantris, Baldur's Gate III), via a
  genuinely different profile from each (see neighbor check below).
- Scores: Structural Despair 1, Limited Heroism 1, Moral Cynicism 1, Structural Corruption 2,
  Redemption Difficulty 2, Narrative Acceptance of Injustice 2, Explicit Darkness 3.
- **Bundle-vs-split decision, addressed explicitly per this session's brief:** scored as one
  entry covering the full four-book main cycle (Eragon, Eldest, Brisingr, Inheritance) plus the
  2006 film, not split by book the way the Harry Potter series is on this catalog. The
  deciding difference from Harry Potter: HP's split rests on a well-documented, dramatic
  book-to-book escalation explicitly built into its marketing and reception (a children's
  mystery opener maturing into a war-and-genocide finale, with each individual book independently
  famous enough to be its own cultural reference point) — a real multi-tier gap between its
  first and last entries. The Inheritance Cycle's darkness intensifies too (see Explicit
  Darkness below) but stays within a single consistent YA-epic-fantasy register throughout,
  without HP's audience-shift thesis or the individual-book fame that would make readers
  reasonably expect a separate score per volume. A rough independent estimate of Eragon (Book 1)
  alone — a considerably gentler farm-boy-finds-a-dragon-egg opener, frequently compared to Star
  Wars and Anne McCaffrey's Dragonriders of Pern — suggests it would land around Tier 3, roughly
  two tiers below this bundled score; real, but a smaller and less culturally-marked gap than
  HP's, so bundling (matching how The Stormlight Archive, The Wheel of Time, and A Song of Ice
  and Fire are all treated as single entries on this catalog despite real internal escalation)
  is the more consistent call.
- Rationale: Structural Corruption (2) comes from King Galbatorix's century-long tyranny —
  seized through his own genocide of the Dragon Riders decades before the story starts, enforced
  by the Ra'zac as a secret-police-style hunting apparatus — a real, sustained institutional
  case, though concentrated in one usurped kingdom rather than multiple independently-corrupt
  institutions. Redemption Difficulty (2) is carried by Murtagh's arc: bound into forced service
  to Galbatorix against his will, his path to freedom requires literally changing his own
  fundamental self-identity (his "true name") — a real, costly transformation, ultimately
  achieved. Narrative Acceptance of Injustice (2) reflects a specific, deliberate ending choice:
  Galbatorix's immediate tyranny is fully defeated, but the deeper injustice — the historic
  genocide of the old Dragon Rider order — is never undone; Eragon and Saphira instead found an
  *entirely new* order in a distant land, explicitly because Alagaësia itself isn't yet safe or
  ready for Riders to return, which reads as "the old injustice persists; a hopeful but separate
  new beginning is offered instead" rather than a clean fix. Explicit Darkness (3) is grounded in
  a specific, reviewer-flagged pattern: extensive, graphic on-page torture of named female
  characters recurs and escalates across the series (Arya "burned, punctured, drugged, branded"
  in Eldest; Nasuada's "brutal disfiguring and dehumanizing torture" in the finale) — critics
  explicitly describe this as "a crutch" the author leans on repeatedly, not an isolated beat.
- **On the 2006 film adaptation:** widely regarded as a poor, heavily simplified adaptation that
  strips out most of the book's plot, characters, and complexity ("the blandest, hollowest
  hero's journey," "arguably the worst book to movie adaptation"). Since it's tonally *lighter*
  than the books rather than darker, it doesn't move any axis — the same principle applied to
  The Dresden Files and The Shannara Chronicles earlier this session: a gentler adaptation
  doesn't lower a score set by a darker primary source, just as a darker adaptation (Dirk
  Gently's 2016 series, The Dark Crystal: Age of Resistance) can raise one.
- Cozy Fantasy = No. Hopepunk = No: classic heroic-fantasy virtue-rewarded structure, but not
  organized around kindness as deliberate resistance praxis to an institution (the Fierce shape)
  or built around mortality/time as an organizing meditation.
- Neighbor check: none of the six other works tied at 5.2125 share an identical per-axis
  profile. A Knight of the Seven Kingdoms' Structural Despair 2 and Redemption Difficulty 1 swap
  against this entry's 1 and 2 (Murtagh's forced-identity-change arc is costlier than anything in
  Dunk & Egg's more contained political intrigue). Dragonlance and Elantris both trade
  Structural Despair 2/Narrative Acceptance of Injustice 1 against this entry's 1/2 (their
  central conflicts resolve more completely than the Riders' unaddressed genocide does).
  Checked further against a non-adjacent Tier 5 work, The Magicians (5.8875, the tier's
  ceiling): The Magicians scores higher specifically via Limited Heroism 2 and Redemption
  Difficulty 2 combined with real unresolved psychological damage (depression, addiction) that
  Eragon's more classically-heroic, cleanly-won conflict doesn't carry — a sensible ordering
  within the tier. Label check: "Gloomy Fantasy" fits — real, escalating institutional cruelty
  and an unresolved historical genocide sit alongside a fundamentally triumphant, hopeful heroic
  arc.
- Added to xlsx row 115, and to tier 5 on both index.html and es/index.html, inserted into the
  tier's floor cluster (exact tie at 5.21 displayed); title "Eragon (The Inheritance Cycle)" in
  EN, "Eragon (El Legado)" in ES (the Spanish series title, "El Legado" — book titles themselves
  keep their English names in translation); medium: "Novels, Film" / "Novelas, Película".
  Updated the Summary sheet's tier-5 count (21 → 22) and total-scored count (113 → 114 of 114).
  Updated the catalog-size mentions in both pages' meta/JSON-LD description tags (113 → 114).

### 39. The Dark Tower — Stephen King — Novels

- Tier 7 (Extreme Dark Fantasy), Final Score 7.80 (Weighted Internal Score 2.8) — an exact
  numeric tie with Attack on Titan and House of the Dragon, via a genuinely different profile
  from each (see neighbor check below).
- Scores: Structural Despair 3, Limited Heroism 3, Moral Cynicism 2, Structural Corruption 2,
  Redemption Difficulty 3, Narrative Acceptance of Injustice 3, Explicit Darkness 4.
- Rationale: the complete 8-book series (The Gunslinger through The Dark Tower, plus The Wind
  Through the Keyhole). Reality's decay ("the world has moved on") is the series' single most
  explicit, repeated, author-confirmed theme — King himself has described the Crimson King as a
  direct embodiment of "chaos and entropy" — but Structural Despair stops short of the ceiling
  (3, not 4) because Roland's quest is shown genuinely stabilizing the Tower by the end, a real
  achieved improvement, not a world where nothing can alter the trajectory. That distinction is
  exactly why Limited Heroism and Narrative Acceptance of Injustice carry the story's real
  bleakness instead: Roland reaches the Tower — succeeds, by any conventional measure — and is
  immediately reset to the desert at the start of his quest, implying he has done this before,
  possibly many times, with no confirmation the cycle ever actually ends (critics describe
  whether he "succeeded" as explicitly left unanswered). That's about as direct a match for
  "even the biggest victories are insufficient" as this scale has scored, and Redemption
  Difficulty (3) follows the same logic: Roland's arc toward genuine love and connection (his
  ka-tet, replacing his old ruthlessness) is real, but the loop's implication that he hasn't yet
  earned a different outcome — despite carrying the Horn of Eld this time as a sliver of hope —
  keeps his redemption unresolved rather than achieved. Structural Corruption (2) is grounded in
  a specific institutional case distinct from the series' cosmic-scale themes: the Wolves of the
  Calla, a sustained, organized child-theft practice (children returned "roont" — mentally and
  physically ruined) enforced by a hidden power connected to the Crimson King's forces, not an
  isolated crime. Explicit Darkness sits at the ceiling (4) on King's characteristically visceral
  and sustained horror content across eight books — the Low Men, Mordred (a monstrous
  spider-child who kills and feeds on people including his own surrogate mother), and repeated
  graphic violence throughout.
- Cozy Fantasy = No. Hopepunk = No: matches precedent (no work at Tier 6 or darker carries the
  tag).
- Scored against the complete 8-book main series (the connective tissue linking most of King's
  other work is acknowledged but not itself in scope for this entry).
- Neighbor check: Attack on Titan's Limited Heroism 2 (a genuine, lasting diplomatic peace is
  achieved) sits below this entry's 3 (Roland's own victory doesn't durably resolve anything for
  him personally), while Titan's Moral Cynicism 3 and Structural Corruption 3 (idealism
  repeatedly, brutally punished; multi-institutional societal rot) both sit above this entry's 2
  and 2 — Dark Tower's antagonist force is cosmic/entropic rather than a critique of specific
  political institutions the way Titan's is. House of the Dragon's Structural Despair 2 and
  Moral Cynicism 3 differ from this entry's 3 and 2 in exactly opposite directions — HotD's
  succession war is a contained, single-dynasty tragedy where honor is systematically punished
  by court politics, while Dark Tower's despair is cosmological rather than political, and no
  single act of court cynicism drives its plot the way the Hightower coup drives HotD's. Checked
  further against a non-adjacent Tier 7 work, His Dark Materials (7.4625): this entry's
  Structural Despair 3 and Redemption Difficulty 3 both sit above HDM's 2 and 2 (reality-decay
  as a repeated, explicit, book-spanning thesis is a more totalizing condition than HDM's
  contained Dust-crisis, and Roland's unresolved cyclical redemption is less certain than Mrs.
  Coulter's costly-but-successful one), offset by this entry's Structural Corruption 2 sitting
  below HDM's 3 (the Magisterium's intercision program is a cleaner, more centralized
  institutional-design case than the Calla Wolves' more contained practice) — a sensible,
  evidence-based ordering. Label check: "Extreme Dark Fantasy" fits — cosmic-scale decay,
  extensive visceral horror, and an ending that refuses easy resolution sit at the tier's
  established severity, alongside Titan and HotD.
- Added to xlsx row 114, and to tier 7 on both index.html and es/index.html, appended after
  House of the Dragon per score order (three-way tie at 7.80); title "The Dark Tower" in EN, "La
  Torre Oscura" in ES (the standard Spanish title used across all translated editions); medium:
  "Novels" / "Novelas". Updated the Summary sheet's tier-7 count (5 → 6) and total-scored count
  (112 → 113 of 113). Updated the catalog-size mentions in both pages' meta/JSON-LD description
  tags (112 → 113).

### 38. The Grim Company — Luke Scull — Novels

- Tier 6 (Dark Fantasy), Final Score 6.7875 (Weighted Internal Score 2.35) — an exact numeric
  tie with Märchen Crown and The Dark Crystal: Age of Resistance.
- Scores: Structural Despair 2, Limited Heroism 2, Moral Cynicism 2, Structural Corruption 3,
  Redemption Difficulty 2, Narrative Acceptance of Injustice 2, Explicit Darkness 4.
- Rationale: complete trilogy (The Grim Company, Sword of the North, Dead Man's Steel), an
  explicitly self-identified grimdark series reviewers repeatedly compare to Joe Abercrombie's
  The First Law (already Tier 9 on this scale) — "no-one does grimdark fantasy better than Joe
  Abercrombie, but... Scull comes incredibly close." Structural Corruption (3) rests on more
  than the initial 500-years-dead-gods/tyrant-magelord premise: book 2 shows the rebels'
  victorious liberation of Dorminia curdling into an equally absolute new tyranny under the
  White Lady ("anyone perceived as a threat seized and imprisoned or exiled"), and book 3 shows
  Dorminia conquered outright by the Fade — a specific, textually-confirmed "toppling one tyrant
  just installs the next" pattern, not a static backdrop. Redemption Difficulty (2) is carried
  by Davarus Cole's arc: a godly essence residing in him grows stronger with every death that
  "feeds it," meaning battlefield survival itself risks eroding who he is — a genuinely costly,
  ongoing struggle against self-corruption, matching "possible, but exacts a real sacrifice"
  rather than a rarer, mostly-failing pattern (no confirmed evidence his arc specifically fails
  or only partially succeeds — see correction note below). Explicit Darkness reaches the ceiling
  (4) on strong, repeated reviewer language ("amazingly violent," "two parts amoral,
  ultra-violent fantasy," "gore and borderline horror scenes") sustained across all three books.
- Cozy Fantasy = No. Hopepunk = No: matches precedent (no work at Tier 6 or darker carries the
  tag).
- Scored against the complete, published trilogy — Luke Scull has indicated interest in
  additional standalone books in the same setting, but none are part of this entry.
- **Same-session correction:** this entry originally scored Redemption Difficulty at 3 (not 2),
  landing at 7.125, Tier 7. That revision was made specifically because the profile had landed
  as an exact per-axis match with Märchen Crown — the standing review practice's own red flag —
  and, on the first pass, "Cole's ongoing self-erosion arc" plus "almost everyone in the
  ensemble is killed off by the final book" were treated as sufficient grounds to move from
  RD2 to RD3. On reflection (prompted by a direct question about why this session's last three
  additions had all landed in Tier 7), that reasoning doesn't hold up: neither piece of evidence
  actually confirms Cole's *redemption specifically* fails or lands only partially — a costly,
  ongoing struggle is exactly what RD2's anchor already describes, and general trilogy-wide
  carnage isn't the same claim as a named character's arc failing. The tell, in hindsight, was
  that the log entry itself justified the revision partly by noting it "moved the total off the
  Märchen Crown match" — evidence should drive a score change, not the other way around. Reverted
  to RD2, landing back at Tier 6, tied exactly with Märchen Crown — which is a legitimate
  coincidence, not a problem: the two works reach comparable severity via genuinely different
  content (fairy-tale-court intimate horror vs. a tyranny-replaces-tyranny political cycle plus
  cosmic invasion), and Tier 6 fits the critical consensus ("some felt it wasn't grimdark
  enough... lacking the grimdark blurring of good and evil") better than Tier 7 did.
- Neighbor check (post-correction): Märchen Crown's profile is now an exact match — addressed
  directly above rather than papered over. Checked against a non-adjacent Tier 6 work, The
  Sandman (6.1125): Sandman's Redemption Difficulty 3 (Dream's arc costs him his literal
  existence, a textually confirmed, completed cost) is a stronger, more direct case than
  anything confirmed for Grim Company, supporting this entry's more conservative RD2. Label
  check: "Dark Fantasy... genuinely heavy without tipping into nihilism" fits better than Tier
  7's "Extreme" framing did, matching reviewers' own hedged read on the book's grimdark
  credentials.
- Added to xlsx row 113 (tier corrected from 7 to 6), and to tier 6 on both index.html and
  es/index.html (moved out of the tier-7 section into tier 6, tied with Märchen Crown and The
  Dark Crystal: Age of Resistance); title "The Grim Company" kept identical in EN and ES (no
  Spanish-language edition found); medium: "Novels" / "Novelas". This correction itself updated
  the Summary sheet's tier-6 count (18 → 19, the state after The Dark Tower's addition) and
  tier-7 count (6 → 5); total-scored count and the pages' catalog-size mentions are unaffected
  by a tier move and remain at 113 of 113.

### 37. The Dresden Files — Jim Butcher — Novels, TV series

- Tier 6 (Dark Fantasy), Final Score 6.1125 (Weighted Internal Score 2.05) — an exact numeric
  tie with Re:Zero, Clevatess, and The Sandman, via a genuinely different profile from each (see
  neighbor check below).
- Scores: Structural Despair 1, Limited Heroism 2, Moral Cynicism 2, Structural Corruption 2,
  Redemption Difficulty 2, Narrative Acceptance of Injustice 2, Explicit Darkness 4.
- Rationale: scored against the 18 currently-published novels (of a planned 25, the series
  remains ongoing as of Twelve Months, January 2026) plus the 2007 SciFi Channel adaptation —
  the show is real but tonally lighter and looser than the source ("nothing like the books" per
  contemporary reviews), so it doesn't push any axis higher than the novels already set. Limited
  Heroism sits at 2: Harry wins each book's immediate crisis, but at real, escalating personal
  cost (his body crippled and only restored via a Faustian bargain with the Winter Queen), and
  each defeated villain reveals a larger one behind it (Denarians, the Black Council, the
  Outsiders) — a durable "resolves the threat, deeper condition intact" pattern rather than
  structural fixes. Moral Cynicism (2) reflects the story's own central moral compromise: in
  *Changes*, Harry personally triggers a bloodline curse that wipes out the entire Red Court
  vampire nation — including, implicitly, non-combatants caught in that bloodline — as the only
  way to save his daughter, cutting his former lover's throat to do it. That's the protagonist
  himself committing a magically genocidal act as the story's own resolution, not a villain's
  crime, a real "the world rewards ruthless pragmatism" data point distinct from a merely neutral
  moral physics. Structural Corruption (2) comes from the White Council's own justice system,
  which executes practitioners (including its own members) after "a brief trial" for breaking
  the Laws of Magic — Harry himself narrowly avoided this for killing his abusive mentor in
  self-defense — a real, notorious institutional harshness, though the Council isn't purely
  villainous (Harry has genuine allies within it), keeping this short of a multi-institution
  Structural Corruption 3. Redemption Difficulty (2) is carried across the ensemble: Harry's own
  ongoing struggle against the Winter Knight mantle's corrupting influence is a continuous, costly
  battle rather than a one-time fix, and his apprentice Molly Carpenter's fall into forbidden
  mind magic costs her years of consequence and atonement. Explicit Darkness reaches the ceiling
  (4): the Red Court are predatory on-page killers, the Denarians are literal serial-killer-tier
  villains possessed by fallen angels, and the *Changes* throat-cutting and its citywide
  magical-war aftermath are sustained, visceral content recurring across nearly the entire
  18-book run, not an isolated beat.
- Cozy Fantasy = No. Hopepunk = No: matches precedent (no work at Tier 6 or darker carries the
  tag) — found-family loyalty is real and central, but the surrounding institutional harshness
  and the protagonist's own genocide-adjacent moral compromise sit past the point where
  "kindness as the organizing response" is the most honest one-line description.
- Scored against the currently-published 18 novels; the series is explicitly unfinished (7 more
  volumes planned as of this entry), so later escalations aren't factored in, matching how this
  catalog treats other ongoing series (Märchen Crown, The Stormlight Archive before its
  post-promotion correction).
- Neighbor check: Re:Zero's Structural Despair 2 (demi-human oppression as an ongoing societal
  backdrop) sits above this entry's 1 — Dresden's supernatural society has harsh laws but no
  equivalent persecuted-underclass throughline — trading against this entry's Limited Heroism 2
  vs. Re:Zero's 1 (Re:Zero's Return-by-Death mechanic is a genuinely more corrective fix than
  Dresden's escalating-threat pattern). Clevatess's Structural Despair 2 and Redemption
  Difficulty 1 (a more central, more successful found-family redemption arc) both differ from
  this entry's 1 and 2 in offsetting directions. The Sandman's Redemption Difficulty 3 (Dream's
  arc costs him his literal existence) sits above this entry's 2, trading against The Sandman's
  Structural Corruption 1 vs. this entry's 2 (Heaven/Hell's mythic-scale politics in The Sandman
  vs. the White Council's concrete, on-page execution practice here). Checked further against a
  non-adjacent Tier 6 work, Supernatural (6.90, added earlier this session, the closest tonal
  cousin as another urban-fantasy monster-hunter): Supernatural's Moral Cynicism 3 and Structural
  Corruption 3 (a textually-confirmed, actively malevolent God orchestrating events across three
  cosmic institutions) both sit above this entry's 2 and 2 — Dresden's White Council is harsh but
  not portrayed as secretly malevolent by design — while this entry's Explicit Darkness 4 sits
  above Supernatural's 3 (prose fiction's page can sustain a level of visceral detail broadcast
  TV's standards-and-practices couldn't). Label check: "Dark Fantasy... genuinely heavy without
  tipping into nihilism" fits — real horror and moral compromise sit alongside Harry's persistent
  wisecracking, found-family loyalty, and heroism.
- Added to xlsx row 112, and to tier 6 on both index.html and es/index.html, inserted
  immediately after The Sandman per score order (exact tie); title "The Dresden Files" in EN,
  "Los Archivos Dresden" in ES (the title used across the Spanish-language editions); medium:
  "Novels, TV series" / "Novelas, Serie de TV". Updated the Summary sheet's tier-6 count
  (17 → 18) and total-scored count (110 → 111 of 111). Updated the catalog-size mentions in both
  pages' meta/JSON-LD description tags (110 → 111).

### 36. His Dark Materials — Philip Pullman — Novels, TV series

- Tier 7 (Extreme Dark Fantasy), Final Score 7.4625 (Weighted Internal Score 2.65) — the new
  tier-7 floor, just below The Stormlight Archive (7.575).
- Scores: Structural Despair 2, Limited Heroism 3, Moral Cynicism 2, Structural Corruption 3,
  Redemption Difficulty 2, Narrative Acceptance of Injustice 3, Explicit Darkness 4.
- Rationale: covers Philip Pullman's trilogy (Northern Lights, The Subtle Knife, The Amber
  Spyglass) and the faithful 2019-2022 BBC/HBO adaptation. Limited Heroism and Narrative
  Acceptance of Injustice are both unusually high for this scale on a specific, textually
  explicit basis, not an assumption: the trilogy's own ending states outright that Lord Asriel's
  entire multiverse-spanning war against Heaven and the Magisterium "would have failed anyway"
  as a strategy — research into the ending confirms "the Church is not really gone" and that
  "getting rid of the Magisterium is not the only part of building the Republic," with the
  actual resolution reframed as an incomplete, indefinite, personal-scale task ("we have to
  build the Republic of Heaven where we are") rather than an institutional victory. That's about
  as direct a textual match for Limited Heroism's "even the biggest victories are insufficient"
  anchor as this scale has scored, and it drives Narrative Acceptance of Injustice to 3 in
  parallel: the Magisterium's institutional evil is explicitly left standing, an ongoing
  structural condition rather than a defeated one. Structural Corruption sits at 3: the
  Magisterium is a totalitarian church-state controlling governments, education, and research
  across the story's worlds, and its "intercision" program — surgically severing children from
  their dæmons, run as sanctioned institutional policy under the General Oblation Board, not a
  rogue faction's crime — is as clean a "central institutions exist to sustain exploitation" case
  as this scale has scored. Redemption Difficulty (2) is carried by Mrs. Coulter, an established
  child-abuser (including of her own daughter) whose final act — sacrificing her life alongside
  Lord Asriel to destroy the angel Metatron, motivated by love rather than self-interest — is
  widely read by critics as "a redemption of a kind," achieved but only at the cost of her life,
  matching the "real sacrifice: loss, pain, renunciation" anchor precisely. Explicit Darkness
  reaches the ceiling (4): intercision recurs as a central plot engine across the trilogy (not
  an isolated incident), and Lord Asriel sacrificing his own son Roger's life to power the
  experiment that tears open the sky is one of the more shocking single moments in mainstream YA
  fantasy, alongside real war-in-heaven battle content and the literal death of God.
- Cozy Fantasy = No. Hopepunk = No: matches precedent (no work at Tier 6 or darker carries the
  tag) — Lyra and Will's love and moral growth are real, but the story's own ending explicitly
  argues against "the grand crusade" as the right shape for hope, which is close to the opposite
  of Fierce Hopepunk's thesis that organized resistance is the causally correct, effective
  strategy.
- Scored against the complete trilogy and its full television adaptation, not the standalone
  companion novels (La Belle Sauvage, The Secret Commonwealth), which sit outside this entry's
  scope.
- Neighbor check: The Stormlight Archive's Redemption Difficulty 3 ("rare, most who seek it fail
  or achieve it only partially," its own established reasoning) sits above this entry's 2 — a
  specific gap, since Mrs. Coulter's redemption arc actually *succeeds* at real cost rather than
  failing or landing only partially, a less bleak case than Stormlight's pattern — trading
  against this entry's Explicit Darkness 4 vs. Stormlight's 3 (intercision's sustained,
  central-to-the-plot cruelty against children is a more concentrated horror than Stormlight's
  more diffuse epic-fantasy violence). Checked further against a non-adjacent Tier 7 work,
  Attack on Titan (7.80): Attack on Titan's Structural Despair 3 and Moral Cynicism 3 both sit
  above this entry's 2 and 2 (Titan's world is cosmologically bleaker and its moral physics more
  actively punish idealism than anything in Pullman's trilogy, where individual virtue —
  Lyra's honesty, Will's courage — is treated as genuinely meaningful even though it can't fix
  institutions), while this entry's Explicit Darkness 4 matches Titan's — a sensible ordering
  given the two works' different registers. Label check: "Extreme Dark Fantasy" fits — genuine
  institutional child abuse and a war that explicitly fails sit at a severity distinctly above
  Tier 6's "heavy without tipping into nihilism," while the story's persistent warmth (love,
  personal growth, the ongoing possibility of building something better) keeps it short of
  Tier 8's more totalizing bleakness.
- Added to xlsx row 111, and to tier 7 on both index.html and es/index.html, inserted as the new
  first (lowest-scoring) entry in the tier, before The Stormlight Archive; title "His Dark
  Materials" in EN, "La Materia Oscura" in ES (the official Spanish trilogy title); medium:
  "Novels, TV series" / "Novelas, Serie de TV". Updated the Summary sheet's tier-7 count (3 → 4)
  and total-scored count (109 → 110 of 110). Updated the catalog-size mentions in both pages'
  meta/JSON-LD description tags (109 → 110).

### 35. The Dark Crystal: Age of Resistance — Jim Henson & Frank Oz — TV series

- Tier 6 (Dark Fantasy), Final Score 6.7875 (Weighted Internal Score 2.35) — an exact numeric
  tie with Märchen Crown, via a genuinely different profile (see neighbor check below). Notably
  darker than its own parent film, The Dark Crystal (Tier 4, 4.20, added earlier this session).
- Scores: Structural Despair 3, Limited Heroism 2, Moral Cynicism 2, Structural Corruption 3,
  Redemption Difficulty 0, Narrative Acceptance of Injustice 3, Explicit Darkness 4.
- Rationale: this 2019 Netflix prequel (10 episodes, cancelled after one season) is bound by a
  structural constraint the film isn't: as a prequel to a story that already establishes the
  Gelfling race is nearly wiped out and the Skeksis rule unchecked for a thousand years, Season
  1's real, hard-won victory (the Gelfling clans unite for the first time and force a Skeksis
  retreat) is inescapably read against a known, doomed future — a specific, textually-grounded
  reason Structural Despair (3) and Narrative Acceptance of Injustice (3) both sit well above
  the film's Structural Despair 2 / Narrative Acceptance of Injustice 1. The season also
  establishes the Darkening (an active, spreading corruption of Thra caused by the Skeksis'
  crystal misuse) as an ongoing, worsening condition, not a static backdrop. Structural
  Corruption matches the film's 3 for the same reason established there: the Skeksis are Thra's
  only shown ruling power, and this season depicts the exploitative machinery (systematic
  essence-draining, the Garthim army under construction) being actively built out, if anything
  more explicitly than the film's post-hoc thousand-year status quo. Redemption Difficulty stays
  at the film's 0 — Season 1 doesn't center a personal moral-repair arc for any major character;
  it's a story about a collective uprising, not individual redemption. Explicit Darkness reaches
  the ceiling (4), one level above the film's 3, on specific critical consensus: reviewers
  repeatedly describe the show as pushing further than the film into "torture, disfigurement,
  and violence that are genuinely unpleasant," including a sustained, graphic on-screen sequence
  of a sympathetic character's essence being drained and her body disintegrating — critics
  specifically called it "Game of Thrones for a younger audience," and the 10-episode format
  sustains that intensity across far more runtime than the film's 93 minutes could.
- Cozy Fantasy = No. Hopepunk = No: the season's central shape (formerly-divided Gelfling clans
  choosing unity as their resistance strategy against the Skeksis) is arguably a closer
  numerical fit for Fierce Hopepunk than the film's solitary-quest structure, but Limited
  Heroism and Moral Cynicism don't sit at the floor the way that shape requires (Avatar's LH1/
  MC1), and this entry lands at Tier 6 — matching the established precedent that no work at this
  severity or darker carries the tag, since the surrounding content dominates enough page-time
  that "kindness as the organizing response" stops being the most honest description.
- Scored against the complete, aired Season 1 only — the series was cancelled before a second
  season, so later chapters of the Gelfling resistance (and its established eventual defeat)
  are not part of the scored text, matching how this catalog treats other cancelled shows (The
  Shannara Chronicles, earlier this session).
- Neighbor check: Märchen Crown's Redemption Difficulty 2 sits above this entry's 0 (no
  comparable personal-repair arc exists in this season), trading against this entry's Structural
  Despair 3 and Narrative Acceptance of Injustice 3 vs. Märchen Crown's 2 and 2 (Märchen Crown's
  ongoing serialized story doesn't carry Age of Resistance's specific certain-doom prequel
  structure) — the three-axis difference nets to the same total via independently-reasoned
  gaps, not a coincidence. Checked further against a non-adjacent Tier 6 work, The Sandman
  (6.1125, added earlier this session): The Sandman's Redemption Difficulty 3 (Dream's arc costs
  him his literal existence) sits well above this entry's 0, while this entry's Structural
  Despair 3 and Narrative Acceptance of Injustice 3 both sit above The Sandman's 1 and 2 (The
  Sandman's ending is explicitly cyclical/restorative — Daniel's succession — while this entry's
  known future is straightforwardly worse) — a sensible ordering between two works that reach
  a similar total through very different content. Label check: "Dark Fantasy... genuinely heavy
  without tipping into nihilism" fits — the season's own ending keeps real hope alive (the
  clans' unity is portrayed as meaningful, not futile), and the wider two-work Dark Crystal
  story eventually does restore balance, even though this chapter is the bleakest part of it.
- Added to xlsx row 110, and to tier 6 on both index.html and es/index.html, inserted
  immediately after Märchen Crown per score order (exact tie); title "The Dark Crystal: Age of
  Resistance" in EN, "Cristal oscuro: La era de la resistencia" in ES (Netflix's own regional
  title for the series — notably using "Cristal oscuro," the Spain-dub name, rather than "El
  cristal encantado," the Latin American dub name used for the 1982 film, a genuine
  inconsistency in the source material reflected here rather than smoothed over); medium: "TV
  series" / "Serie de TV". Updated the Summary sheet's tier-6 count (16 → 17) and total-scored
  count (108 → 109 of 109). Updated the catalog-size mentions in both pages' meta/JSON-LD
  description tags (108 → 109).

### 34. The Dark Crystal — Jim Henson & Frank Oz — Film

- Tier 4 (Fantasy in Gray Tones), Final Score 4.20 (Weighted Internal Score 1.2) — an exact
  numeric tie with The NeverEnding Story and Once Upon a Time, via a genuinely different profile
  from each (see neighbor check below).
- Scores: Structural Despair 2, Limited Heroism 0, Moral Cynicism 0, Structural Corruption 3,
  Redemption Difficulty 0, Narrative Acceptance of Injustice 1, Explicit Darkness 3.
- Rationale: scored as the 1982 film only — the 2019 Netflix prequel series, Age of Resistance,
  is queue item #35 and out of scope here. Structural Corruption is the profile's standout value
  at 3: the Skeksis aren't one corrupt faction among legitimate institutions, they *are* Thra's
  only shown ruling power, and their thousand-year reign is defined entirely by exploitation —
  systematically draining the life-essence of Podlings and Gelflings to extend their own lives,
  having already carried out a near-total genocide of the Gelfling race before the film even
  starts (Jen and Kira are the last two). That's "injustice embedded in central institutions"
  with no competing legitimate power shown at all, a stronger case than the more common
  "anomalous usurping tyrant" pattern this scale usually scores at Structural Corruption 1
  (e.g. Willow's Bavmorda). Against that: Limited Heroism and Moral Cynicism both sit at the
  floor (0) because Jen's quest achieves about as complete a resolution as this scale has
  scored — not just stopping the Skeksis but healing the millennium-old cosmic wound at its
  root, reuniting the Skeksis and their opposite-selves the Mystics back into a single
  transcendent species (the urSkeks), with Kira's apparent death at the climax explicitly undone
  by the ending rather than left as a cost. Redemption Difficulty sits at 0 for a specific
  reason distinct from "reforms easily": there isn't a character-level moral-repair arc in this
  film at all — the Skeksis don't individually repent, they're cosmically reintegrated into
  something that transcends the good/evil split, a different construct than personal redemption.
  Explicit Darkness reaches 3 on well-documented grounds: the Skeksis' exaggerated physical
  decay, the essence-draining sequences (visually a form of vampiric body-horror), and
  specifically SkekTek's mind-wipe of a captured Podling (hair whitening, face caving in, eyes
  glazing over) are widely cited by retrospective reviews as "uncomfortably dark" and
  "traumatic nightmare fuel" for an ostensibly family-rated 1982 film.
- Cozy Fantasy = No. Hopepunk = No, despite a numeric profile that superficially resembles the
  Fierce Hopepunk shape (real institutional oppression + Limited Heroism/Moral Cynicism both at
  the floor): considered and rejected on narrative-shape grounds, not just the numbers. Fierce
  Hopepunk requires kindness/community organized *as resistance praxis* (Avatar's found-family
  actively opposing empire); Jen's story is a solitary prophesied quest resolved through
  mythic-fantasy mechanics (finding a shard, a cosmic conjunction), not collective kindness
  chosen as a deliberate strategy against the Skeksis.
- Neighbor check: The NeverEnding Story's Limited Heroism 1 and Redemption Difficulty 2 (Bastian's
  own costly corruption arc) both sit above this entry's 0 — a specific gap, since this film has
  no comparable personal-corruption throughline for its protagonist — trading against this
  entry's Structural Corruption 3 vs. NES's 0 (NES's Nothing is an existential/cosmic threat,
  not an institutional one, the opposite shape). Once Upon a Time's Redemption Difficulty 2
  (Regina's and Rumpelstiltskin's costly arcs) also sits above this entry's 0, trading against
  this entry's Structural Corruption 3 vs. OUAT's 1 (OUAT's corrupt rulers are each individually
  anomalous and correctable, not one totalizing regime). Checked further against a non-adjacent
  Tier 4 work, The Shannara Chronicles (4.875, added earlier this session, the closest peer for
  "real institutional persecution" among this session's additions): Shannara's Narrative
  Acceptance of Injustice 2 (the Crimson's persecution thread stays open due to the show's
  cancellation) sits above this entry's 1 (the genocide's demographic damage isn't undone, but
  the ending's "Jen and Kira will rebuild" framing is explicitly hopeful and resolution-oriented,
  not left ambivalent), while this entry's Limited Heroism 0 sits well below Shannara's 1 — a
  clean, complete mythic resolution vs. Shannara's real-world production accident leaving things
  open. Label check: "Fantasy in Gray Tones (high stakes, real losses, but still high hope)"
  fits — a genuinely severe, embedded institutional evil and a completed genocide sit inside a
  story that ends in total restoration.
- Added to xlsx row 109, and to tier 4 on both index.html and es/index.html, inserted
  immediately after Once Upon a Time per score order (exact tie); title "The Dark Crystal" in
  EN, "El cristal encantado" in ES (the Latin American dub title, matching this catalog's
  existing preference for the Latin American title when it differs from Spain's — Spain uses
  "Cristal oscuro"); medium: "Film" / "Película". Updated the Summary sheet's tier-4 count
  (20 → 21) and total-scored count (107 → 108 of 108). Updated the catalog-size mentions in both
  pages' meta/JSON-LD description tags (107 → 108).

### 33. Charmed — Constance M. Burge — TV series

- Tier 4 (Fantasy in Gray Tones), Final Score 4.65 (Weighted Internal Score 1.4) — an exact
  numeric tie with Earthsea, Avatar: The Last Airbender, Final Fantasy XII, and Grimgar: Ashes
  and Illusions, via a genuinely different profile from each (see neighbor check below).
- Scores: Structural Despair 1, Limited Heroism 1, Moral Cynicism 1, Structural Corruption 1,
  Redemption Difficulty 2, Narrative Acceptance of Injustice 2, Explicit Darkness 2.
- Rationale: the original 1998-2006 WB/CW series (the 2018 CW reboot is a separate production
  and out of scope for this entry). The Halliwell sisters' "can't use magic for personal gain"
  rule is close to an explicit, mechanical just-world guarantee, keeping Moral Cynicism low (1);
  the demonic hierarchy (the Source, the Triad) is straightforwardly evil rather than a
  corrupted-from-legitimate institution, keeping Structural Corruption low (1) — the "Elders,"
  the show's good-aligned governing council, are shown as flawed and bureaucratic at points but
  never rise to a central-institution-level critique. The two axes that carry this entry's real
  weight: Redemption Difficulty (2) is earned by Cole Turner's arc — Phoebe's husband, possessed
  by and eventually merged with the Source of All Evil, whose love-driven struggle to resist
  total corruption spans multiple seasons and ultimately *fails*, ending in his vanquishing
  rather than a successful redemption, a real and costly exception to the show's otherwise
  reliable "love wins" pattern. Narrative Acceptance of Injustice (2) is earned by a specific,
  well-documented case: Prue Halliwell's death in the Season 3 finale ("All Hell Breaks Loose")
  is permanent — not undone despite that same episode's own time-reset plot device — and the
  show gives her no on-screen closure afterward (no funeral episode; Season 4 simply states she
  died), a gap critics and fans have specifically flagged (paste magazine's "It Still Stings:
  Justice for Prue"). Explicit Darkness (2) reflects the show's generally restrained, network-TV
  demon-of-the-week violence — real but not graphic in sustained detail, distinctly softer than
  Supernatural's practical-horror aesthetic (also Tier 6, added earlier this session).
- Cozy Fantasy = No. Hopepunk = No: love and sisterhood are the show's central themes, but the
  narrative isn't structured as an oppressed group's organized resistance to an institution (the
  Fierce shape) or built around mortality/time as an organizing meditation (the Bittersweet
  shape) — it's episodic good-vs-evil urban fantasy with genuine but conventionally-resolved
  stakes.
- Scored against the complete original 8-season, 178-episode series through its finale ("Forever
  Charmed"), which gives the surviving sisters (and Paige's replacement of Prue) a settled,
  hopeful ending.
- Neighbor check: none of the four other works tied at 4.65 share an identical per-axis profile.
  Avatar/Grimgar's Structural Despair 2 (an active genocide backstory; a stranded-in-a-death-game
  premise) sits above this entry's 1, trading against their Narrative Acceptance of Injustice 1
  vs. this entry's 2 (Prue's unaddressed death has no equivalent in either). Earthsea's Moral
  Cynicism 0 and Structural Corruption 2 differ from this entry's 1 and 1 in opposite directions
  — Earthsea's mythic story isn't institutional at all, closer to a personal quest, the opposite
  shape from Charmed's demonic-hierarchy backdrop. Final Fantasy XII's Structural Corruption 2
  and Redemption Difficulty 1 swap against this entry's 1 and 2 — Charmed's Cole arc is a more
  costly, failed redemption than anything in FFXII's political-intrigue plot. Checked further
  against a non-adjacent Tier 4 work, Once Upon a Time (4.20, added earlier this session, the
  closest tonal cousin as another found-family urban-fantasy TV drama): Once Upon a Time's Moral
  Cynicism 0 (True Love's Kiss as explicit magical law) sits below this entry's 1 (Cole's failed
  redemption is a real cynicism data point OUAT's cleaner magic system doesn't share), while
  this entry's Narrative Acceptance of Injustice 2 sits above OUAT's 1 (OUAT's finale resolves
  nearly everything; Prue's death never gets equivalent narrative closure) — a sensible,
  evidence-based ordering between the two closest peers on the scale. Label check: "Fantasy in
  Gray Tones (high stakes, real losses, but still high hope)" fits — a real, narratively
  unaddressed permanent loss and one failed redemption arc sit inside a fundamentally
  love-and-sisterhood-affirming show.
- Added to xlsx row 108, and to tier 4 on both index.html and es/index.html, inserted
  immediately after Grimgar per score order (exact tie); title "Charmed" in EN, "Embrujadas" in
  ES (the title used in both Spain and Latin American Spanish-language markets); creator
  credited as "Constance M. Burge" (the series creator, matching the site's convention of
  crediting the creator/showrunner for original TV properties rather than the studio); medium:
  "TV series" / "Serie de TV". Updated the Summary sheet's tier-4 count (19 → 20) and
  total-scored count (106 → 107 of 107). Updated the catalog-size mentions in both pages'
  meta/JSON-LD description tags (106 → 107).

### 32. Supernatural — Eric Kripke — TV series

- Tier 6 (Dark Fantasy), Final Score 6.90 (Weighted Internal Score 2.4) — the new tier-6
  ceiling, landing in a previously empty gap between Märchen Crown (6.7875) and The Stormlight
  Archive (7.575, Tier 7).
- Scores: Structural Despair 2, Limited Heroism 2, Moral Cynicism 3, Structural Corruption 3,
  Redemption Difficulty 2, Narrative Acceptance of Injustice 2, Explicit Darkness 3.
- Rationale: 15 seasons (2005-2020), the Winchester brothers hunting monsters after their
  mother's demonic murder. Structural Corruption reaches 3 on real multi-institutional grounds:
  both of the setting's ultimate cosmic institutions are shown as genuinely corrupt across the
  show's run — Heaven's angel bureaucracy (Zachariah's manipulations, Naomi's mind-control of
  Castiel, an actual angelic civil war) and Hell's demon hierarchy (Azazel's decades-long
  breeding-program scheme to engineer Sam as a vessel, the crossroad-deal economy) — with the
  season 11/15 revelation that God himself (Chuck) sits above both, confirmed to have been
  "maliciously manipulating every tragedy in [the brothers'] lives for his personal
  entertainment" as material for his own authored story. Moral Cynicism reaches 3 for the same
  reason, on a specific textual basis distinct from a merely "neutral" world: the setting's
  ultimate authority figure has an active, textually-confirmed preference for cruelty and
  suffering over kindness because it makes "better story" — closer to "the world punishes virtue
  and rewards brutality" than tier 6's more typical "morally neutral" default. Explicit Darkness
  lands at 3, not the ceiling: despite genuinely dark content (Dean's ~30 subjective years of
  Hell-torture, becoming a torturer himself under Alastair; recurring on-screen demonic
  possession/body-horror; graphic monster-of-the-week violence across 327 episodes), this is
  network television (The CW), and much of the show's darkest content — Dean's Hell torture
  specifically — is delivered through dialogue and brief flashback rather than sustained
  on-screen depiction, distinct from a premium-cable or manga format with no such constraint.
- Cozy Fantasy = No. Hopepunk = No: matches precedent (no work at Tier 6 or darker carries the
  tag) — found-family/brotherly love is genuinely central, but the show isn't structured as an
  oppressed group's organized resistance to a specific institution (the Fierce shape).
- Scored against the complete 15-season, 327-episode series through its actual finale: Chuck is
  stripped of his power (though left alive, not killed) and Jack — Jack, a redeemed nephilim who
  had earlier been treated as a dangerous liability — takes his place as a genuinely benevolent
  new god, reshaping Heaven "for the better." Dean dies on a routine hunt; Sam lives a full life;
  the brothers reunite in a peaceful Heaven. A real, structural fix, achieved only after 15
  seasons of an escalating "stop the immediate threat, a worse one is revealed behind it"
  pattern (the actual apocalypse, the Leviathans, the Darkness/Amara, the British Men of
  Letters, Chuck's endgame) — which is why Limited Heroism sits at 2 rather than 1 despite the
  finale's genuine resolution: the dominant felt pattern across the run is "resolves the
  immediate threat, deeper condition intact" until the very last season.
- Neighbor check: initially derived to an identical per-axis match with Claymore (also Tier 6,
  6.5625) — flagged immediately per the standing review practice and re-examined rather than
  accepted. On reflection, Moral Cynicism was under-scored at 2: Claymore's "morally neutral"
  world doesn't have anything equivalent to a textually-confirmed governing authority who
  actively prefers cruelty as better narrative material — a specific, evidence-based reason to
  revise to 3, which also differentiates the profile from Märchen Crown (also initially an exact
  match before this correction; Märchen Crown's Explicit Darkness 4 vs. this entry's 3 — a
  manga's page can depict extremity a basic-cable network drama can't — combined with the
  revised Moral Cynicism gap nets out to a small but real 0.1125-point difference rather than an
  exact tie). Checked further against a non-adjacent Tier 6 work, Re:Zero (6.1125): Re:Zero's
  Explicit Darkness 4 (Subaru's repeated on-screen violent deaths as a structural, central
  mechanic) sits above this entry's 3, while this entry's Structural Corruption 3 (multi-
  institutional: Heaven, Hell, and God himself) sits above Re:Zero's 2 (the Witch Cult as a
  severe but non-central faction) — a sensible, differently-shaped comparison. Label check:
  "Dark Fantasy... genuinely heavy without tipping into nihilism" fits — extreme cosmic-scale
  betrayal and real torture content sit inside a story that ultimately restores a benevolent
  order and gives its leads a peaceful ending, not a nihilistic one.
- Added to xlsx row 107, and to tier 6 on both index.html and es/index.html, appended as the new
  final entry in the tier (highest tier-6 score); title "Supernatural" in EN, "Sobrenatural" in
  ES (the title used across Latin American press and Warner Channel's regional broadcast);
  medium: "TV series" / "Serie de TV". Updated the Summary sheet's tier-6 count (15 → 16) and
  total-scored count (105 → 106 of 106). Updated the catalog-size mentions in both pages'
  meta/JSON-LD description tags (105 → 106).

### 31. The Sandman — Neil Gaiman — Comics, TV series

- Tier 6 (Dark Fantasy), Final Score 6.1125 (Weighted Internal Score 2.05) — an exact numeric
  tie with Re:Zero and Clevatess, via a genuinely different profile from each (see neighbor
  check below).
- Scores: Structural Despair 1, Limited Heroism 2, Moral Cynicism 2, Structural Corruption 1,
  Redemption Difficulty 3, Narrative Acceptance of Injustice 2, Explicit Darkness 4.
- Rationale: Neil Gaiman's 75-issue Vertigo comic (1989-1996) plus the Netflix adaptation
  (2022-2025, which carries the story through to the same ending). Redemption Difficulty is the
  clear swing criterion at 3, the highest value assigned to any tier-6 work so far: the entire
  series is organized around whether Dream, one of the seven cosmic Endless, can genuinely
  change, and the answer the text gives is that meaningful change costs him his own existence —
  he dies (in "The Kindly Ones") as the direct, textual consequence of killing his son Orpheus,
  itself an act of mercy that broke an ancient law of his own kind; Daniel, a transformed and
  gentler aspect, succeeds him. That's a categorically more expensive redemption arc than the
  typical tier-6 "real, costly, but survivable" bar this scale usually applies — matching the
  "rare, most who seek it fail or achieve it only partially" anchor used for A Song of Ice and
  Fire/The First Law rather than tier 6's usual RD2. Explicit Darkness sits at the ceiling (4)
  on well-documented grounds: issue #6 ("24 Hours") has Dr. Destiny psychologically torture,
  mutilate, and murder ordinary diner patrons over 24 hours — Gaiman has said the deliberate
  intent was "if I go this far — once — nobody will trust me," a mainstream-comics benchmark for
  extremity; the "Calliope" issue depicts a muse imprisoned and repeatedly raped by two authors
  across decades for creative inspiration; "The Doll's House" arc features a literal convention
  of serial killers. Limited Heroism and Moral Cynicism land at 2 rather than higher: most
  individual story arcs *do* resolve their immediate threat (24 Hours ends when Dream reclaims
  his tools; the Doll's House vortex crisis and Corinthian are both stopped), but the deeper
  condition — mortality, loss, historical atrocity as recurring texture across the many
  centuries-spanning vignettes — isn't fixed, and the anthology structure means some individual
  stories resolve kindly while others (Calliope's trauma, background historical suffering) are
  simply left as they are, not corrected. Structural Corruption stays low (1): Hell's own
  succession politics (Lucifer abandoning the throne, several claimants contesting the key) is
  real but mythological-personal in scale, not a real-world institutional critique the way
  Attack on Titan/A Song of Ice and Fire's central examples are. Structural Despair stays low
  (1) for a specific reason: the ending is explicitly cyclical rather than declining — Dream's
  death is immediately followed by Daniel's succession, continuity and renewal rather than
  civilizational decay.
- Cozy Fantasy = No. Hopepunk = No: not remotely a genre or narrative-shape fit for either tag.
- Scored against the complete 75-issue comic run and the complete Netflix adaptation (2 seasons
  plus the "Death: The High Cost of Living"-adjacent bonus epilogue), which carries the story
  through the same ending (Dream's death, Daniel's succession) rather than stopping short.
- Neighbor check: Re:Zero's Redemption Difficulty 2 (Rem's memory loss, Roswaal's centuries of
  scheming) sits below this entry's 3 — a specific, evidence-based gap given Dream's redemption
  costs him his literal existence, not just years of struggle — while Re:Zero's Structural
  Corruption 2 (the Witch Cult as a severe if non-central corrupting faction) sits above this
  entry's 1, and Re:Zero's Structural Despair 2 sits above this entry's 1 (demi-human oppression
  as an ongoing world condition vs. this entry's cyclical-renewal ending) — three genuine,
  independently-reasoned differences that happen to net to the same total, not a copy. Clevatess
  differs similarly: its Redemption Difficulty 1 (Clevatess's found-family arc with the human
  infant is comparatively gentler and more successful) sits well below this entry's 3, while its
  Structural Despair 2 and Structural Corruption 2 both sit above this entry's 1 and 1
  respectively. Checked further against a non-adjacent Tier 6 work, Pan's Labyrinth (6.45): both
  share Explicit Darkness 4 and a fascist/authoritarian-adjacent institutional backdrop, but
  Pan's Labyrinth's Narrative Acceptance of Injustice 3 (Falangist Spain's violence is never
  narratively corrected) sits above this entry's 2, and its Redemption Difficulty 0 (not
  designed as a redemption story at all) sits well below this entry's 3 — a sensible ordering
  given how differently the two works are actually structured. Label check: "Dark Fantasy
  ... genuinely heavy without tipping into nihilism" fits — extreme, well-documented content sits
  inside a work whose defining thesis is that change and mortality, while costly, are meaningful
  rather than purely bleak.
- Added to xlsx row 106, and to tier 6 on both index.html and es/index.html, inserted
  immediately after Clevatess per score order (exact tie); title "The Sandman" kept identical in
  EN and ES (no distinct official Spanish title found for either the comic or the Netflix
  series — DC/Vertigo and Netflix both market it under the English title in Spanish-language
  markets, matching the site's existing convention for The Witcher/The Legend of Zelda); medium:
  "Comics, TV series" / "Cómics, Serie de TV". Updated the Summary sheet's tier-6 count (14 → 15)
  and total-scored count (104 → 105 of 105). Updated the catalog-size mentions in both pages'
  meta/JSON-LD description tags (104 → 105).

### 26. Dirk Gently's Holistic Detective Agency — Douglas Adams — Novels, TV series

- Tier 4 (Fantasy in Gray Tones), Final Score 4.5375 (Weighted Internal Score 1.35) — an exact
  numeric tie with Harry Potter and the Prisoner of Azkaban, via a genuinely different profile
  (see neighbor check below).
- Scores: Structural Despair 1, Limited Heroism 1, Moral Cynicism 1, Structural Corruption 2,
  Redemption Difficulty 1, Narrative Acceptance of Injustice 1, Explicit Darkness 3.
- Rationale: this queue item explicitly named both media, and the two exist in real tension
  worth documenting rather than picking one and ignoring the rest. Douglas Adams' two novels
  (Dirk Gently's Holistic Detective Agency, 1987; The Long Dark Tea-Time of the Soul, 1988) and
  the 2010 BBC series (Stephen Mangan, 4 episodes) share one register: whimsical,
  interconnected-mystery absurdist comedy in Adams' voice — real deaths occur (Gordon Way's
  murder, an airport check-in desk exploding, a severed head) but they're processed through
  comic tone, not horror, and the fading, senile Norse gods of Tea-Time read as melancholy
  rather than despairing. The 2016-2017 BBC America series (creator Max Landis), by contrast,
  is a substantial tonal departure — critics described it as combining "the violence of The
  Walking Dead with the oddball stories of Twin Peaks" and noted it "violates the spirit of its
  source material"; it adds Project Blackwing, a real government institution built to hunt,
  capture, and experiment on people with paranormal abilities (Dirk himself is a former
  captive), an on-screen assassin character (Bart), and reviewer-documented "gore and a lot of
  blood." Rather than silently scoring only the gentler version, Explicit Darkness (3) and
  Structural Corruption (2) are set by this darkest confirmed adaptation, consistent with how
  Explicit Darkness is defined ("the visibility and intensity of violence... as depicted," per
  CRITERIA_THEORY.md) — the violent content is real and mainstream, not a discarded rough cut. The other axes stay low because the *comedic, ultimately-triumphant* throughline holds
  across every version, including the 2016 show: both novels end with their central mysteries
  fully resolved, and reviewers confirm the 2016 series' Season 2 finale (which became the de
  facto series finale on cancellation) gives the core cast "a happy ending... everyone living
  happily ever after," landing Limited Heroism, Moral Cynicism, and Narrative Acceptance of
  Injustice all at 1 rather than higher. The finale did introduce one new, unexplored mystery
  hook before cancellation — a forward-looking dangling thread, not a lingering unresolved
  injustice, so treated differently from The Shannara Chronicles' Crimson thread (Narrative
  Acceptance of Injustice 1, not 2).
- Cozy Fantasy = No. Hopepunk = No: Blackwing is real institutional harm, but the franchise's
  organizing shape across every version is absurdist mystery-comedy built on "the
  interconnectedness of all things," not an oppressed group's organized resistance to that
  specific institution.
- Scored against both novels and both TV adaptations (2010 BBC, 2016-2017 BBC America) as one
  entry rather than splitting, since — unlike the Final Fantasy/Baldur's Gate splits earlier in
  this catalog — there's no clean per-installment darkness escalation to split along; the
  franchise's two TV adaptations are simply different creative takes on largely the same
  underlying premise, not sequential chapters of one growing story.
- Neighbor check: Harry Potter and the Prisoner of Azkaban's Narrative Acceptance of Injustice 2
  (Sirius's wrongful imprisonment stays only partially resolved within this book) trades against
  this entry's Redemption Difficulty 1 (no confirmed deep redemption arc across any version) vs.
  Azkaban's Redemption Difficulty 0 — a clean, textually-grounded swap, not an identical match.
  Checked against a non-adjacent Tier 4 work, The Shannara Chronicles (4.875, added earlier this
  session): Shannara scores higher specifically via Narrative Acceptance of Injustice (2 vs. 1
  — its Crimson-persecution thread stays genuinely open due to cancellation, while this entry's
  unresolved thread is a fresh hook rather than a lingering injustice) despite an identical
  Structural Corruption (2, both driven by a real institution built to hunt/harm a class of
  people — Blackwing and the Crimson respectively). Label check: "Fantasy in Gray Tones (high
  stakes, real losses, but still high hope)" fits — real on-screen violence and one dark
  government-conspiracy backstory sit inside a fundamentally comic, ultimately-triumphant
  franchise.
- Added to xlsx row 105, and to tier 4 on both index.html and es/index.html, inserted
  immediately after Harry Potter and the Prisoner of Azkaban per score order (exact tie); title
  "Dirk Gently's Holistic Detective Agency" in EN, "Dirk Gently: Agencia de investigaciones
  holísticas" in ES (the official Anagrama translation title for the first novel, used since the
  TV adaptations kept the English title even in Latin American streaming); medium: "Novels, TV
  series" / "Novelas, Serie de TV". Updated the Summary sheet's tier-4 count (18 → 19) and
  total-scored count (103 → 104 of 104). Updated the catalog-size mentions in both pages'
  meta/JSON-LD description tags (103 → 104).

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
