# gamedev-coach

A Claude plugin marketplace of **Socratic game-design skills** that coach a designer through the pre-production process — the thinking and shaping that happens *before* any code is written.

Each skill drives the work forward the way a good design mentor would: by asking one focused question at a time, reflecting the answer back more sharply, helping the designer converge instead of sprawl, and ending with a real artifact saved to disk.

## Who it's for

Game designers — especially students and newer designers who have plenty of ideas but want help focusing them and moving through a real process. The skills speak to you as a peer learning the craft, using real design vocabulary.

## The pipeline

Game design before code moves from a fuzzy idea to a spec concrete enough to prototype. These skills follow that arc. The pipeline is being built out phase by phase:

| Phase | Skill | What it does | Status |
| :-- | :-- | :-- | :-- |
| 1. Concept | `game-concept` | Turns a raw idea into one sharp concept: high-concept line, pitch, player fantasy, hook, comparables, audience. | ✅ Available |
| 2. Pillars | `game-pillars` | Derives the 2–4 commitments every later decision is checked against. | 🔜 Planned |
| 3. Core loop | `game-core-loop` | Drafts and stress-tests the moment-to-moment loop and primary verbs. | 🔜 Planned |
| 4. GDD | `game-gdd` | Scaffolds and maintains the living Game Design Document. | 🔜 Planned |
| 5. Scope | `game-scope` | Pressure-tests scope and feasibility against a realistic timeline. | 🔜 Planned |

Each skill hands off to the next, so a session in one phase points you to where to go next.

## Install

```shell
/plugin marketplace add Itschrismorgan/gamedev-coach
/plugin install game-design@gamedev-coach
```

Then start a session by just describing a game idea, or saying something like "help me figure out my game idea."

## Repository layout

```
gamedev-coach/
├── .claude-plugin/
│   └── marketplace.json        # the marketplace catalog
└── plugins/
    └── game-design/
        ├── .claude-plugin/
        │   └── plugin.json     # the plugin manifest
        └── skills/
            └── game-concept/
                ├── SKILL.md
                └── assets/
                    └── concept-template.md
```

## License

MIT — see [LICENSE](LICENSE).
