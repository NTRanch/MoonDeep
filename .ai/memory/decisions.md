# Decisions (studio rulings)

- COMMISSION (2026-10-26): MoonDeep is a commissioned build, not
  a study. The design documents in `docs/` are approved as
  drafted; changes to them are design decisions, recorded here.
- ENGINE (2026-10-26): Rust + Bevy. The game is turn-based,
  state-heavy, and content-heavy; the choice is a studio-stack
  decision — the deterministic rig runtime, the reaction-audio
  contracts, and the seeded-RNG fixed-step idiom the design
  leans on are all Rust, and the build shares a spine with the
  studio's other Bevy work. Latest Rust; the Bevy version is
  pinned per project and upgrades are deliberate events
  (roadmap §7, Fork B).
- NAMES (2026-10-26): the title is **MoonDeep**. The heroine is
  **Odette** (a proud knight, the white swan); her alter ego is
  **Odile** (single-l, the ballet spelling; an initial double-l
  spelling was corrected the same day). Runner-up pair Celeste /
  Noctis was considered and not adopted.
- LEARNING VEHICLE (2026-10-26): the build deliberately uses
  Bevy tooling the studio has not used before (roadmap §3),
  assigned where each tool is genuinely the right one — novelty
  rides on real use, never on novelty for its own sake.
- HANDS-ON TRACK (2026-10-26): MoonDeep's build is designed as
  the Moonlight Track (M1–M8) for Hands-On, hosted by Odette
  with Odile as second voice. The track design lives in roadmap
  §6; the Hands-On curriculum edit is gated separately.
- HEADER (2026-10-26): the keeper header is
  `assets/moondeep-header.png` — the pendulum-and-swan-feathers
  treatment, borderless form.
- TEXTURE LADDER (standing studio rule): build and test at the
  highest quality first (lossless masters, full resolution,
  memory accepted), then step down incrementally, measuring at
  each step; the shipping floor is set by eye, one tier above
  the step that stops cutting it.
- AUDIO (standing studio rule): no audio testing is ever
  audible unless the studio expressly presses play. Generation,
  QC, and verification are silent — loudness, waveform, and file
  metrics only; nothing autoplays. Reaction audio follows the
  torori contracts; the conditioning trigger snap is the
  identical sample every time.
- ATTRIBUTION: public artifacts carry studio attribution only
  (Nice Thoughts Ranch).
