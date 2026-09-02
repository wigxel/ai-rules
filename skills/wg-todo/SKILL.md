---
name: todo-scan
description: Scan codebase for TODO/FIXME comments and sync with beads tracker
---

# TODO Scanner

Find and track TODO annotations across the codebase using beads.

## Keywords

Scan for (case-insensitive):
- `TODO` / `to-do` / `to do`
- `FIXME` / `fix-me`
- `HACK`
- `XXX`
- `BUG`
- `DEPRECATED`

Exclude `node_modules/`, `.git/`, and generated files.

## Workflow

1. **Search** — Use any file search tool (Grep, Glob, ripgrep, IDE search) to find matches.
2. **Deduplicate** — Check existing beads before adding:
   ```bash
   bd todo list
   bd search "<keyword>"
   ```
   Skip anything that already exists.
3. **Add** — For each new TODO:
   ```bash
   bd todo add "<title>"
   bd tag <id> "source:<file>:<line>"
   ```
4. **Close** — When a TODO is addressed:
   ```bash
   bd todo done <id>
   ```
