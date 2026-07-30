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

## Queue

1. [x] El Principito (The Little Prince) — Antoine de Saint-Exupéry — Book — DONE, see Completed
2. [x] Adventure Time — DONE, see Completed
3. [x] Star vs. las fuerzas del mal (Star vs. the Forces of Evil) — DONE, see Completed
4. [x] Clevatess (Majū no Ō to Akago to Shikabane no Yūsha) — Yūji Iwahara — Manga — DONE, see Completed
5. [x] Saga de Tanya the Evil (The Saga of Tanya the Evil) — DONE, see Completed
6. [x] Re:Zero − Starting Life in Another World — DONE, see Completed
7. [x] Legend (1985 film, dir. Ridley Scott, Tom Cruise — a dark lord hunting the last unicorns) — DONE, see Completed
8. [ ] La historia sin fin (The NeverEnding Story)
9. [ ] Shin Sekai Yori (From the New World)
10. [ ] Mushishi
11. [ ] Record of Lodoss War
12. [ ] The Legend of Vox Machina
13. [ ] The Nightmare Before Christmas
14. [ ] Willow (1988)
15. [ ] Labyrinth (1986 film, dir. Jim Henson, David Bowie — a goblin king, a labyrinth, a stolen baby brother)

## Completed

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
