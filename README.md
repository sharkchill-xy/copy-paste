---
name: Manage Project Long-Term Progress
description: Maintain long-term project continuity through README, changelog, ADRs, worklogs, current-status docs, and Claude-facing rules.
---

# Manage Project Long-Term Progress

## Purpose

Use this skill when working on a project that spans many sessions and needs durable documentation of:

- what the project is
- what changed
- why key decisions were made
- what happened in each work session
- what the current state is
- how Claude should continue contributing consistently

This skill is for building and maintaining a **project knowledge system**, not just a codebase.

The goal is to preserve continuity for:
- the future human maintainer
- the current operator
- collaborators
- Claude across sessions

---

## Core Principle

Do **not** put everything into memory.

Instead, organize long-term project knowledge into layers:

- `README.md` → what the project is and how to start
- `CHANGELOG.md` → version-level user-visible changes
- `docs/decisions/` → why important decisions were made
- `docs/worklog/` → what happened in each session
- `docs/plans/now.md` → current focus, blockers, next steps
- `.claude/CLAUDE.md` → stable collaboration rules for Claude
- memory → only long-lived reusable patterns, not full session history

A good rule:

- **process** goes to worklog
- **reasoning** goes to ADRs
- **release-impact** goes to changelog
- **current direction** goes to `now.md`
- **stable operating rules** go to `CLAUDE.md`

---

## Recommended Documentation Tree

Use this structure unless the project already has a better established system:

```text
project/
├── README.md
├── CHANGELOG.md
├── CONTRIBUTING.md
├── docs/
│   ├── architecture/
│   │   └── overview.md
│   ├── decisions/
│   │   ├── README.md
│   │   ├── ADR-0001-...
│   │   └── ADR-0002-...
│   ├── plans/
│   │   ├── roadmap.md
│   │   ├── milestones.md
│   │   └── now.md
│   ├── worklog/
│   │   └── 2026/
│   │       ├── 2026-04-08-session.md
│   │       └── 2026-04-10-session.md
│   ├── specs/
│   └── runbooks/
└── .claude/
    ├── CLAUDE.md
    ├── rules/
    │   ├── docs.md
    │   ├── testing.md
    │   └── commits.md
    └── skills/
````

If the repository is small, start with the minimum viable set:

```text
README.md
CHANGELOG.md
docs/decisions/
docs/worklog/
docs/plans/now.md
.claude/CLAUDE.md
```

---

## Responsibilities of Each File

### `README.md`

Use for:

* project purpose
* problem being solved
* quick start
* repo map
* doc map

Do not use it as a running diary.

### `CHANGELOG.md`

Use for:

* user-visible changes
* release notes
* meaningful additions, changes, fixes, removals

Do not dump raw commit history into it.

### `docs/decisions/ADR-xxxx-*.md`

Use for:

* important architectural decisions
* trade-offs
* reasons behind major changes
* long-term consequences

Write an ADR when future you might ask:
**“Why did we choose this?”**

### `docs/worklog/YYYY/YYYY-MM-DD-session.md`

Use for:

* session goals
* what was done
* findings
* decisions made during the session
* blockers
* next steps

This is the operational history of the project.

### `docs/plans/now.md`

Use for:

* current focus
* active blockers
* immediate next steps
* short horizon status

This is the handoff file for the next session.

### `.claude/CLAUDE.md`

Use for:

* stable collaboration rules
* document maintenance expectations
* how Claude should behave in this repo
* where to look before making changes

Keep it short, actionable, and stable.

### Memory

Use only for:

* long-term reusable patterns
* recurring project constraints
* learned preferences
* repeated gotchas

Do not store full session logs in memory.

---

## Standard Operating Workflow

Whenever contributing to a long-running project, follow this order.

### 1. Understand the current state

Before making substantial changes, read:

* `README.md`
* `docs/plans/now.md`
* recent files in `docs/worklog/`
* relevant ADRs in `docs/decisions/`
* `.claude/CLAUDE.md`

This prevents re-solving already-settled questions.

### 2. Do the work

Complete the requested coding, design, refactoring, debugging, or planning task.

### 3. Decide what must be documented

After the work is done, classify the outcome:

* Was there a **major decision**? → write/update an ADR
* Was there a **session worth preserving**? → update worklog
* Did the **current status** change? → update `now.md`
* Was there a **user-visible change**? → update changelog
* Did the **collaboration rules** change? → update `CLAUDE.md`

### 4. Leave the project in a resumable state

At the end of the session, make sure the next contributor can answer:

* What was attempted?
* What was completed?
* What remains?
* What are the current risks?
* What should happen next?

If these are not obvious, update `docs/worklog/...` and `docs/plans/now.md`.

---

## Documentation Decision Rules

Use these rules to determine where information belongs.

### Put information in `worklog` when:

* it happened in this session
* it explains progress over time
* it captures findings, experiments, blockers, or next steps
* it may help continue work later

### Put information in an ADR when:

* the decision changes architecture, process, boundaries, or dependencies
* alternatives were considered
* there are real trade-offs
* future maintainers will need the reasoning

### Put information in `CHANGELOG.md` when:

* a release note or user-facing summary would mention it
* behavior changed in a meaningful way
* a feature, fix, removal, or breaking change occurred

### Put information in `now.md` when:

* it affects the next session
* it changes current priorities
* it introduces or removes a blocker
* it changes what is most important right now

### Put information in `.claude/CLAUDE.md` when:

* it is a stable instruction for future Claude sessions
* it should be followed regularly
* it applies across multiple tasks

### Put information in memory when:

* it is likely to be useful repeatedly
* it is not just a one-off event
* it is short enough to remain durable and clear

---

## Writing Standards

When updating any project progress docs:

* prefer short sections and bullets over long prose
* write facts first, interpretation second
* make decisions explicit
* distinguish completed work from planned work
* distinguish local experiments from accepted project direction
* avoid vague language such as “cleaned things up” or “improved architecture”
* include references to related files, modules, or tickets where useful

Good:

* “Split token validation from session creation to prepare for SSO integration.”

Bad:

* “Refactored auth stuff.”

Good:

* “Blocked by admin portal dependency on legacy session shape.”

Bad:

* “There were some compatibility issues.”

---

## Templates

## Template: `docs/plans/now.md`

```md
# Now

