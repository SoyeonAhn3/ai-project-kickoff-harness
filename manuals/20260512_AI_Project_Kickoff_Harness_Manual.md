# AI Project Kickoff Harness

> A CLI automation harness that transforms vague project ideas into development-ready plans through AI-driven interviews and validation.

| Item | Detail |
|---|---|
| Version | v1.5 (includes v2 design skills) |
| Date | 2026-05-12 |
| Audience | Developers who want structured project planning before coding |

---

## Table of Contents

- [1. Overview](#1-overview)
- [2. Prerequisites](#2-prerequisites)
- [3. Getting Started](#3-getting-started)
- [4. Key Features](#4-key-features)
- [5. Data Storage](#5-data-storage)
- [6. Cautions & Limitations](#6-cautions--limitations)
- [7. Troubleshooting (FAQ)](#7-troubleshooting-faq)

---

## 1. Overview

AI Project Kickoff Harness converts project ideas into a structured kickoff document through **AI-driven interviews**. Built on Claude Code's Skill system, it provides 14 slash commands that — when run in sequence — automatically generate everything from requirements gathering to design documents, all within a single Markdown file.

| Item | Detail |
|---|---|
| Platform | Claude Code CLI (terminal, desktop app, VS Code extension) |
| Output | `{project_name}_kickoff.md` (single source of truth) |
| Languages | Korean / English (selected at kickoff start) |
| Project Types | AI, Automation, BI/Analytics, Pipeline, WebApp, CLI, Library (7 types) |
| Skills | 10 v1 kickoff + 4 v2 design = 14 total |

---

## 2. Prerequisites

- [ ] **Claude Code CLI** installed — see the [official installation guide](https://docs.anthropic.com/en/docs/claude-code)
- [ ] **gh CLI** installed and authenticated (`gh auth login`) — required for `/kickoff-skills` to fetch GitHub skills
- [ ] **Git** initialized — run `git init` in the project directory

---

## 3. Getting Started

1. Navigate to the harness folder
   ```
   cd AI-Project-Kickoff-Harness
   ```
2. Launch Claude Code
   ```
   claude
   ```
3. Start the kickoff with a slash command
   ```
   /kickoff-start
   ```
4. Select your language and describe your project idea freely
5. Run the remaining skills in order (see [4. Key Features](#4-key-features))

### Execution Order

```
[v1 Kickoff — Planning]
/kickoff-context     → (Optional) Collect user background
/kickoff-start       → Idea input + project type detection
/kickoff-interview   → Planning interview + design interview
/kickoff-suggest     → AI idea suggestions
/kickoff-profile     → Final kickoff document review
/kickoff-evaluate    → Honest evaluation
/kickoff-done        → Definition of Done

[v2 Design — Detailed Design (Optional)]
/design-requirements → Requirements definition
/design-architecture → Detailed system architecture
/design-data-model   → Data model
/design-ai-workflow  → AI workflow (AI projects only)

[Wrap-up]
/kickoff-gap         → Gap & contradiction check
/kickoff-checklist   → Development readiness checklist
/kickoff-skills      → Copy base skills to project folder
```

---

## 4. Key Features

### 4.1 kickoff-context — User Context Collection

An optional skill that captures "who are you and why are you building this" before the kickoff begins. The collected context propagates to all subsequent skills, enabling tailored recommendations and evaluations.

| Collected Item | Examples |
|---|---|
| Project purpose | Portfolio / work automation / learning / production |
| Target audience | Hiring manager / team lead / self |
| Current skill level | Beginner–Advanced + specific competencies |
| Target role | Job title or "none" |
| Time budget | Expected development period |
| Differentiation | Keywords |

> ⚠️ **Note:** This skill is optional — skipping it won't break subsequent skills. However, having context improves evaluation and suggestion quality.

---

### 4.2 kickoff-start — Idea Input + Type Detection

Accepts a free-text project idea and automatically classifies it into one of 7 project types (or a composite). Creates the project folder and kickoff document — the entry point of the entire flow.

| Step | Action |
|---|---|
| Language selection | Choose Korean / English (applies to all outputs) |
| Idea input | Free-text description (5+ words) |
| Type detection | Auto-detection via keyword + context analysis, user confirmation |
| Project setup | Set project name and output path (auto-generated if omitted) |
| Document creation | Generate initial `{project_name}_kickoff.md` |

**Supported project types:** AI, Automation, BI/Analytics, Pipeline, WebApp, CLI, Library

---

### 4.3 kickoff-interview — Planning & Design Interview

Collects requirements through structured questions tailored to the project type. Consists of two phases: Planning Interview (What) and Design Interview (How).

| Interview | Content | Skippable |
|---|---|---|
| Planning (What) | Purpose, users, core features, data sources, output format, tech stack, constraints | No |
| Design (How) | Pipeline flow, external dependencies, data structures, failure scenarios | Yes |

- Questions are presented in batches of 3–8 (minimizing user burden)
- "I don't know" / "Recommend something" → AI suggests alternatives immediately
- Different question sets per project type

---

### 4.4 kickoff-suggest — AI Idea Suggestions

Analyzes interview results and suggests up to 5 features or structural improvements the user may not have considered.

| Item | Description |
|---|---|
| Suggestions | Up to 5 |
| Included info | Idea, difficulty, estimated time, MVP suitability |
| User choice | Accept / defer / reject each suggestion |
| On acceptance | Auto-added to "Adopted AI Suggestions" section |

---

### 4.5 kickoff-profile — Final Document Review

Reviews the kickoff document filled by previous skills (start → interview → suggest) for consistency and quality. From this point, the kickoff document becomes the **Single Source of Truth**.

| Review Area | Description |
|---|---|
| Consistency | Check contradictions between type, features, and tech stack |
| Completeness | Identify "TBD" items and missing sections |
| Quality | Verify MVP classification, refine tech stack rationale |

---

### 4.6 kickoff-evaluate — Honest Evaluation

Scores the project across 4+2 dimensions for value and feasibility, providing an objective assessment.

| Dimension | Item | Activation |
|---|---|---|
| Value | Technical growth contribution | Always |
| Value | Practical/business value | Always |
| Value | Differentiation | Always |
| Feasibility | Completion within time budget | Always |
| Conditional | Learning cost efficiency | Portfolio/learning projects |
| Conditional | Security risk | Web/app + external users |

- Each dimension scored 1–5 with rationale
- Improvement suggestions for low-scoring dimensions
- Document cascade update checklist when MVP scope changes

---

### 4.7 kickoff-done — Definition of Done

Generates 5–10 measurable conditions that define when the project is "done."

| Category | Example |
|---|---|
| Core deliverables | "N API endpoints operational" |
| Quality criteria | "Test coverage ≥ 80%" |
| Documentation | "README includes execution instructions" |
| Deployment (conditional) | "Docker image builds successfully" |

---

### 4.8 design-requirements — Requirements Definition (v2)

Analyzes kickoff document sections 1–8 to generate Functional Requirements (FR), Non-Functional Requirements (NFR), and user flows.

| Output | Description |
|---|---|
| FR table | FR-001+ format, derived from core features, with priority |
| NFR table | NFR-001+ format, 7 categories with conditional activation |
| User flows | Primary / alternative / exception flows |
| Gap interview | Up to 5 clarifying questions |

**NFR Categories:** Performance, Security (conditional), Scalability (conditional), Availability (conditional), Maintainability, Compatibility (conditional), Data Quality (conditional)

---

### 4.9 design-architecture — Detailed System Architecture (v2)

Based on section 9 (requirements), generates system structure, tech selection rationale, deployment configuration, and Architecture Decision Records (ADR).

| Output | Description |
|---|---|
| System diagram | Text-based architecture diagram |
| Component table | Role, technology, inputs/outputs |
| Tech selection rationale | Includes comparison alternatives |
| Deployment config | Conditional (production/external only) |
| ADR | Only for decisions involving trade-offs |

---

### 4.10 design-data-model — Data Model (v2)

Generates entity definitions, relationships, integrity rules, data lifecycle, and migration strategy.

| Output | Description |
|---|---|
| Entity definitions | Fields, types, constraints |
| Relationships | 1:N, N:M between entities |
| Integrity rules | Business rules + NFR-based |
| Migration strategy | Conditional (production only) |

---

### 4.11 design-ai-workflow — AI Workflow (v2)

Activated only for AI projects. Generates AI I/O definitions, prompt design, model selection, and fallback strategies. Automatically skipped for non-AI projects.

| Output | Description |
|---|---|
| AI I/O definitions | Input/output format per feature, validation rules |
| Prompt design | System prompt, templates, Temperature |
| Model selection | Including cost estimation |
| Fallback strategy | Alternative actions per failure scenario |
| Evaluation & monitoring | AI quality metrics + targets |

---

### 4.12 kickoff-gap — Gap & Contradiction Check

Scans the entire kickoff document to find missing information, cross-section contradictions, and infeasible combinations.

| Check Category | Description |
|---|---|
| 1. Missing required items | Remaining "TBD" items, empty sections |
| 2. Cross-contradictions | Conflicts between features, constraints, and tech stack |
| 3. Feasibility | Time budget vs. feature scope |
| 4. External dependencies | Accessibility of required services |
| 5. Definition of Done | Mapping between completion criteria and core features |
| 6. Design interview consistency | Internal consistency of sections 2–4 |
| 7. v2 cross-section validation | NFR↔constraints, flows↔architecture, architecture↔data model, v1↔v2 |

---

### 4.13 kickoff-checklist — Development Readiness Checklist

Generates a pre-development checklist based on the kickoff and design documents. When v2 design is complete, also generates a project structure tree and `.env.example`.

| Output | Condition |
|---|---|
| Environment setup checklist | Always |
| Tools/accounts checklist | Always |
| Project structure tree | When v2 design is complete |
| `.env.example` | When v2 design is complete |

---

### 4.14 kickoff-skills — Base Skill Copy

Copies 7 base development skills from the GitHub Skill_package repository into the completed project folder. Uses `gh` CLI for selective copy without full repository cloning.

---

## 5. Data Storage

- **Single file**: All skill outputs accumulate in a single `{project_name}_kickoff.md`
- **YAML frontmatter**: Stores metadata (project name, creation date, language, last executed skill) at the top of the file
  ```yaml
  ---
  project: my_project
  created: 2026-05-12
  language: en
  last_skill: kickoff-done
  ---
  ```
- **Progress tracking**: The `last_skill` field automatically tracks how far the process has progressed
- **Revision History**: v2 design skills log changes to existing sections in a table at the bottom of the document
- **Output path**: `../{project_name}/pre-requirement/{project_name}_kickoff.md` (parent directory of the harness)

---

## 6. Cautions & Limitations

> ⚠️ **Execution order is mandatory**: Each skill verifies that its prerequisite skill has been completed. Skipping ahead will prompt you to run the prerequisite first.

> ⚠️ **Manual editing caution**: Changing section header format (`## N. Title`) may cause parsing failures in subsequent skills. Content can be freely edited, but preserve the header format.

> ⚠️ **v2 design skills are optional**: Development can begin after v1 kickoff alone (start–done). v2 design skills (requirements–ai-workflow) are only needed when detailed design is required.

> ⚠️ **gh CLI authentication required**: Complete `gh auth login` before running `/kickoff-skills`. Without authentication, skill copying will fail.

> ⚠️ **Session continuity recommended**: Running multiple skills within a single Claude Code session is recommended. If the session changes, the kickoff document must be re-read, though `last_skill` enables automatic state recovery.

---

## 7. Troubleshooting (FAQ)

**Q. I get an error saying the kickoff document cannot be found.**
A. Skills search for files matching the `**/*_kickoff.md` pattern. Run `/kickoff-start` first to create the document, or verify the filename ends with `_kickoff.md`.

**Q. I'm told to "run the prerequisite skill first."**
A. Progress is tracked via the `last_skill` field in the YAML frontmatter. Run the indicated prerequisite skill to proceed.

**Q. I want to regenerate an already-completed section.**
A. Re-running the corresponding skill will prompt "Overwrite or edit?" Choose overwrite to regenerate that section from scratch.

**Q. The project type was detected incorrectly.**
A. At STEP 3 of `/kickoff-start`, respond with "no" and specify the correct type directly.

**Q. Can I start development without the v2 design skills?**
A. Yes. After `/kickoff-done`, run `/kickoff-gap` → `/kickoff-checklist` → `/kickoff-skills` to generate the checklist and skills without v2 design.

**Q. I want to proceed in Korean.**
A. When running `/kickoff-start`, select "1. 한국어" at the language selection prompt. All subsequent outputs and questions will be in Korean.

---

> This manual was auto-generated on 2026-05-12.
