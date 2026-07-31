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
8. [x] La historia sin fin (The NeverEnding Story) — DONE, see Completed
9. [x] Shin Sekai Yori (From the New World) — DONE, see Completed
10. [x] Mushishi — DONE, see Completed
11. [x] Record of Lodoss War — DONE, see Completed
12. [x] The Legend of Vox Machina — DONE, see Completed
13. [ ] The Nightmare Before Christmas
14. [ ] Willow (1988)
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

## Completed

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
