# Current state — 2026-10-26 (founding)

- MoonDeep is the studio's painterly fantasy adventure RPG:
  Odette, a proud knight, and Odile, the cursed alter ego who
  shares her body. Its systems are Battle-Lust (the expedition
  clock), Depth (campaign-long hypnotic conditioning), the
  conditioning tracks (Dairy, Service, Doll), and the Untouched
  Path (the abstinence hard mode). All design is complete,
  approved, and of record in `docs/`.
- Build commissioned 2026-10-26. Engine: Rust + Bevy, latest
  Rust, one pinned Bevy version per project. Architecture:
  `moondeep-core` (pure Rust, zero engine references, every rule
  deterministic and headless-testable) plus `moondeep-app` (the
  thin Bevy shell — it draws and plays sound; it never decides a
  game outcome).
- No code exists yet. The roadmap (`docs/roadmap.md`) runs
  slices S0–S9 under gates G0–G6; S0 (workspace + tuning
  skeleton) is the next step. Nothing is called "the game" in
  public-facing text until the studio play gate (G6) passes —
  before that it is "the build at gate Gn".
- Art is the bottleneck and is not scheduled anywhere: Odette's
  painted rig parts (dense-mesh rig over character-pipeline
  painted art, at the highest texture quality first) gate every
  presentation claim past S4's stub. Core slices are ordered so
  the game is fully playable and gate-verifiable on placeholder
  geometry until art lands.
- MoonDeep's build is simultaneously the Hands-On **Moonlight
  Track** (M1–M8, designed in roadmap §6): each slice twins with
  a level hosted by Odette, with Odile as the track's second
  voice. The curriculum edit itself is a separate gated step in
  the Hands-On repo; this repo carries the design only.
- The repo ships with a bloch memory tree (`.ai/memory/`), the
  project skill (`skills/moondeep/`), and the keeper header
  (`assets/moondeep-header.png`, approved 2026-10-26).
