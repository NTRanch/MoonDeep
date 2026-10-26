# Conditioning Tracks — Design Expansion for MoonDeep

**Status:** Design proposal by the studio, 2026-10-26, written to the studio's direction
of the same day: the game gets a different name, and the hypnosis design gains
erotic, kink-specific **long-term conditioning tracks** — what she repeatedly
does to herself in subspace, and what others do to her, permanently reshapes
what she craves, how her body presents, and which endings she can reach.
Extends the design-basis notes (Battle-Lust) and docs/design-hypnosis.md (Depth) without
contradicting either. All values are ours to tune; all characters are adults.
Behavior/concept level only — no source-game assets, text, art, or code.

**Studio narrative rule (binding, from the NTRanch progression model):**
conditioning never installs a foreign desire. Each track surfaces a desire
the heroine already has hidden, or dissolves the block keeping her from it.
Her internal voice renders this: early on she is aroused and enjoying herself
but embarrassed and hesitant inwardly, and that hesitation is what shows
outwardly; as conditioning deepens she becomes more eager and outwardly
embracing — because the wanting was always hers. Every track spec below
names, per heroine, *which hidden desire it taps or which block it dissolves*.
That line is not flavor; it is the consent-legibility device the whole
progression runs on.

---

## 1. The rename

The game no longer carries the source game's name. The internal
reference notes keep the source game's name, *Jessika's Curse* —
that is the reference work. Ours is ours.

Candidates, with a search-index collision check (2026-10-26; indicative only,
not a trademark clearance):

| Candidate | Collision check | Verdict |
|---|---|---|
| *The Deepening* | Taken — a Steam game/book series already uses it (*The Deepening: Eco-Offensive*) | Reject as a bare title |
| *Trancebound* | Minor uses only (a remix project, an AI roleplay listing); no game of note | Viable |
| *The Moonwell Deepening* | No game surfaced under this name | Rejected by the studio, 2026-10-26; title ruled **MoonDeep** |
| *Succumb* | Very generic; drowns in search | Reject |
| *Pendulum* | Generic; many products | Reject as a bare title |

