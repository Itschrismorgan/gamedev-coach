# gamedev-coach — project guide

This repo is a **Claude plugin marketplace** of Socratic game-design skills. Each skill coaches a designer through one phase of pre-production (the work that happens *before* writing code) by asking focused questions and producing a concrete artifact.

The skills are intended for a college-level game-design student — someone with strong ideas who needs help focusing and driving a real process forward. Treat the designer as a serious peer learning the craft.

---

## Current status / next action (pick up here)

**The five-phase pipeline is complete** — all skills (`game-concept`, `game-pillars`, `game-core-loop`, `game-gdd`, `game-scope`) are **built and pushed to GitHub** at https://github.com/Itschrismorgan/gamedev-coach (branch `main`), plugin at v0.5.0.

Next actions are no longer "build a phase." They are:

1. **Run triggering evals** (see Deferred below). All five descriptions now compete for similar phrasing — this is the moment they were waiting for.
2. **Test the live pipeline** end-to-end with a real game idea (install, run concept → scope, confirm handoffs and at least one loop-back work).
3. Consider tagging **v1.0.0** once evals pass and a live run-through is clean.

**Pipeline shape (decided):** linear *with loop-backs* — a later phase can send the designer back to revise an earlier artifact (e.g. `game-scope` reopening `game-pillars`). Every skill from phase 2 on must therefore handle two entry states (fresh vs. revisit), point its handoff both forward and back, and write to a **revision trail** in its artifact. Scope stays at phase 5 (it's the reality gate that triggers loop-backs); the pipeline stays at five phases. The re-entry + loop-back pattern is established in `game-pillars` — follow it.

To validate and test the live marketplace:

```bash
claude plugin validate .
/plugin marketplace add Itschrismorgan/gamedev-coach
/plugin install game-design@gamedev-coach
```

After adding a new skill, bump `version` in `plugin.json` (and the marketplace entry if pinned), commit, and push; installed users update via `/plugin marketplace update`.

### Deferred

- **Triggering evals (TODO, later).** No skill's `description` has been eval'd yet. Once the pipeline has several skills competing for similar phrasing (concept vs. pillars vs. core-loop overlap), run triggering-accuracy evals with the `skill-creator` skill and tighten descriptions. Undertriggering is the main risk.

---

## Repository layout

```
gamedev-coach/
├── .claude-plugin/
│   └── marketplace.json          # marketplace catalog (lists the plugin)
├── plugins/
│   └── game-design/              # ONE plugin holds ALL phase skills
│       ├── .claude-plugin/
│       │   └── plugin.json       # plugin manifest
│       └── skills/
│           ├── game-concept/     # phase 1 skill
│           │   ├── SKILL.md
│           │   └── assets/
│           │       └── concept-template.md
│           ├── game-pillars/     # phase 2 skill
│           │   ├── SKILL.md
│           │   └── assets/
│           │       └── pillars-template.md
│           ├── game-core-loop/   # phase 3 skill
│           │   ├── SKILL.md
│           │   └── assets/
│           │       └── core-loop-template.md
│           ├── game-gdd/          # phase 4 skill
│           │   ├── SKILL.md
│           │   └── assets/
│           │       └── gdd-template.md
│           └── game-scope/        # phase 5 skill (reality gate)
│               ├── SKILL.md
│               └── assets/
│                   └── scope-template.md
├── README.md
├── LICENSE
└── CLAUDE.md                     # this file
```

Decisions already made: repo name `gamedev-coach`; **one plugin** (`game-design`) containing every phase skill, so users install once and get the whole pipeline.

---

## The pipeline (roadmap)

Pre-production moves a fuzzy idea toward a spec concrete enough to prototype. Each skill owns one phase and hands off to the next.

| Phase | Skill | Owns the question | Status |
| :-- | :-- | :-- | :-- |
| 1. Concept | `game-concept` | What is this game, and who's it for? | ✅ Built |
| 2. Pillars | `game-pillars` | What must always be true about it? (2–4 commitments) | ✅ Built |
| 3. Core loop | `game-core-loop` | What does the player repeat, second to second? | ✅ Built |
| 4. GDD | `game-gdd` | The living spec — systems, controls, progression, scope | ✅ Built |
| 5. Scope | `game-scope` | Is this buildable in the time available? | ✅ Built |

The pipeline is complete. `game-scope` is terminal: it hands off to production (build the vertical slice) and is the main source of loop-backs to earlier phases.

---

## Design philosophy (apply to every skill)

These principles are what make the skills work. Keep them consistent across the pipeline.

1. **Drive forward by asking questions.** The skill is a coach, not a form or a scribe. It interrogates the idea so the designer sees it more clearly than before.

2. **One question at a time.** Ask a single question, then stop and wait. Never stack questions. The rhythm — question, answer, reflect, sharpen, next — is the whole point. This is a hard rule.

3. **Be Socratic.** Mirror answers back in crisper words; push on vagueness; name scope creep and "park" tangents without losing them; prefer one concrete moment over abstractions; reward specificity.

4. **Help the designer converge.** The student's failure mode is carrying ten half-ideas. Every skill should narrow and sharpen rather than expand.

5. **Peer-level voice.** Real design vocabulary (player fantasy, core verb, core loop, comparables, MDA), defined briefly the first time. No dumbing down, no lecturing.

6. **End with an artifact + handoff.** Every completed session saves a markdown doc to the designer's working folder (using a template in the skill's `assets/`) and points explicitly to the next phase skill and why it matters.

---

## How to author a new phase skill

1. Create `plugins/game-design/skills/<skill-name>/SKILL.md`.
2. Frontmatter needs `name` and a **pushy, trigger-rich `description`** — list the phrases a designer would actually say, and state when it should fire (and that it follows the previous phase). Undertriggering is the main risk.
3. Body: short framing, then the Socratic interview flow for that phase (a path, not a rigid script), a convergence/synthesis step, an artifact-save step, and a handoff to the next phase.
4. Add a fill-in template under that skill's `assets/`.
5. Bump `version` in `plugin.json` (and the marketplace entry if pinned) so installed users receive the update.
6. `claude plugin validate .`, commit, push. Users get it via `/plugin marketplace update`.

Reference: the `game-concept` skill is the pattern to follow. The official skill-authoring guidance lives in the `skill-creator` skill if you want to run evals on triggering accuracy.

---

## Useful docs

- Marketplaces: https://docs.claude.com/en/docs/claude-code/plugin-marketplaces
- Plugins: https://docs.claude.com/en/docs/claude-code/plugins
