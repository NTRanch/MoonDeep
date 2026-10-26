# MoonDeep — Build Plan (Commissioned)

**Status:** Commissioned by the studio, 2026-10-26. Engine **RULED**:
Rust + Bevy. Design of record: the design-basis notes (Battle-Lust),
docs/design-hypnosis.md (Depth), docs/design-conditioning-tracks.md (tracks, craving,
subspace, the Untouched vow) — design APPROVED by the studio as drafted,
names RULED: **MoonDeep** / **Odette** (heroine) / **Odile** (alter ego,
single-l ballet spelling). Behavior/concept level only — no source-game
assets, text, art, or code. NTRanch lane only; studio attribution; no
Light Show linkage.

**Two binding conditions from the commission (the studio, 2026-10-26):**

1. **Learning vehicle.** MoonDeep deliberately uses Bevy tooling and
   features the studio has **not** used yet, so building it teaches the
   studio new Bevy. Novelty must ride on genuine use — each new tool is
   assigned to the slice where it is actually the right tool (§3).
2. **Hands-On levels.** MoonDeep's build is simultaneously designed as
   a level track for Hands-On, in the same shape as the
   existing Playroom/Study curriculum (§6). The curriculum edit itself
   is gated separately by the maintainers; this plan carries the design section
   only and does not touch the Hands-On tree.

**Art is the bottleneck, and this plan does not pretend otherwise.**
Odette's painted rig parts (dense-mesh rig over character-pipeline
painted art is the studio's ruled production route) gate every
presentation milestone. No art deliverable is scheduled anywhere in
this plan; slices are ordered so the game is fully playable and
gate-verifiable on placeholder geometry until art lands, and art
arrival never blocks a core gate.

---

## 1. Architecture — core first, shell thin

The Hands-On pattern, applied to a full game:

```
moondeep/                       (workspace)
├── crates/
│   ├── moondeep-core/          pure Rust game logic — ZERO engine refs
│   └── moondeep-app/           the Bevy shell — draws, plays sound, nothing else decides
└── assets/                     shell-side only (scenes, RON data, audio)
```

### 1.1 `moondeep-core` — the game itself

Everything the design docs specify as *rules* lives here, engine-free,
deterministic, headless-testable:

| Module (alphabetical) | Owns |
|---|---|
| `battle` | Turn engine: speed-ordered turns, command issue, the disobedience roll and substitution table, Succumb state, lust-cinematic finisher eligibility |
| `conditioning` | Per-track conditioning (0–100, tiers 0–5 at 20/40/60/80/100), the three sources (Self 4 / Partner 7 / Enemy 10 per interval) and their residue rules |
| `craving` | Per-track craving clocks: period `max(1, 6 − tier)` days, unmet escalation (voice lines → +10% Lust gain per unmet track → disobedience-table entry at double-period) |
| `depth` | The Depth ratchet (tiers 1–5), tier benefits (Echoes, Second Sight, Whisper Motes, The Wielded Bar, Two Hands on the Wheel), named triggers, susceptibility compounding, enemy imprinting and trigger variants, the one-time Unraveling |
| `economy` | Gold flows: church tiered removal (50 g base tier shape from the design basis), fountain partial reduction, track income flavors (Dairy sales, Service wages, Doll gifts/tribute) |
| `expedition` | The expedition clock: Lust per character 0–100, raised **only** by landed lust-channel attacks, **never decays in the field**; HP as a fully separate axis with separate services |
| `party` | Party state, per-character Lust/profiles, shared-source Depth resonance |
| `rng` | The run's seeded RNG stream: every roll (disobedience, benefit, spark) draws at a defined tick point; sessions and battles replay exactly from seed |
| `session` | Subspace sessions: intervals, source selection, benefit engine (gold 55%; stat glimpse 12% + 1%/interval spent, one glimpse converting permanent at a tier crossing; skill spark 5% + 1%/interval beyond the third, duplicates → permanent stat +1), subspace multipliers (conditioning ×1.5 in subspace; Depth amplifier ×(1 + 0.25 × Depth tier)) |
| `tracks` | The three track specs as data (Dairy, Service, Doll) + the §4.5 extension frame — a track is a record (act, install, economy, agency expression, presentation stages ≤3, endings), not a code path |
| `vow` | The Untouched Path: vow state, Resolve stacks (+2% XP, +1% crit per stack, cap 10; one stack spendable to auto-pass a disobedience roll), Temptation (0–100; +2 landed lust attack, +3/day per unmet installed craving, +5 per subspace entry, +1 per vetoed Odile-first dialogue), the next-rest Resolve check and the break/re-swear rules, milestone boons by campaign thirds (Stillwater Mind, The Untempted Eye, Crown of Resolve + Untouched ending + Odile Mode unlock) |
| `world` | Campaign state: day clock, town/dungeon structure, ending evaluation (per-track agency-flip endings, *Fully Hers* composite at 3+ tracks tier 4+, Depth-gated endings, Untouched ending) |