**RULED (the studio, 2026-10-26): *MoonDeep*.** The studio rejected *The
Moonwell Deepening* and, after a second pass over English and Japanese
candidates, ruled **MoonDeep** (studio's styling) — the moonwell as a
place she sinks into, one word, no collision surfaced. The doc uses
**MoonDeep** as the title from here; "moonwell" survives only as the
in-world name of an induction site.

**Heroine rename — RULED (the studio, 2026-10-26).** The lead is **Odette**,
a proud knight — and her cursed alter ego is **Odile** (single-l,
the ballet spelling — an initial double-l
"Odille" was corrected to this, 2026-10-26). The white-swan/black-swan pairing is public-domain
ballet, and it maps the design exactly: Odette commands, Odile
craves, and the game is the negotiation between them. The three earlier
design forks translate unchanged (Jessy → Odile throughout:
Odile-initiated choices remain vetoable at a lust cost). Celeste /
Noctis was the studio's other liked pair and is recorded as the
runner-up; it was not adopted (Noctis carries a strong Final Fantasy
XV association).

---

## 2. The model: three clocks, one amplifier

| Axis | Clock | Raised by | Relieved by |
|---|---|---|---|
| **Lust** (Battle-Lust, the design basis §3) | Per expedition, 0–100, never decays in the field | Enemy lust-channel attacks | Town services only |
| **Depth** (the hypnosis design §2) | Campaign, ratchet, tiers 1–5 | Deliberate trance sessions at induction sites; harvested imprints | One quest, once, one tier (the Unraveling) |
| **Conditioning** (new, per track) | Campaign, per-track 0–100, tiered 0–5 | Repeated acts on that track — hers, a partner's, an enemy's | Per-track cleansing (town service, priced, partial) |
| **Craving** (new, per track) | Days-scale pressure | An installed track going unmet | Satisfying the track (session, service, or event) |
| **Temptation** (new, denial only) | Campaign while the vow holds | Lust attacks, unmet cravings, trance exposure, time | The vow breaking — or being kept to a milestone (§5) |

**Depth is the amplifier.** Conditioning gain from any source is multiplied
by `(1 + 0.25 × Depth tier)`: hypnosis doesn't choose what she becomes, it
makes whatever she *does* stick faster. Depth also gates *self-induction*:
at Depth 2+ she can enter subspace at camp or in town without a site or an
operator — which is what makes self-conditioning a full playstyle rather
than a tutorial verb.

**Subspace is the room where tracks grow.** Entering subspace — at an
induction site, via the combat Trance stance, or by self-induction — puts
her in the state where conditioning registers:

- Resistance drops: conditioning gain ×1.5 while in subspace, from any
  source, hers included.
- Self-play actions unlock (§3 tracks): the focused, repeated acts that
  build each track. Outside subspace the same acts are unavailable or
  cosmetic — the trance is what makes them *training*.
- Time passes in intervals. An enemy interruption in the field is a real
  risk: she starts any fight entered from subspace at elevated Lust.
- Odile is present. In subspace the internal voice is Odile's, which is how
  the player *hears* the studio rule: early sessions are embarrassment and
  negotiation; deep sessions are Odile asking, then Odette agreeing.

**Three sources, three prices.** Every track grows from the same act
performed three ways, and the differences are the game's social geometry:

| Source | Gain/interval | Cost | Residue |
|---|---|---|---|
| **Self** (she does it, player directs) | 4 | Time; raises her own craving honestly | None — clean progress, her choice throughout |
| **Partner / operator** (an NPC conditions her: the mesmerist, a dairy hand, a dominant householder, a lover) | 7 | Gold or favors; requires the relationship | Their *imprint*: +Depth tuition per the hypnosis design, and her craving arrives flavored to *them* until cleansed |
| **Enemy imprint** (suffered in combat: overpowering grapples, mesmerist attacks, track-specific lust moves) | 10 if the fight is won while she spent turns tranced/exposed | The fight itself; she doesn't choose the flavor | Their trigger variant until cleansed at church-tier prices (as the hypnosis design §2) |

Self-conditioning is the slowest and the only residue-free route — the
build for a player who wants her to *choose* this. Partner routes are the
economy route. Enemy imprinting is the roguelike route: the dungeon itself
trains her, and winning decides whether it was tuition or damage.

---

## 3. Sessions and the benefit engine

A **session** is one subspace visit spent on one track focus, measured in
**intervals** (abstract units; ~a scene beat each). The player picks the
track and the length up front, and can extend at the door of each interval
with the craving cost of stopping *shown* — the game's core temptation UI.

**Conditioning per interval:** base gain by source (table above) ×
subspace multiplier × Depth multiplier. Crossing 20/40/60/80/100 raises the
track tier 1–5. Tier effects per track are specified in §4.

**Benefit rolls (the studio's mechanic):** every interval rolls on the
track's benefit table. The longer she goes, the better it pays *and* the
deeper it sets — one dial, two directions:

- **Gold.** Each track has an in-world income flavor (§4): milk sold,
  service wages, gifts and tribute, performance fees. Roll 55%: gold =
  track base × (1 + tier), jittered by the run's seeded RNG.
- **Stat glimpse.** Roll 12% + 1% per interval already spent in this
  session: a temporary +1 to the track's paired stat until next rest.
  At a tier crossing, one pending glimpse becomes **permanent** — this is
  how long sessions convert to character growth, and it is deliberately
  the same roll, so the player feels the gamble become a guarantee at
  exactly the moment the conditioning sets.
- **Skill spark.** Roll 5% + 1% per interval beyond the third: she learns
  one skill from the track's skill list (seeded draw, no duplicates;
  when the list empties, sparks convert to a permanent stat +1). Skills
  are real loadout skills under the design basis's limited-equip rule, so a
  conditioned body is a *build*, not just a state.

Determinism note: all rolls draw from the run's seeded RNG stream at a
defined tick point, exactly as the design basis's disobedience roll — sessions
are replayable and testable, never wall-clock random.

**Craving, the maintenance economy.** At tier 1+ a track installs a craving
with a period: `days = max(1, 6 − tier)`. While unmet, craving does three
things, in escalating order: her internal-voice lines for that track start
appearing in town; her Lust gain multiplier in combat rises +10% per unmet
track; and at double-period overdue, that track's acts enter her
**disobedience table** — in Battle-Lust's upper band, a replaced command
can now be *the craving's act* (she milks herself mid-fight, kneels,
presents — per track, §4). Craving is never a stat tax; per the design basis's
founding choice, the cost is agency. Satisfying a craving (a session, a
partner visit, a town service) resets the period and pays the session's
benefit rolls as normal — the loop is generous on purpose: this is a game
about a girl whose needs have become her economy.