## Current Focus
[What is the project actively trying to complete?]

## Why This Matters
[Why this work is the current priority]

## Active Blockers
- [blocker 1]
- [blocker 2]

## Current Risks
- [risk 1]
- [risk 2]

## Next 3 Steps
1. ...
2. ...
3. ...

## Related Docs
- [link]
- [link]
```

---

## Template: session worklog

Path example:

```text
docs/worklog/2026/2026-04-08-session.md
```

Template:

```md
# Session Log — 2026-04-08

## Goal
[What was the intended goal of this session?]

## Done
- ...
- ...
- ...

## Findings
- ...
- ...
- ...

## Decisions
- ...
- ...
- ...

## Blockers
- ...
- ...

## Next
- ...
- ...
```

---

## Template: ADR

Path example:

```text
docs/decisions/ADR-0003-separate-token-validation.md
```

Template:

```md
# ADR-0003: [Title]

## Status
Accepted

## Context
[What situation created the need for this decision?]

## Decision
[What was decided?]

## Alternatives Considered
1. ...
2. ...
3. ...

## Consequences

### Positive
- ...
- ...

### Negative
- ...
- ...

## References
- ...
- ...
```

---

## Template: `CHANGELOG.md`

```md
# Changelog

## [Unreleased]

### Added
- ...

### Changed
- ...

### Fixed
- ...

### Removed
- ...

## [0.1.0] - YYYY-MM-DD

### Added
- Initial release.
```

---

## Template: `.claude/CLAUDE.md`

```md
# Claude Collaboration Rules

## Before Working
- Read `docs/plans/now.md` before making substantial changes.
- Check relevant ADRs in `docs/decisions/` for settled architectural choices.
- Review recent `docs/worklog/` entries when continuing existing work.

## Documentation Rules
- Update `docs/worklog/` after any substantial multi-step session.
- Update `docs/plans/now.md` when priorities, blockers, or next steps change.
- Create an ADR for decisions with long-term architectural or workflow impact.
- Update `CHANGELOG.md` only for meaningful user-visible changes.

## Working Style
- Prefer minimal diffs over broad refactors unless refactoring is the explicit goal.
- Make reasoning explicit when changing architecture or interfaces.
- Leave the project in a resumable state at the end of the session.
```

---

## Commit Message Guidance

Commit messages should describe the specific change.
Use the body to explain why when helpful.

Recommended format:

```text
type(scope): short summary

Why:
- ...
- ...

Refs:
- ADR-0003
- docs/worklog/2026/2026-04-08-session.md
```

Examples of `type`:

* `feat`
* `fix`
* `refactor`
* `docs`
* `test`
* `chore`

Do not use the commit message as a substitute for an ADR or a worklog.

---

## End-of-Session Checklist

Before ending a substantial session, check:

* [ ] Is the current state reflected in `docs/plans/now.md`?
* [ ] Was a meaningful session recorded in `docs/worklog/`?
* [ ] Did any major decision require an ADR?
* [ ] Did any user-visible behavior change require changelog updates?
* [ ] Are Claude’s future instructions still accurate in `.claude/CLAUDE.md`?
* [ ] Can another person resume the work without reading the whole codebase?

If not, update the relevant docs.

---

## Heuristics for Good Long-Term Project Documentation

A project knowledge system is working well when:

* a new contributor can get oriented quickly
* a returning contributor can resume work in minutes
* important decisions are not lost in chat or commit history
* current priorities are visible without reading many files
* Claude can continue work consistently across sessions
* documentation grows by purpose, not by chaos

---

## Anti-Patterns

Avoid these mistakes:

### 1. Putting everything into memory

Memory should not become a full project archive.

### 2. Turning README into a dumping ground

README is an entrypoint, not the complete history.

### 3. Using changelog as a development diary

Changelog is for meaningful change summaries, not session-by-session notes.

### 4. Hiding decision logic in commit messages only

Commits are too granular and too fragmented to replace ADRs.

### 5. Letting `now.md` drift out of date

If `now.md` is stale, the handoff path breaks.

### 6. Writing vague notes

Every entry should help someone decide what to do next.

---

## When to Suggest Creating Missing Files

If the project lacks long-term continuity structure, suggest creating:

* `docs/plans/now.md`
* `docs/worklog/`
* `docs/decisions/`
* `.claude/CLAUDE.md`

If the repo already has similar files, prefer extending the existing system instead of introducing duplicates.

---

## Default Behavior When Asked to “Document Progress”

When a user asks to document project progress:

1. summarize what changed in the current session
2. identify whether any major decisions occurred
3. update or propose:

   * worklog entry
   * `now.md`
   * ADR if needed
   * changelog if needed
4. ensure the project is resumable from docs alone

---

## Summary

This skill treats project continuity as a system with distinct layers:

* **README** for orientation
* **CHANGELOG** for versioned results
* **ADR** for reasons
* **WORKLOG** for session progress
* **NOW** for handoff state
* **CLAUDE.md** for collaboration rules
* **memory** for durable reusable patterns

The desired outcome is simple:

**Anyone — including future Claude — should be able to understand where the project is, why it got there, and what should happen next.**
