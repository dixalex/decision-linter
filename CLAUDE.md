# Decision Linter — AI Skill for Pre-Commitment Judgment Checks

## What This Is

A Claude Code skill that runs a structured judgment check before consequential decisions. Scores the decision environment as Kind (trust gut) or Wicked (impose structure), runs consider-the-opposite debiasing, surfaces blind spots, and outputs a paste-ready judgment memo.

Based on: Kahneman-Klein (conditions for intuitive expertise), Hogarth (kind vs wicked environments), Tetlock (superforecasting), Morewedge (debiasing interventions).

## Installation

```
/plugin marketplace add dixalex/decision-linter
```

Or place `skills/decision-linter/` in your `.claude/skills/` folder.

## Dependencies

**None.** This skill uses only Claude's reasoning — no external tools, MCP servers, or plugins required.

## Usage

Invoke with `/decision-linter` or naturally: "check my assumptions", "lint this decision", "sanity check this proposal".

The skill also auto-triggers when it detects you're about to commit to a high-stakes, low-reversibility direction.

## Output

Produces a paste-ready judgment memo (under 300 words) suitable for PRs, Slack, proposals, or decision logs.
