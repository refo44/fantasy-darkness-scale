# Criteria Theory

Theoretical grounding for the 7 criteria used in the Fantasy Darkness Scale (v2 methodology).
This is distinct from the operational 0-4 scoring anchors in the Methodology sheet: those
tell you *how to score* a criterion; this explains *what each criterion is actually a
construct of*, and why they don't fully overlap despite being highly correlated in practice.

Useful when a work's darkness doesn't fit neatly into the literal anchor text — asking "which
theoretical pole is this closer to" is often clearer than re-reading the anchor wording.

## The seven constructs

### Structural Despair
**Construct: the cosmological trajectory of the fictional world.** Not "does something bad
happen," but: left to its own logic, does this world's *system* trend toward improvement or
decline? It's a property of the setting itself, independent of any character's choices — the
baseline direction the world would move in if no one intervened.

- **Low (0): Progress** — **High (4): Decay**

### Limited Heroism
**Construct: the efficacy of individual agency against structural forces.** This is the
classic agency-vs-structure tension in narrative theory. Does one person's action meaningfully
reshape the world-system, or does the system absorb/nullify individual effort, leaving only
local and temporary effects? It measures how much a story believes in the causal power of a
protagonist.

- **Low (0): Agency** — **High (4): Futility**

### Moral Cynicism
**Construct: the moral physics of the fictional universe.** Does the story's internal logic
operate on "just world" causality (virtue produces good outcomes) or "cynical world"
causality (outcomes are set by power/ruthlessness, and moral behavior is irrelevant or
actively punished)? This is about the *reward structure* built into how the fiction works,
not about any single event.

- **Low (0): Justice** — **High (4): Cynicism**

### Structural Corruption
**Construct: institutional integrity vs. institutional design.** Distinct from Moral Cynicism
(which is about individual-level cause and effect) — this asks whether *institutions
themselves* (governments, faiths, economies) are functioning as designed to perpetuate
injustice, versus being basically legitimate systems with occasional bad actors. It's about
the system's blueprint, not any one person's virtue or vice.

- **Low (0): Legitimacy** — **High (4): Corruption**

### Redemption Difficulty
**Construct: the accessibility of moral repair.** Can a character who has done wrong achieve
genuine moral recovery, and at what price? This measures the story's stance on whether moral
failure is *reversible*, and how expensive reversal is — in sacrifice, suffering, or things
that can't be undone.

- **Low (0): Grace** — **High (4): Damnation**

### Narrative Acceptance of Injustice
**Construct: the story's own resolution posture toward injustice.** Distinct from whether
injustice *exists* in the world (other criteria cover that) — this is about whether the
*narrative itself* treats a given injustice as something the plot will resolve, versus
something the story presents as permanent and doesn't even attempt to fix. It's about
narrative closure applied specifically to injustice.

- **Low (0): Resolution** — **High (4): Permanence**

