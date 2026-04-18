# Decision Linter

Like ESLint for your thinking. A 2-minute judgment check before consequential decisions.

## What it does

- Scores assumptions as **Kind** (trust gut) or **Wicked** (impose structure) on 5 dimensions
- Runs **consider-the-opposite** — the only debiasing technique proven on experienced professionals
- Surfaces blind spots: what's missing from your experience, what's irrelevant but feels important
- Outputs a **paste-ready judgment memo** for PRs, Slack, proposals, or decision logs
- Decomposes multi-decision documents into individual checks with a summary table

## When it triggers

- Before architecture choices, technology selection, product direction
- Before client proposals, estimates, pricing decisions
- When you say "should I do this?", "check my assumptions", "sanity check this"
- When you dump a spec or proposal for review

## Install as Claude Code Plugin

```
/plugin marketplace add dixalex/decision-linter
/plugin install decision-linter@decision-linter
```

Then use it:
```
/decision-linter should we rewrite our monolith in microservices?
```

Or just describe a decision naturally — it auto-triggers when it detects high-stakes, low-reversibility choices.

## Based on

Cognitive science research: Kahneman-Klein (conditions for intuitive expertise), Hogarth (kind vs wicked environments), Tetlock (superforecasting), Morewedge (debiasing interventions).