**Core laws (inherited, non-negotiable):**

- **Determinism.** Fixed-step evaluation; no wall-clock randomness
  anywhere; same seed + same inputs = same campaign, byte-for-byte in
  the event log. This is what makes every design number testable.
- **Numbers are the design docs' numbers.** Starting values come from
  design-conditioning-tracks §6 ("stated so they can be argued with
  concretely") and the design basis §3 — the design basis's UNKNOWNs (band edges,
  disobedience curve shape) are *our* tuning constants, named as such
  in one `tuning` module, never smuggled in as if sourced.
- **Typed refusals.** Illegal transitions (self-play while sworn,
  cleansing a track with no imprint residue, spending Resolve at zero
  stacks) return typed errors, never panics or silent no-ops.
- **Tracks are data.** A new track (§4.5 candidates: Oral, Bondage,
  Exhibition, Feet) is a new record + its per-heroine hidden-desire
  line, not a new subsystem.
- **No engine types cross the boundary.** Core speaks in its own
  types; the shell translates. If Bevy were swapped tomorrow, only
  `moondeep-app` dies. (This is also what makes §6's Hands-On levels
  possible: the levels teach the core.)

### 1.2 `moondeep-app` — the Bevy shell

The shell renders core state and forwards input. It owns: window/render,
the rig presentation (lumen-rig-core / Torogao runtime driving Odette's
dense-mesh rig), UI screens (including the **Body & Tracks wheel** —
design-conditioning-tracks §6), dialogue presentation (incl. tier-3+ option
reordering rendered, never decided, by the shell), and audio playback
through the torori reaction contracts (subspace = the conditioning
kit's first consumer; the trigger snap is the **identical sample every
time** — the deliberate inversion of the shuffle-bag rule).

Shell rule: **the shell never decides a game outcome.** If a number
changed, core changed it. Presentation interpolation (expression
ladders, smooth parameter travel) is shell work; state is not.

---

## 2. What the studio already uses (so "new" means new)

Verified from the Hands-On tree (the studio's only Bevy-adjacent
build to date) and Strobe planning:

- **Already studio practice:** pure-Rust core + thin shell split
  (Hands-On's `milking-core`/`hands-on`); ECS discipline as a *taught
  concept* (CURRICULUM P3: components are data, systems are functions,
  the schedule is a contract; change detection; fixed-timestep
  scheduling); fixed-step deterministic evaluation with seeded RNG and
  twin-run hash gates; RON-flavored data records for profiles.
- **Uncertainty, marked honestly:** Strobe's Bevy slice (its
  SPEC-BEVY design document) is
  *designed, not yet built* — no shipped studio Bevy binary exists
  to audit. Claims below about "not yet used" mean: not present in
  Hands-On's workspace and not built in any Strobe slice at plan time.
  The maintainers should re-verify against the Strobe tree at S0's gate; if a
  feature turns out to be in Strobe use, it drops off the "new" list
  but stays assigned to its slice if it is still the right tool.