**Body and presentation changes.** Each track carries presentation stages
tied to tiers — sprite/portrait state variants, outfit unlocks, expression
sets. Art-budget discipline: stages are capped at **3 visual steps per
track** (early / set / deep), however many mechanical tiers exist, so the
matrix stays shippable.


---

## 4. The tracks

Each spec: the act, what it installs, tier effects, benefits, the craving's
disobedience act, presentation stages, and the town/NPC surface. Extension
tracks (§4.5) prove the frame is general: any kink that fits *act → craving
→ economy* can be added without new systems.

### 4.1 The Dairy Track — breasts → the hucow (studio-specified)

- **Acts.** In subspace she plays with her breasts — kneading, suckling
  play, pumping toys from the conditioning-lab prop family; partners milk
  or handle her; a milking-machine fixture is the lab's version. Enemy
  source: breast-focused lust attacks and grapples.
- **What it installs.** Sensitivity first, then growth, then production:
  her breasts **enlarge one presentation stage per two tiers** (3 stages),
  she becomes able to **lactate** (tier 2), then to let down **on command
  or trigger** (tier 4). The craving is to *be milked* — fullness is a
  felt state, not a meter abstraction: internal voice, then visible
  discomfort cues, then the disobedience act.
- **Fullness sub-meter.** Once lactating, fullness refills over time and
  after arousal; milking empties it. Overfull = Lust gain +, distraction
  lines; milked recently = the Afterglow buff (party morale, §4.3 shares
  the buff machinery). Milk is an inventory good: sold raw, or crafted
  ("moonmilk" potions — a lust-relief consumable that is *not* a town
  service, the track literally produces its own sink; using her own
  product to manage Battle-Lust is the track's signature loop).
- **Benefits.** Gold: milk sales at the dairy barn, price scales with tier
  and stage (she becomes a *prize* producer). Paired stat: VIT (body) /
  CHA (pride in it). Skills: **Letdown** (distraction / ingredient burst),
  **Gentle Hands** (milk another — party support: clears one ally's
  craving), **Barn Rights** (passive daily milk income without a session).
- **Disobedience act.** Kneading herself; at deep tiers, hiking her top
  and offering — to the nearest hands, ally or enemy.
- **Town surface.** The dairy barn (new operator: the Dairykeeper — buyer,
  milking service, partner-conditioning source), fitted bras/cup-size shop
  beats that mark the growth stages in dialogue, a milking-parlor service
  that satisfies the craving without a self-session.
- **Ending flags.** *The Prized Cow* (she is kept, cherished, and owned by
  the barn) vs *The Dairykeeper's Partner* (agency flip: the barn is hers;
  she keeps books nobody expected a hucow to keep).

### 4.2 The Service Track — ass → overpowered → the TPE domestic slave (studio-specified)

- **Acts.** In subspace she plays with her ass — plugs, training, presenting
  practice; partners spank, plug, and overpower her in training bouts;
  enemy source: grapples she loses, pin/overpower lust finishers, bandit
  and boss "claimed" cinematics survived.
