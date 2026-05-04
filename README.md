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
User idea (free text)
  → Project type detection
  → Planning interview (What to build)
  → Design interview (How to build — skippable)
  → AI idea suggestions (up to 5, with effort estimates)
  → project_kickoff.md generation (profile + architecture + data structure)
  → Gap/contradiction check (finds issues before development)
  → Dev checklist generation
  → Base skill setup (7 skills from GitHub)
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
/kickoff-start          # Input idea + detect project type
/kickoff-interview      # Planning & design interview
/kickoff-suggest        # AI suggests additional ideas
/kickoff-profile        # Generate project_kickoff.md
/kickoff-gap            # Check for gaps and contradictions
/kickoff-checklist      # Generate dev checklist
/kickoff-skills         # Fetch base skills from GitHub
```

### Output

```
pre-requirement/project_kickoff.md    # Single source of truth
.claude/skills/*                      # 7 base development skills
```

## Project Structure

```
AI-Project-Kickoff-Harness/
├── .claude/skills/          # Development skills (base 7 + kickoff skills)
│   ├── dev-log/             # Error/change logging (JSONL)
│   ├── gen-manual/          # Manual generation
│   ├── github-push/         # Commit & push automation
│   ├── phase-doc/           # Phase document management
│   ├── readme-gen/          # README generation
│   ├── skill-template/      # Skill creation template
│   └── test-scenario/       # Test scenario generation
├── Phase/                   # Phase-based development docs
│   ├── Phase1_kickoff-start.md
│   ├── Phase2_kickoff-interview.md
│   ├── Phase3_kickoff-suggest.md
│   ├── Phase4_kickoff-profile.md
│   ├── Phase5_kickoff-gap.md
│   ├── Phase6_checklist-skills.md
│   └── Phase7_integration-test.md
└── pre-requirement/         # Planning & dogfooding artifacts
    ├── Plan.txt             # Master plan (updated through dogfooding)
    ├── project_profile.md   # Dogfooding round 1 output
    ├── gap_report.md        # Dogfooding round 1 output
    ├── dev_checklist.md     # Dogfooding round 1 output
    └── dogfooding_log.md    # Dogfooding process record
```

## Development Methodology

This harness was developed using **dogfooding** — it used its own process to plan itself.

- **Round 1**: Applied the harness flow to plan the harness itself. Found 4 design issues (format mismatch, missing steps, unclear structure).
- **Round 2**: Applied the harness to a different project (stock market analysis). Found 3 additional improvements (interview rules, recommendation logic, effort estimates).

All 7 discoveries were immediately reflected in the design. See [pre-requirement/dogfooding_log.md](./pre-requirement/dogfooding_log.md) for full details.

## Documents

| Document | Description |
|---|---|
| [Plan.txt](./pre-requirement/Plan.txt) | Master plan with full flow, rules, and roadmap |
| [dogfooding_log.md](./pre-requirement/dogfooding_log.md) | Dogfooding rounds 1 & 2 findings and improvements |
| [project_profile.md](./pre-requirement/project_profile.md) | Dogfooding round 1 output (harness self-profile) |
| [gap_report.md](./pre-requirement/gap_report.md) | Dogfooding round 1 gap analysis |
| [dev_checklist.md](./pre-requirement/dev_checklist.md) | Dogfooding round 1 dev checklist |

## Current Status

| Phase | Status | Deliverable |
|---|---|---|
| Phase 1 — kickoff-start | 🔲 Not Started | Idea input + project type detection skill |
| Phase 2 — kickoff-interview | 🔲 Not Started | Planning & design interview skill |
| Phase 3 — kickoff-suggest | 🔲 Not Started | AI idea suggestion skill |
| Phase 4 — kickoff-profile | 🔲 Not Started | project_kickoff.md generation skill |
| Phase 5 — kickoff-gap | 🔲 Not Started | Gap/contradiction check skill |
| Phase 6 — checklist + skills | 🔲 Not Started | Checklist generation + GitHub skill fetch |
| Phase 7 — integration test | 🔲 Not Started | End-to-end validation + documentation |

## Roadmap

### v2 (Planned)

- Phase document auto-generation
- Full design document generation (7 types: architecture, data model, requirements, etc.)
- Codex CLI / Gemini CLI support
- README auto-generation via readme-gen skill
- Interview termination condition (auto-detect when enough info collected)
- Project type-specific question templates

---

<p align="center">Made with AI-assisted development</p>
