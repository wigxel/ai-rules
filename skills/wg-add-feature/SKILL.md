---
name: add-feature
description: Turn a feature request into a beads issue — grill the requirements, then create the bead with an optional waiting-on-user label and wire dependencies. Use when the user asks to add a feature, create a bead for a feature, or invokes /add-feature.
triggers:
  - phrase: "/add-feature"
  - phrase: "add a feature"
  - phrase: "new feature"
  - phrase: "create a bead"
---

# Add Feature

Turn a feature request into a beads issue. Nothing more — no implementation, no
branches, no gates, no PRs. This skill ends when the bead exists and its
dependencies are wired.

## 1. Check for beads

Run `bd list`. If `bd` is missing, fails, or the repo has no beads
initialized, stop:

> This repo has no beads task tracking, so there is nowhere to record the
> feature. Run `bd init` (or ask me) if you want to set it up — no bead was
> created.

Do not fall back to a markdown TODO or any other tracker.

## 2. Grill the requirements

Before anything is created, load the `grilling` skill and interview the user
about the feature: what it does, what it is explicitly *not*, who/what it
touches, and how success is verified. Follow `grilling`'s design-tree rounds —
numbered questions with recommended answers, recomputing the frontier each
round — until nothing is silently assumed.

`grilling` ends only when the user confirms shared understanding. That
confirmation is the gate: no bead until they say so.

## 3. Ask about the label, then create

Once requirements are settled, ask the user one question:

> Tag it `waiting-on-user`? (the repo convention — it means planned and
> waiting on you to green-light)

Recommended: yes. If yes, create with the label; if no, create without it:

```bash
bd create "<title>" --type feature --label waiting-on-user
# or, label declined:
bd create "<title>" --type feature
```

- `<title>` — one line distilled from the grilled requirements.
- Description — the settled requirements, verbatim enough that a future
  session can implement without re-interviewing the user. The distilled
  decisions, not the question transcript.
- Priority — only set it if the user stated one during grilling; never invent
  one.

## 4. Link it

Show every open issue in one flat list — epics and regular tasks together,
each with its id and title:

```bash
bd list --status open
```

Then ask: "which of these should the new bead depend on? (pick any, or
none)". Never pre-select, recommend, or choose one yourself — list, ask, wait.

For each picked task, verify the arrow direction once with `bd dep --help`
(conventions drift between bd versions) and wire it:

```bash
bd dep add <new-bead> <picked-id>   # new depends on picked
```

If a picked issue is an epic, wire it as the parent instead — epics don't
block:

```bash
bd update <new-bead> --parent <epic-id>
```

If the user says none, leave the bead standalone.

Report the new bead id, its links, and stop.