- **What it installs.** A paired craving: **to be overpowered** (the body's
  want) that matures into **to be kept** (the life want): taken in hand by
  someone stronger, put in a collar, given a household and orders in it.
  TPE arrives by degrees — first she craves the moment of being pinned;
  by tier 3 she craves *instructions*; by tier 5 she craves the whole
  arrangement, total power exchange as domestic peace.
- **The Yield stance (combat verb).** From tier 2: instead of resisting a
  grapple she can **Yield** — damage converts to Lust + imprint gain, and
  a yielded fight she still wins pays out like a partner session. Yielding
  is surrender as a tactic, kin to the Trance stance: the game keeps
  making "letting it happen" a decision with a price and a payout.
- **Domestic economy.** Service is the steadiest gold in the game: inn
  shifts, housekeeping for the manor, serving at the tavern — wages +
  tips, paid per session-equivalent, available whenever she presents
  herself for work at tier 1+. It's deliberately *reliable where the other
  tracks are gambly*: the slave build is the game's econ backbone.
- **Benefits.** Gold: wages (above). Paired stat: DEX (grace under orders)
  / STR (being handled made her strong). Skills: **Household** (cooking
  buffs for the party; equipment upkeep discount), **Perfect Service**
  (party buff when she follows the leader's issued commands three turns
  running), **Present** (taunt-by-offering: draws enemy attention to her,
  on her terms).
- **Disobedience act.** Kneeling. At deep tiers: presenting — bent,
  offered, waiting to be taken or told.
