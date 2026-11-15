# lean-website-kickoff

A token-efficient agent skill for kicking off professional website projects: brief → design research → plan → build → verify. It keeps the full workflow's quality bar (free resources only, no AI slop, check-ins after phases 1, 4 and 6) while cutting token use.

## How it saves tokens

- **Fresh chat per phase.** Each phase writes a file (`concepts_brief.md`, `research/DESIGN_RESEARCH.md`, `design_draft.md`). The next phase starts in a new chat with only those files attached.
- **Text before screenshots.** Sites are read as text, with their computed styles. Each site gets at most two screenshots.
- **Design rules cached once.** Rules from the GitHub repos go into `research/DESIGN_RULES.md`, which later projects reuse.
- **Smaller research set.** 6 reference sites instead of 10+, and one fresh-context reviewer per gate.
- **Lazy loading and short updates.** Skills load only when their phase starts, files change by targeted edits, and progress updates are one line each.
- **Asks before installing.** Tools are never installed automatically.

## Install

Copy `skills/lean-website-kickoff/` into your agent's skills folder. For Claude Code, that's:

```bash
mkdir -p ~/.claude/skills
cp -r skills/lean-website-kickoff ~/.claude/skills/
```

Then start a session with: "Use lean-website-kickoff for a new website."
