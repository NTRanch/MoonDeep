---
name: "moondeep"
description: "Project conventions for MoonDeep (Nice Thoughts Ranch): the core-first architecture (moondeep-core decides, moondeep-app only draws), gate discipline G0–G6 with slice test floors, the design documents of record and which one owns what, determinism and twin-run evidence, the texture ladder, the audio silence rule and torori contracts, and studio attribution. Use when implementing a slice, tuning a design number, adding a track, or editing any file in this repository."
---

# MoonDeep — project conventions

## What this project is

A painterly fantasy adventure RPG: Odette, a proud knight, and
Odile, the cursed alter ego who shares her body. Battle-Lust is
the expedition clock; Depth is the campaign-long conditioning
ratchet; the conditioning tracks (Dairy, Service, Doll) are
cravings with economies and endings; the Untouched Path is the
abstinence hard mode. The build doubles as the Moonlight Track
(M1–M8) for Hands-On — building the game is the curriculum.

## Documents of record

- `docs/roadmap.md` owns the build — architecture, slices
  S0–S9, gates G0–G6, the new-tooling map, and the open forks.
- `docs/design-conditioning-tracks.md` owns the tracks —
  sessions, the benefit engine, craving, the three launch
  tracks, track interactions, and the Untouched Path.
- `docs/design-hypnosis.md` owns Depth — the tier bargain,
  triggers, imprinting, and the fusion with Battle-Lust.
- `.ai/memory/` owns state — current, decisions, handoffs.
  Findings go to the inbox first and are promoted when
  validated. Design changes are recorded in `decisions.md`.

## The architecture law

- `moondeep-core` is the game: pure Rust, **zero engine
  references**, deterministic, headless-testable. Every rule —
  Battle-Lust, Depth, tracks, craving, the vow — lives here.
- `moondeep-app` is the shell: it renders core state, forwards
  input, presents the rig, and plays audio. **The shell never
  decides a game outcome.** If a number changed, core changed
  it. Dialogue reordering, disobedience substitution, ending
  evaluation — all core decisions the shell only renders.
- No engine types cross the boundary. Core speaks in its own
  types; the shell translates.
- Tracks are data, not code paths: a new track is a record
  (act, install, economy, agency expression, presentation
  stages ≤ 3, agency-flip ending) plus its per-heroine
  hidden-desire line.
- Illegal transitions return typed errors — never panics, never
  silent no-ops.

## Numbers and determinism

- Starting values are the design docs' numbers. Open questions
  in the design basis (band edges, the disobedience curve) are
  **our** tuning constants, named as such in the one `tuning`
  module, each sourced to its doc section — never smuggled in
  as if sourced.
- Fixed-step evaluation; no wall-clock randomness anywhere.
  Every roll draws from the run's seeded RNG stream at a
  defined tick point. Same seed + same inputs = same campaign,
  byte-for-byte in the event log.
- Anything that touches the RNG stream ships with a twin-run
  determinism proof.

## Gate discipline

- Slices land under the roadmap's gates (G0–G6). Test counts are
  **floors set at slice start**; a slice that lands under its
  floor has not landed. The test split is half validation, half
  adversarial.
- Report exactly what ran: tests passed/failed, clippy and fmt
  state, what was skipped. Never claim a gate that did not run.
- Nothing is called "the game" in public-facing text before the
  studio play gate (G6) passes — before that, "the build at
  gate Gn".
- Each slice uses the Bevy tooling the roadmap §3 assigns to
  it; that assignment is the learning curriculum, not a
  suggestion. `bevy_egui` is the debug/inspector lane only and
  never ships in the release surface.

## Style, texture, and audio rules

- Art lane: painterly. Characters are dense-mesh rigs over
  character-pipeline painted art, driven by the studio rig
  runtime; presentation interpolation is shell work, state is
  not.
- Texture ladder: build and test at the highest quality first
  (lossless masters, full resolution), then step down
  incrementally with measurements at each step. The shipping
  floor is set by eye, one tier above the step that stops
  cutting it.
- Audio silence: generation, QC, and verification are silent
  (loudness, waveform, file metrics only); nothing autoplays;
  audible testing happens only when the studio expressly
  presses play.
- Reaction audio follows the torori contracts: layered loops
  plus event one-shots on the fixed-step clock. The
  conditioning trigger snap is the **identical sample every
  time** — the deliberate inversion of the shuffle-bag rule.

## Attribution and hygiene

- Public artifacts carry studio attribution only:
  Nice Thoughts Ranch.
- Keep lists, modules, and file entries in alphabetical order
  unless dependency order requires otherwise.