### Explicit Darkness
**Construct: surface-level presentation, not theme.** The only criterion that isn't about the
fictional world's underlying logic — it measures the visibility and intensity of violence,
horror, and disturbing content *as depicted*, independent of what it means thematically. This
is exactly why it can diverge from the other six (see Nightmare Before Christmas and Final
Fantasy III & V in `ADDITIONS_LOG.md`'s v2 rescoring backlog): a world can be thematically
light while still showing something visceral on the page, or vice versa. It's why it carries a
slightly lower weight (0.10 vs 0.15) — it's tracking sensory intensity, not worldview.

- **Low (0): Restraint** — **High (4): Horror**

## Why six criteria correlate and one doesn't

Structural Despair, Limited Heroism, Moral Cynicism, Structural Corruption, Redemption
Difficulty, and Narrative Acceptance of Injustice all cluster around **the world's internal
logic** — its cosmology, its treatment of agency, its moral causality, its institutions, its
capacity for repair, its posture toward resolution. That's the theoretical reason those six
correlate so highly in the v1 data (r > 0.96 between every pair, measured across all 87
works).

Explicit Darkness measures something categorically different: **what's shown, not what's
meant.** A story can be thematically wholesome yet visually macabre (Nightmare Before
Christmas), or thematically grim with almost nothing shown explicitly. That's why it needs
independent scoring attention during rescoring rather than assuming it will track the other
six — and why, when a work's tier comes out wrong on a first pass, Explicit Darkness is the
first place to re-check (see FF III & V for a concrete example of exactly this correction).

## Quick reference table

| Criterion | Construct | Low (0) | High (4) |
|---|---|---|---|
| Structural Despair | World's cosmological trajectory | Progress | Decay |
| Limited Heroism | Individual agency vs. structural force | Agency | Futility |
| Moral Cynicism | Moral physics / causality | Justice | Cynicism |
| Structural Corruption | Institutional design | Legitimacy | Corruption |
| Redemption Difficulty | Accessibility of moral repair | Grace | Damnation |
| Narrative Acceptance of Injustice | Story's resolution posture | Resolution | Permanence |
| Explicit Darkness | Surface presentation | Restraint | Horror |

## Cozy Fantasy and Hopepunk: theoretical relationship to the seven constructs

Two additional descriptive tags run alongside the seven scored criteria (see `ADDITIONS_LOG.md`
for the full tagging rules and `TIER_GUIDE.md` for tier-by-tier examples). Both are excluded
from the score formula on purpose — genre *stance* toward darkness isn't the same axis as
*amount* of darkness (Avatar: The Last Airbender is tagged Hopepunk while depicting genocide).
But neither tag is arbitrary: each variant maps onto a specific, describable position across the
constructs above.

### Cozy Fantasy: genre membership, not mood

**Not a construct on the same axis as the seven criteria** — this tag tracks book-publishing
genre membership (comfort-focused, low-stakes, community/found-family as the text's actual
organizing project), not a score profile. A work can feel cozy in tone without qualifying (My
Neighbor Totoro doesn't get this tag, even though it's Gentle in Hopepunk terms).

Where it does connect to the constructs: genuine Cozy Fantasy requires **Structural Corruption**
and **Structural Despair** to stay very low — the genre's whole premise depends on the world not
actively working against its characters' comfort. Two variants, distinguished by how much real
friction that comfort has to survive:

- **Wholesome Cozy Fantasy** — the comfort is *unthreatened*: Structural Corruption and
  Structural Despair sit at 0, nothing presses against the found-family core at all.
  *Example: Legends & Lattes (Tier 1) — the scale's only confirmed Cozy Fantasy work.*
- **Resilient Cozy Fantasy** — the comfort *survives real friction*: Structural Corruption
  begins registering (1) — some genuine flaw or threat exists, and the community/found-family
  core has to hold up against it rather than existing in a vacuum. What distinguishes this from
  Fierce Hopepunk below is that the friction stays background-level, not the text's central
  conflict. *No confirmed example currently sits in this tier — a real gap, noted honestly in
  `TIER_GUIDE.md` rather than papered over.*

### Hopepunk: three variants sharing one thesis, differing on which construct they answer

**Shared thesis across all three:** kindness/hope is depicted as a *deliberate, load-bearing
choice*, not naivety — this is what separates Hopepunk from simply "a work with a happy
ending." The three variants differ in *which* construct's high pole they're responding to:

- **Gentle Hopepunk** — responds to nothing; no real adversity is required at all. Structural
  Despair and Structural Corruption both sit at 0 — kindness/community is simply the world's
  default operating state, not a stance taken against anything.
  *Examples: My Neighbor Totoro, Kiki's Delivery Service, Ponyo — all Tier 1.*
- **Fierce Hopepunk** — responds directly to **Structural Corruption**. Real institutional
  injustice exists (an oppressive system, empire, or institution), but the story keeps
  **Limited Heroism** and **Moral Cynicism** low anyway: resistance is genuinely effective
  (Agency, not Futility) and kindness is the causally *correct* strategy, not a naive one
  (Justice, not Cynicism). This is the variant that scales hardest across tiers — the same
  shape gets genuinely costlier as Structural Corruption climbs.
  *Examples: The House in the Cerulean Sea (Tier 2, lightest form) → Avatar: The Last Airbender
  (Tier 4) → The Legend of Korra (Tier 5, heaviest form) — the same shape, escalating cost.*
- **Bittersweet Hopepunk** — responds directly to **Structural Despair** in its existential
  register: real, permanent loss (mortality, time) that isn't a corrupt institution waiting to
  be reformed — nothing *resolves* it. The distinguishing move is keeping **Moral Cynicism** low
  anyway: choosing connection despite guaranteed future grief is treated as worthwhile, not
  foolish. This variant is also the one most likely to coexist with a real, non-zero
  **Narrative Acceptance of Injustice** on the specific loss in question — the loss itself
  doesn't get undone; the story's stance toward it does.
  *Defining example: Frieren: Beyond Journey's End (Tier 3). Also Mushishi (Tier 3) — arguably
  the purest fit on the whole scale, since its entire episodic structure is organized around
  "loss is real and often permanent, and connection persists anyway."*

**Why the tag disappears past Tier 5:** not because found-family warmth stops existing in
darker works (Re:Zero and Clevatess, both Tier 6, have real found-family cores), but because at
that severity the surrounding content dominates enough page-time that "kindness as the
organizing response to adversity" stops being the most honest one-line description of what the
work is actually about.
