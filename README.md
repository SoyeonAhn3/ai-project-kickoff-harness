🌐 [한국어](./README_ko.md) | [English](./README.md)

# AI Project Kickoff Harness

> A CLI automation harness that transforms vague project ideas into structured, development-ready plans through AI-driven interviews and validation.

## Overview

Many projects fail not because of bad code, but because requirements were unclear before development started. This harness solves that by conducting structured interviews, identifying gaps and contradictions, and generating a comprehensive kickoff document — all before a single line of code is written.

Developed using its own process (dogfooding): the harness was used to plan itself across 2 iterations, discovering and fixing 7 design improvements in the process.

## Table of Contents

- [How It Works](#how-it-works)
- [Technology](#technology)
- [Quick Start](#quick-start)
- [Project Structure](#project-structure)
- [Development Methodology](#development-methodology)
- [Documents](#documents)
- [Current Status](#current-status)
- [Roadmap](#roadmap)

## How It Works

```
/kickoff-context     → Collect user meta info (purpose, skill level, time budget)
/kickoff-start       → User idea (free text) → Project type detection
/kickoff-interview   → Planning interview (What) + Design interview (How — skippable)
/kickoff-suggest     → AI idea suggestions (up to 5, with effort estimates)
/kickoff-profile     → project_kickoff.md generation (profile + architecture + data)
/kickoff-evaluate    → Honest evaluation (value + feasibility check) [v1.5]
/kickoff-gap         → Gap/contradiction check (finds issues before development)
/kickoff-checklist   → Dev checklist generation
/kickoff-done        → Definition of Done (measurable completion criteria) [v1.5]
/kickoff-skills      → Base skill setup (7 skills from GitHub)
```

## Technology

| Technology | Role | Why |
|---|---|---|
| Claude Code Skill | Harness engine (orchestrator) | Native integration with Claude CLI, skill chaining |
| Markdown | Output format | Human-readable, version-controllable, universal |
| Git / GitHub | Skill distribution, project sharing | Standard for open-source collaboration |
| gh CLI | Fetch skills from Skill_package repo | Enables selective folder copy without full clone |

## Quick Start

### Prerequisites

- Claude Code CLI installed
- gh CLI installed and authenticated
- Git initialized in target project

### Usage

Run each skill in sequence:

```
/kickoff-context        # (Optional) Collect purpose, skill level, time budget
/kickoff-start          # Input idea + detect project type
/kickoff-interview      # Planning & design interview
/kickoff-suggest        # AI suggests additional ideas
/kickoff-profile        # Generate project_kickoff.md
/kickoff-evaluate       # Honest evaluation (v1.5 — in progress)
/kickoff-gap            # Check for gaps and contradictions
/kickoff-checklist      # Generate dev checklist
/kickoff-done           # Definition of Done (v1.5 — in progress)
/kickoff-skills         # Fetch base skills from GitHub
```

### Output

```
output/{project_name}/{project}_kickoff.md    # Single source of truth
output/{project_name}/kickoff_state.md        # Progress tracking
.claude/skills/*                              # 7 base development skills
```

## Project Structure

```
AI-Project-Kickoff-Harness/
├── .claude/skills/              # Kickoff skills + development skills
│   ├── kickoff-context/         # User context collection (v1.5)
│   ├── kickoff-start/           # Idea input + type detection
│   ├── kickoff-interview/       # Planning & design interview
│   ├── kickoff-suggest/         # AI idea suggestions
│   ├── kickoff-profile/         # Kickoff document generation
│   ├── kickoff-gap/             # Gap/contradiction check
│   ├── kickoff-checklist/       # Dev checklist generation
│   ├── kickoff-skills/          # GitHub skill fetch
│   ├── dev-log/                 # Error/change logging (JSONL)
│   ├── github-push/             # Commit & push automation
│   └── ...                      # Other base skills
├── Phase/                       # Phase-based development docs
│   ├── Phase1~7                 # Core skills (completed)
│   ├── Phase8_kickoff-context.md    # v1.5 — Context-Aware (completed)
│   ├── Phase9_kickoff-evaluate.md   # v1.5 — Honest Evaluation
│   └── Phase10_kickoff-done.md      # v1.5 — Definition of Done
├── output/                      # Generated kickoff documents per project
│   └── hr_data_analytics/       # Integration test output
└── pre-requirement/             # Planning & dogfooding artifacts
    ├── Plan.txt                 # Master plan
    ├── backlog.md               # Improvement backlog
    └── dogfooding_log.md        # 3 rounds of dogfooding record
```

## Development Methodology

This harness was developed using **dogfooding** — it used its own process to plan itself.

- **Round 1**: Applied the harness flow to plan the harness itself. Found 4 design issues (format mismatch, missing steps, unclear structure).
- **Round 2**: Applied the harness to a different project (stock market analysis). Found 3 additional improvements (interview rules, recommendation logic, effort estimates).
- **Round 3**: Full integration test with HR data analytics project. Validated end-to-end flow (start → interview → suggest → profile → gap → checklist). Found 1 bug, 2 gap issues — all resolved.

All 8+ discoveries were immediately reflected in the design. See [pre-requirement/dogfooding_log.md](./pre-requirement/dogfooding_log.md) for full details.

## Documents

| Document | Description |
|---|---|
| [Plan.txt](./pre-requirement/Plan.txt) | Master plan with full flow, rules, and roadmap |
| [dogfooding_log.md](./pre-requirement/dogfooding_log.md) | Dogfooding rounds 1~3 findings and improvements |
| [backlog.md](./pre-requirement/backlog.md) | Improvement backlog with decision rationale |
| [project_profile.md](./pre-requirement/project_profile.md) | Dogfooding round 1 output (harness self-profile) |

## Current Status

| Phase | Status | Deliverable |
|---|---|---|
| Phase 1 — kickoff-start | ✅ Complete | Idea input + project type detection skill |
| Phase 2 — kickoff-interview | ✅ Complete | Planning & design interview skill |
| Phase 3 — kickoff-suggest | ✅ Complete | AI idea suggestion skill |
| Phase 4 — kickoff-profile | ✅ Complete | project_kickoff.md generation skill |
| Phase 5 — kickoff-gap | ✅ Complete | Gap/contradiction check skill |
| Phase 6 — checklist + skills | ✅ Complete | Checklist generation + GitHub skill fetch |
| Phase 7 — integration test | ✅ Complete | End-to-end validation + documentation |
| Phase 8 — kickoff-context | ✅ Complete | Context-aware prompting (v1.5) |
| Phase 9 — kickoff-evaluate | 🔲 Not Started | Honest evaluation layer (v1.5) |
| Phase 10 — kickoff-done | 🔲 Not Started | Definition of Done generation (v1.5) |

## Roadmap

### v1.5 (In Progress)

- ✅ Context-Aware Prompting — collect user purpose/level/time before kickoff
- 🔲 Honest Evaluation Layer — 5+1 dimension project feasibility check
- 🔲 Definition of Done — measurable completion criteria generation
- 🔲 Conditional security evaluation (web/app + external users only)

### v2 (Planned)

- Phase document auto-generation
- Full design document generation (7 types: architecture, data model, requirements, etc.)
- Codex CLI / Gemini CLI support
- Interview termination condition (auto-detect when enough info collected)

---

<p align="center">Made with AI-assisted development</p>