- **Presentation.** Posture softens (sprite idle changes), collar item
  tiers (ribbon → leather → named collar), uniform outfits (maid first —
  the game's iconic look for this track), a kneeling idle in town.
- **Town surface.** The manor householder (partner-conditioning source and
  the TPE relationship's face), the innkeeper (employer), a collarwright.
- **Ending flags.** *Kept* (TPE domestic slave to the householder, ending
  text frames it as the peace she chose piece by piece) vs *Head of
  Household* (agency flip: the house runs on her discipline; the
  householder takes orders about everything except her).

### 4.3 The Doll Track — pussy → the brainless fucktoy (studio-specified)

- **Acts.** In subspace she plays with her pussy — fingers, toys, edging
  games Odile sets her; partners use her in training (positional coaching,
  orgasm control); enemy source: direct stimulation lust attacks, toys
  planted by trapper enemies, a "demo doll" exhibition bout.
- **What it installs.** The craving to **be used**, and a mind whose
  priorities *shift* rather than empty — per the studio's standing ruling on
  this endpoint in the studio's other work: not quiet, not blank. Her
  thoughts fill with service, arousal, training, and pride in being good
  at it; deciding and knowing are surrendered, and her internal voice
  stays present and busy to the end. "Brainless" in this design means the
  *burden of choosing* is what she craves losing — which is why the
  mechanic expresses it through the game's agency systems, not INT stats.
- **Orgasm conditioning.** The track's mechanical heart: orgasms on
  command (tier 3), the refractory period trained away (tier 4 — she can
  be brought off and be ready again at once), and at tier 5 **Cum-Drunk**:
  after an orgasm she gains a powerful Afterglow state (speed +, party
  morale) instead of the spent state that ends other girls' fights.
- **Dialogue narrowing (the visible mind).** At tiers 3+, her dialogue
  options *reorder*: flirt / offer / please options surface first, proud-
  knight options sink — never removed, and Odile-first choices can be
  overridden by the player at a Lust cost (the hypnosis design's veto,
  applied at the sentence level). The player feels the track in every
  conversation, not just in scenes.
- **Benefits.** Gold: gifts and tribute from admirers (unreliable, large —
  the mirror of Service's steady wages). Paired stat: CHA / LUK. Skills:
  **On Command**, **Again** (ignore one Succumb per expedition — readiness
  trained into her), **Read a Partner** (seduction recon: learn an NPC's
  hidden desire or an enemy's track weakness).
- **Disobedience act.** Rubbing against the nearest anything; at deep
  tiers, begging — the only disobedience act that can target an *enemy's*
  morale instead of wasting her turn, if her CHA carries it.
- **Presentation.** Expression sets (glazed, heart-eyed, tongue-out bliss
  states from the studio's ruled ahegao bar), a permanently softer
  portrait at deep tiers, toy-belt outfit line.
- **Town surface.** The courtesan-trainer at the bathhouse (partner
  source), admirers' gift events, a toy shop that is also an intel broker.
- **Ending flags.** *The Prized Toy* (a consort kept for use, adored for
  it) vs *The Trainer* (agency flip: she teaches the bathhouse's girls —
  the doll runs the dollhouse).

### 4.4 Track interactions

- **Dominance.** Her highest track is her *dominant* track: it owns the
  majority share of her disobedience table, her deep-tier dialogue
  reordering, and her ending priority. Tracks don't lock each other out;
  they *compete for her*, and the competition is the build.
- **Composite ending.** If three or more tracks reach tier 4+, the
  *Fully Hers* ending unlocks: no single keeper or role — a girl
  conditioned on every axis who knows exactly what she is and negotiates
  her life from inside it. It is the hardest ending to reach by session
  economics (time is finite per campaign) and is treated as the tracks
  system's secret best ending, without framing the single-track endings
  as lesser lives.
- **Triggers can be track-shaped.** A Depth tier's named trigger (§2 of
  the hypnosis design) can be bound to a track: the word doesn't just check
  her trance, it fires that track's craving at full pressure. Enemies who
  learn a *bound* trigger own a remote control for a specific appetite —
  and allies who know it own the antidote (satisfy or soothe her before
  the disobedience table does it for them).

### 4.5 Extension template (future tracks)

Any kink that fits the frame slots in with no new systems: **act** (the
subspace practice), **install** (the craving + its object), **economy**
(its gold flavor and reliability profile), **agency expression** (its
disobedience act and dialogue effect), **presentation** (3 stages max),
**agency-flip ending**. Named candidates on the shelf, one line each:
*Oral* (gag reflex trained away, in shown progression → service-blowjob
mastery economy); *Bondage* (the rope-bunny inversion: escape-artist and
contortion skills — the track that pays in *freedom*); *Exhibition* (being
seen → performance fees, reputation system hook); *Feet* (worship given
and received → court-intrigue recon skills). Each waits for its own
per-heroine hidden-desire line before it ships for that character.

---

## 5. The Untouched Path — abstinence as hard mode (studio-specified)

The counter-design: a **vow** she can swear at the church (tier-priced like
everything in that building — the town sells both directions of her mind,
and this is the third direction: neither).

**The vow.** She will not pleasure herself. Self-play actions lock. The
vow is *specifically* about her own hands (fork, §7): partner and enemy
conditioning still exist in the world, and every point of it feeds
Temptation at double rate — a pure run declines the world too, which is
what makes it hard mode rather than a checkbox.

**The small running benefit (deliberately small).** Per expedition day the
vow holds: **Resolve** +1 stack (cap 10): +2% XP and +1% crit per stack,
a Depth-session discount, and one Resolve can be *spent* to auto-pass a
disobedience roll. On paper this is worse than any track's session
economy. It is meant to be. The vow is not an income strategy; it's a
siege she wins by still being standing at the end.

**Temptation — the pressure the player feels.** Temptation (0–100) is the
hero feeling it, rendered so the player manages a person, not a meter:

- Gains: every lust attack landed (+2), every unmet craving tick from any
  installed track (+3/day — tracks installed *before* the vow become its
  difficulty setting), every subspace entry for Depth purposes (+5),
  every Odile-first dialogue the player vetoes (+1 — *saying no costs*).
- Rendering: internal-voice intrusions escalate by band (glances → lines
  → Odile arguing in full sentences during other scenes), her idle in
  town shifts (restless, then flushed, then a girl holding herself very
  still), and the vow's UI needle is the only gauge in the game that
  *trembles*. The player should feel their own resolve being spent —
  that's the design working.
- At 100: nothing happens immediately. At the *next rest*, she must pass
  a Resolve check (stacks are the dice pool). Fail, and she breaks the
  vow herself — an autonomous self-play scene the player watches rather
  than directs, Temptation resets to 40, Resolve empties, and the track
  Odile chose for her (her dominant craving) gains a full tier's worth of
  conditioning at enemy-imprint rate. Failure is content and a build
  swerve, never a game over: the game is very interested in what she does
  the morning after — re-swear (once, at double price) or walk the tracks
  like everyone else.

**The final payoff (worth the hard mode).** Milestone keeps pay out so the
run isn't all-or-nothing: vow held through campaign thirds → at each, one
*major* permanent boon, escalating:

1. **First third — Stillwater Mind:** once per expedition, completely
   clear her Lust. (The vow's answer to the expedition clock: she bought
   her own sink.)
2. **Second third — The Untempted Eye:** Second Sight without Depth —
   she sees conditioning, triggers, and hidden desires in others, having
   bought with refusal what the deep girls bought with surrender. Mirrors
   optional.
3. **Final third, held to the ending — the Untouched Ending and the
   Crown of Resolve:** a permanent stat package (+2 all, the largest
   single award in the game), the unique ending in which she breaks the
   curse *by out-waiting it* — Odile not exorcised but out-negotiated,
   present, furious, and (the text is explicit) a little proud of her —
   and a New Game+ unlock: **Odile Mode**, playing the campaign from the
   alter ego's side with all tracks pre-installed at tier 2 and the vow
   inverted (her Temptation is *other people's* restraint).

The payoff is worth it in the only currencies this game respects: the
strongest single mechanical award, an ending no track-build can reach,
and the NG+ mode. The cost is a campaign of saying no while the game
makes yes pay gold, stats, and skills in front of you. That asymmetry —
tracks pay *now*, the vow pays *at the end* — is the whole design, and
it's why Temptation has to be felt rather than merely counted.

---

## 6. Surfaces and production notes

- **UI.** One new screen: the **Body & Tracks wheel** — her portrait,
  three (later more) track dials with tier pips, craving clocks, Depth
  pips, and — only while sworn — the Temptation needle. In combat nothing
  new is drawn: cravings express through the existing Battle-Lust bar and
  disobedience system, which is the point — this system lives inside the
  design basis's machinery, not beside it.
- **Audio (torori).** Subspace sessions are the conditioning kit's first
  consumer: induction voice, whisper/affirmation loops (in-house
  production gaps, already catalogued), the identical trigger snap. Track
  sessions key their reaction audio to the act and tier via the studio's
  reaction-profile system (buildup readable by sound, peaks synced to
  events) — a tier-5 session should *sound* conditioned, not just read so.
- **Numbers are starting values.** Session gains (4/7/10), benefit rolls
  (55% / 12%+1% / 5%+1%), craving periods (6 − tier days), Temptation
  gains — all first-pass tuning for a playable prototype, stated so they
  can be argued with concretely.
- **What this resolves from the hypnosis design's forks.** Fork 1 (who
  conditions her): answered structurally — *she does, partners do, and
  enemies do*, at different rates with different residue. Fork 2
  (reversibility): tracks inherit the near-ratchet — cleansing exists per
  track (partner-imprint flavor and one tier at a time, church-priced);
  the ratchet's weight is the design. Fork 3 (Odile's veto): unchanged —
  veto at a Lust cost, never free, never impossible.

## 7. Open forks

1. **Names. RESOLVED (the studio, 2026-10-26).** Title **MoonDeep**;
   heroine **Odette**, alter ego **Odile** (§1).
2. **Vow scope.** This draft scopes the vow to self-pleasure (partner/
   enemy input feeds Temptation double). Alternative: a *total* vow
   (any orgasm breaks it) — harder, cleaner, probably the true hard mode;
   it changes §5's Temptation table.
3. **Party scope.** Battle-Lust in the design basis is party-wide; this draft specs
   tracks for the heroine, with §4.1's Gentle Hands as the first bridge.
   Do party members get full track sets (a build matrix per girl, per the
   studio's per-heroine hidden-desire rule) or heroine-only depth with
   party members on Lust alone?