- **Refinement (same-day check):** three map entries — Bevy states,
  native `bevy_ui`, Bevy audio — already have studio *design*
  coverage in Hands-On's MASTERY.md Arc A (A14 state machines, A11
  Bevy UI, A12 audio in Bevy) and in SPEC-BEVY's Screen-state/UI
  design. They remain **unused in built code**, so they stay on
  the map — but the honest framing is *first build*, not *first
  contact*: MoonDeep is where designed knowledge becomes shipped
  practice. That strengthens, rather than weakens, their slice
  assignments.

---

## 3. New-to-the-studio Bevy tooling map

Each entry: the tool, why MoonDeep genuinely needs it, the slice that
adopts it (§4), and what the studio learns. Ordered alphabetically,
per studio convention.

| Tool / feature | Genuine MoonDeep use | Slice | Learns |
|---|---|---|---|
| **Asset pipeline + hot reload** (`AssetServer`, custom `AssetLoader`, `bevy_asset` diagnostics) | Track specs, dialogue, tuning, and scene data must be data files the studio can tweak without recompiling; hot reload makes tuning sessions (the design docs' numbers are first-pass) a live loop instead of a rebuild loop | S1, deepened S8 | Assets as typed, loadable, reloadable data; loader error handling |
| **Audio: `bevy_audio` + `kira` backend** | Torori reaction audio needs layered loops, event one-shots, and parameter-driven playback on the fixed-step clock; kira's tweens/clocks are the studio's first real game-audio mixing layer (Hands-On has no audio by design) | S7 | Game audio architecture: buses, layering, clock-synced playback |
| **Bevy states + sub-states** (`States`, `SubStates`, `OnEnter`/`OnExit`) | MoonDeep is a state machine wearing a game: Town / Expedition / Combat / Subspace / Rest, and Subspace is naturally a *sub-state* of both Town and Camp. The design's clocks key off state entry/exit | S2 | State-scoped systems and cleanup; sub-states vs. flag soup |
| **Dynamic scenes + reflection** (`DynamicScene`, `Reflect`, `TypeRegistry`) | Town locations, induction sites, and NPC surfaces are content, not code; reflection-driven scene files let locations be authored as data and spawned/despawned whole | S5 | Reflection, the type registry, data-authored worlds |
| **Input focus + gamepad/keyboard navigation** (`bevy_input_focus`) | A JRPG-shape UI is menu-driven; focus management is what makes the Body & Tracks wheel and dialogue navigable by keyboard/gamepad instead of mouse-only | S6 | Focus graphs, directional navigation, accessible menu structure |
| **`bevy_egui` — as the debug/inspector lane only** | Tuning the design docs' starting numbers needs a live inspector (Lust bands, roll rates, craving clocks). egui is the right tool for *developer* surfaces; it is explicitly **not** the shipped UI (see next row) — learning where the line sits is part of the lesson | S3 (debug builds only) | Immediate-mode UI, and the discipline of keeping it out of the shipping surface |
| **Native `bevy_ui` widgets + observers** (`Button`, `Node`, interaction observers) | The shipped UI (dialogue panels, menus, the Body & Tracks wheel) built on Bevy's own UI — the studio has never shipped `bevy_ui`; Bevy's UI is its weakest part (flagged at commission), so this is the deliberate hard-mode pick the studio asked to learn | S6 | Native UI layout, widget events via observers, styling as data |
| **Tilemap approach: hand-rolled chunked tile layers on `bevy_sprite`** (no tilemap crate in v1) | Dungeon/town exploration needs tile maps; building the layer by hand on Bevy sprites (rather than adopting `bevy_ecs_tilemap` sight-unseen) teaches what a tilemap *is*; adopting the crate later becomes an informed decision, and the comparison is a named S4 exit question | S4 | Tile/chunk rendering, texture atlases, map data flow |
| **Animation graphs — rig-driven, not `AnimationPlayer`** (deliberate non-adoption, recorded) | Odette's animation is the studio rig runtime's job (dense-mesh, fixed-step), not Bevy skeletal animation. Recorded here so the map is honest: Bevy's animation graph is *evaluated and declined* for characters; it remains a candidate for UI/prop motion only | — (decision recorded at S4) | Reading a feature and declining it on fit is also tooling literacy |

**Explicitly not new** (studio already there, listed so nobody
double-counts learning value): ECS basics, schedules, change
detection, fixed timestep, seeded determinism, RON data records,
custom shaders/WGSL (the studio's shader work predates this plan).

---

## 4. Slice plan — core first, every slice gated

Studio gate style throughout: cargo test + strict clippy + fmt on
both machines where the tranche calls for it, twin-run determinism
proofs for anything touching the RNG stream, per-slice acceptance
criteria stated *before* the slice starts. Test counts below are
**floors set at slice start** (the slice brief finalizes them); a
slice that lands under its floor has not landed.

### S0 — Workspace + tuning skeleton
- moondeep workspace: `moondeep-core` + `moondeep-app` (window that
  opens, nothing more), latest Rust, pinned Bevy version (one version
  per project; upgrades are deliberate events), `tuning` module
  carrying every starting number from the design docs, named.
- **Acceptance:** build + clippy + fmt clean; `cargo test` green with
  the tuning round-trip tests (every design-doc number present and
  sourced to its doc section in a comment); shell opens a window on
  the studio build machine and in the development sandbox.

### S1 — Data layer: tracks, dialogue, tuning as assets
- Track specs (§4.1–4.3 + extension frame), dialogue records, and
  tuning load from data files through the asset pipeline; hot reload
  in debug builds.
- **Acceptance:** headless test — core builds all three tracks from
  the shipped data files and rejects a malformed record with a typed
  error naming the field; shell test — editing a tuning value in the
  data file changes core behavior without recompilation (debug).

### S2 — Expedition & Battle-Lust (core) + state skeleton (shell)
- Core: `expedition` + `battle` + `rng` — Lust 0–100 event-raised
  only, no field decay; upper-band disobedience with substitution
  classes (solo / ally / enemy); Succumb at max; finisher
  eligibility; HP fully separate. Shell: Bevy states skeleton
  (Town/Expedition/Combat/Rest) driving a placeholder battle screen.
- **Acceptance:** core test floor — the design-basis battery: no-decay
  across a simulated expedition; disobedience only inside the band;
  Succumb exactly at cap; finisher locked below cap; twin-run from
  seed produces identical event logs. Shell: state transitions
  exercised headlessly via Bevy's test harness where possible, else
  scripted smoke on the studio build machine.

### S3 — Town sink + economy (core) + tuning inspector (shell, debug)
- Church tiered removal, fountain partial reduction, gold accounting;
  the expedition clock becomes playable end-to-end: go out, wear
  down, retreat, pay, repeat. egui inspector (debug only) exposes
  bands, rates, and clocks live.
- **Acceptance:** scripted expedition loop test (deterministic,
  seeded) asserting Lust only ever falls at town services; price
  tiers match `tuning`; inspector present in debug, **absent** in
  release (build-flag test).

### S4 — Exploration shell: tile layers, scenes, rig presentation stub
- Hand-rolled tile layers for town + one dungeon; placeholder-geometry
  Odette driven through the rig runtime's parameter surface (the
  animation-graph non-adoption is recorded here); exit question
  answered in the slice report: keep hand-rolled tiles or adopt
  `bevy_ecs_tilemap` for S8's content growth.
- **Acceptance:** both maps load from data; rig parameter travel
  interpolates smoothly (no frame cuts — the studio's standing rule)
  against recorded parameter traces; tile decision written down with
  reasons.

### S5 — Depth & induction (core) + authored locations (shell)
- Core: `depth` complete — sessions at induction sites, tier
  benefits as queryable capabilities, named triggers, susceptibility
  compounding, imprinting + cleansing, the Unraveling (once, one
  tier). Shell: sites authored as dynamic scenes via reflection.
- **Acceptance:** tier-benefit tests per tier (Echoes/Second Sight/
  Motes/Wielded Bar/steered Succumb each proven as a capability
  flag + one behavioral test); trigger-variant cleansing test;
  Unraveling second use refused typed; scene spawn/despawn leaves
  no orphaned entities (entity-count assertion).

### S6 — Subspace, sessions, tracks & craving (core) + native UI (shell)
- The biggest core slice: `session`, `conditioning`, `craving`,
  `tracks` — subspace entry (site / Trance stance / self-induction
  at Depth 2+), the full benefit engine, craving escalation into
  the disobedience table, dominant-track resolution, dialogue
  reordering *decided in core* (shell only renders order). Shell:
  native `bevy_ui` Body & Tracks wheel + dialogue, input focus and
  gamepad navigation.
- **Acceptance:** benefit-roll distribution tests over seeded runs
  (55% / glimpse / spark rates within stated tolerance of the design
  numbers, incl. the glimpse→permanent conversion at tier
  crossings and spark-duplicate→stat conversion); craving period
  `max(1, 6 − tier)` proven per tier; Depth amplifier and subspace
  ×1.5 multiply in the documented order; UI: wheel reachable and
  fully operable by keyboard alone (scripted focus walk).

### S7 — Reaction audio (torori contracts) in the shell
- bevy_audio/kira wiring: layered loops + event one-shots on the
  fixed-step clock; subspace sessions as first consumer of the
  conditioning kit (induction voice, whisper loops — in-house
  production gaps, consumed as cleared files only); trigger snap =
  identical sample, asserted in test.
- **Acceptance:** silent-verification only (studio audio rule):
  loudness/waveform metrics on rendered mixes, no audible testing
  outside the studio's own play; snap-sample hash identical across
  a session's triggers; audio state follows core events 1:1 in a
  recorded trace. **This slice consumes torori; it does not build
  the torori MCP** (it builds on its own standing sequence).

### S8 — The Untouched Path + endings + campaign loop
- Core: `vow` complete + `world` ending evaluation: Resolve/
  Temptation full table, next-rest check, break & re-swear (once,
  double price), milestone boons by thirds, all endings (per-track
  flips, *Fully Hers*, Depth endings, Untouched + Odile Mode flag).
- **Acceptance:** a fully scripted vow campaign (seeded, headless)
  reaches each milestone and the Untouched ending; a scripted
  break-path campaign lands the morning-after state exactly as
  designed (Temptation 40, Resolve empty, dominant-craving track
  +1 tier at enemy-imprint rate); ending-priority test: dominant
  track wins, composite overrides at 3+ tracks tier 4+.

### S9 — Hardening & the studio's play gate
- Adversarial half of the test suite (the studio's 50/50 split):
  malformed data, impossible transitions, RNG-stream abuse,
  save/load mid-session integrity; save format versioned.
  Then the real gate: **the studio plays it.** Slices S0–S8 prove
  the numbers; only play proves the game.
- **Acceptance:** full gate suite green on the studio build machine incl. the
  editor-LSP gate for the workspace; studio play verdict recorded — pass,
  or the loop returns to the named slice.

**Ordering note:** S2→S3→S5→S6→S8 is the core spine; S1 precedes
all of it (data before systems); S4 and S7 are shell slices that
can interleave once their core inputs exist. No slice waits on
art (see §7, Fork A).

---

## 5. Milestones & gates

| Gate | After | Proves |
|---|---|---|
| **G0 — Skeleton** | S0–S1 | Workspace honest: latest Rust, pinned Bevy, data loads, tuning sourced |
| **G1 — The clock works** | S2–S3 | Battle-Lust end-to-end: the design basis's mechanic, playable as a loop on placeholder presentation |
| **G2 — Depth lands** | S5 | The Remothered bargain is mechanical, not prose: tiers give and take, triggers exist, imprinting costs |
| **G3 — She becomes** | S6 | Tracks + craving + sessions: the approved design, fully mechanical; the Body & Tracks wheel is the shipped UI |
| **G4 — It sounds** | S7 | Torori contracts drive the shell; conditioning kit consumed; silent-verification evidence only |
| **G5 — Both roads end** | S8 | Tracks endings *and* the Untouched Path reach their endings in scripted campaigns |
| **G6 — Studio play gate** | S9 | The studio plays MoonDeep and rules. Nothing before this gate is called "the game" in public-facing text — it is "the build at gate Gn" |

Standing gates riding every slice: cargo test floors met or
exceeded, strict clippy, fmt, twin-run determinism where the RNG
stream is touched, forbidden-string hygiene over public artifacts
(NTRanch lane rules), editor-LSP gate at workspace milestones.

---

## 6. Hands-On integration — the MoonDeep Track (design only)

A new Hands-On track in the curriculum's own shape: the Playroom
teaches by *playing a system on a host*; the Study teaches by
*sitting with the code*. MoonDeep is a full game, so its track —
**the Moonlight Track (M1–M8)** — runs in Playroom shape, hosted by
**Odette herself** (with Odile as the track's second voice — the
host pair is the lesson's subject: two agents, one body, negotiated
agency). Each level: the learner *plays a slice of MoonDeep*, then
opens the `moondeep-core` module it twins and finds the numbers
they just felt. Host note: Odette/Odile join the Hands-On cast as
this track's hosts — the CAST.md records are the maintainers' separate gated
edit, not this plan's.

| # | Level | What the learner builds / does | Concept it teaches | Completion evidence | MoonDeep twin |
|---|---|---|---|---|---|
| M1 | **The Bar That Only Rises** | Plays a scripted expedition against lust-channel enemies; then sets the band edge and disobedience curve in tuning data and replays | Event-raised accumulators; no-decay as a clock; agency-loss instead of stat-loss | Twin-run event logs identical from seed; the learner's tuned band changes disobedience onset and the log proves where | `expedition`, `battle`, `rng` (S2) |
| M2 | **The Town Is the Sink** | Runs the expedition→church→expedition loop; prices the church tiers in data and watches expedition profitability bend | Sinks vs. sources; mechanic-to-economy wiring; paying for state | A seeded ledger run: Lust falls *only* at services; gold delta matches hand-computed tiers | `economy` (S3) |
| M3 | **Going Deeper on Purpose** | Takes Odette through two Depth tiers at induction sites; spends a trigger knowingly to escape a fight, then suffers an enemy who learned it | Ratchets; benefit/cost pairing per tier; secrets as mechanics (a trigger is intel) | Tier-benefit checklist demonstrated in play; the leaked-trigger ambush triggers — and the ally snap-out rescues — on script | `depth` (S5) |
| M4 | **Three Sources, Three Prices** | Conditions the same track three ways across three sessions (self / the Dairykeeper / a lost fight) and compares gain, residue, and craving flavor | One system, three social geometries; residue as a design material | Session reports compared side by side; cleansing removes exactly the imprint, at the documented price | `session`, `conditioning` (S6) |
| M5 | **The Benefit Engine** | Runs long vs. short sessions and audits the rolls: gold, glimpses, sparks — then catches a glimpse converting permanent at a tier crossing | Probability as a felt economy; seeded RNG audit; the same roll becoming a guarantee | The learner's audit sheet matches the seeded roll log line for line; distribution within tolerance over the long run | `session` benefit engine (S6) |
| M6 | **Craving Is a Clock** | Lets a craving go overdue on purpose: voice lines, Lust-gain creep, then the disobedience table firing *the craving's act* mid-fight | Pressure without stat taxes; escalation ladders; systems expressing character | Overdue run log shows all three escalation steps in order; satisfying the craving resets the period exactly | `craving` (S6) |
| M7 | **The Wheel** | Navigates the Body & Tracks wheel and a tier-3+ dialogue by keyboard alone; reorders nothing — core decided the order — then reads the record that decided it | UI as rendering of state, never decider of it; focus/navigation as a system; dialogue reordering as a *core* rule | Scripted focus walk completes; the learner names the core record and field that ordered the dialogue | `moondeep-app` UI + `tracks` (S6) |
| M8 | **The Untouched Run** | Plays the vow: swears it, spends Resolve to pass a roll, feels Temptation's needle — then (scripted branch) breaks it at a rest and plays the morning after | Hard modes as inverted economies; end-loaded payoff design; failure as content, never game-over | Milestone boons land at the thirds; break-path state matches the design (Temptation 40, Resolve empty, +1 tier at imprint rate); re-swear at double price or walk away — both paths completable | `vow`, `world` (S8) |

**Track shape notes (for the maintainers' gated curriculum edit):** the
Moonlight Track slots beside the Playroom as a third named track
(the menu already carries Playroom + Study; a third track is a
registry addition, not a framework change — CURRICULUM's registry
is a data table). Levels are *designed* here in the same sense
P2/P3/P5–P9 are designed: buildable when their MoonDeep slice
lands, playable only after it. The Study could later twin M1–M8
as code sittings (S-lesson style) — deliberately **not** designed
here; one track first.

---

## 7. Open forks for the maintainers

- **Fork A — Art sequencing (the real schedule risk).** Odette's
  painted rig parts gate every *presentation* claim past S4's
  stub. Options: (i) commission Odette's character-pipeline run
  (identity record → anchor → expression ladder → studio eye keeper
  gate) in parallel with S0–S2, so parts exist by S4; (ii) build
  core-complete on stubs and commission art at G1. Recommendation:
  (i) — the pipeline is per-girl and slow, the core is not
  blocked either way, and S4's rig traces want real parts. Either
  way: **no art date is promised in this plan.**
- **Fork B — Bevy version pin.** "Latest Rust" is ruled; the Bevy
  pin is not. Bevy churns fast; the plan assumes pinning the
  current stable at S0 and treating upgrades as deliberate events.
  The maintainers confirm the exact version at S0's brief.
- **Fork C — Party scope (carried from design-conditioning-tracks §7.3,
  still open).** This plan's core is written per-character for
  Lust from S2 (the design basis is party-wide) but specs tracks for
  Odette, with party bridges (Gentle Hands class) as designed.
  Full per-girl track sets multiply content and cast work; the
  core's `tracks`-as-data shape supports either ruling without
  re-architecture. Needs a studio decision before S6's brief.
- **Fork D — Vow scope (carried from design-conditioning-tracks §7.2,
  still open).** The plan implements the drafted scope (vow covers
  her own hands; partner/enemy input feeds Temptation double).
  The total-vow alternative changes `vow`'s Temptation table;
  cheapest before S8, expensive after. Needs a studio decision
  before S8's brief.
- **Fork E — egui containment.** The inspector is debug-only by
  build flag, with a release-absence test at S3. If the maintainers prefer
  zero egui in the dependency tree of the shipping crate, the
  inspector moves to a separate dev binary at S3 (small cost,
  cleaner tree). The maintainers' call at S3's brief.
- **Fork F — Save format & campaign length.** S9 versions a save
  format, but campaign length (how many expedition days the
  milestone thirds divide) is a design number the docs leave
  open. It lands in `tuning` at S8 and is the studio's tuning
  call at play, not a blocker.

---

## 8. What this plan is not

- Not a build schedule: no dates, no art promises (§7 Fork A).
- Not the Hands-On curriculum edit: §6 is the design section the maintainers
  gate separately; the Hands-On tree is untouched by this plan.
- Not a cast expansion: party girls beyond Odette are Fork C's
  question, and each would need her own per-heroine hidden-desire
  line before any track ships for her (the design docs' binding
  rule).
- Not a torori build: S7 consumes torori's contracts; the MCP
  builds on its own standing sequence.
