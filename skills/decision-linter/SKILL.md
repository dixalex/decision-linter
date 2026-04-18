---
name: decision-linter
description: "Decision linter — like ESLint for your thinking. Scores assumptions as Kind (trust gut) or Wicked (impose structure), runs consider-the-opposite, surfaces blind spots, outputs a paste-ready judgment memo. Use BEFORE committing to any consequential decision: architecture choices, technology selection, product direction, client proposals, estimates, pricing, hiring, or any 'point of no return.' Also use when the user says 'lint this decision', 'decision check', 'check my assumptions', 'is this the right call', 'should I do this', 'am I missing something', 'sanity check', or dumps a document/spec/proposal for review. Auto-triggers when you detect the user is about to commit to a direction with high stakes and limited reversibility. Do NOT use for trivial or easily reversible choices (variable names, minor refactors, lunch), personal relationship advice, hypothetical scenarios without real stakes, or decisions already shipped and irreversible."
---

# /decision-linter — Lint Your Decisions Before They Ship

A 2-minute judgment check before consequential decisions. Like a linter for thinking — catches assumption bugs before they ship.

## Iron Law

**NO COMMITMENT WITHOUT EVIDENCE.** Confidence is not evidence. "I already know the answer" is the red flag, not the green light.

## Red Flags — If You Catch the User Thinking These, STOP

- "I already know the answer" → Einstellung effect — experience is blocking alternatives
- "This is obvious" → Most consequential mistakes feel obvious in retrospect
- "We can always change it later" → Deferred-decision trap. Can you, really? At what cost?
- "Everyone agrees" → Groupthink. Has anyone been ASKED to argue the opposite?
- "I've seen this before" → False recognition — looks familiar but might not be. What's DIFFERENT?

## Process

### Step 1: Extract Decisions

If the user provides a single decision, proceed to Step 2.

If the user dumps a document, spec, proposal, or multi-part plan — **decompose first**:
- Scan for distinct decision points (architecture choices, technology picks, scope commitments, timeline promises, pricing, feature cuts)
- Present as a numbered list: "I see N decisions embedded here:"
- Ask: "Which feel most consequential? Or check all?"
- Process each through Steps 2-5 independently
- Aggregate into one judgment memo at the end

### Step 2: Score the Environment (Kind vs Wicked)

For each decision, score 5 dimensions (1-5):

| Dimension | 1 (Wicked) | 3 (Mixed) | 5 (Kind) |
|---|---|---|---|
| **Feedback speed** | Months/years | Weeks | Hours/days |
| **Signal accuracy** | Ambiguous, confounded | Noisy but directional | Clear pass/fail |
| **Pattern stability** | Shifting, unprecedented | Some precedent, some novelty | Repeating, stable |
| **Outcome visibility** | Only successes visible | Partial picture | Full picture |
| **Causal clarity** | Many variables | Some confounders | Direct link |

Score each dimension 1-5. Use the midpoint (3) as anchor — most real decisions land there, not at the extremes.

**Scoring thresholds:**
- **20-25: KIND** → Output a brief memo (score + key assumption + verdict). Skip Steps 3-4. Don't create friction where it isn't needed.
- **15-19: MIXED** → Full memo with counter-cases. Continue to Step 3.
- **5-14: WICKED** → Full memo, no shortcuts. Continue to Step 3. This is where the check earns its keep.
- **Threshold ties (exactly 15 or 20):** Round toward WICKED. When in doubt, check.

### Step 3: Consider-the-Opposite

The only debiasing technique proven to work on experienced professionals (19% improvement in field decisions, RCT).

Ask: **"What would have to be true for this to be WRONG?"**

Generate 2-3 specific counter-cases. Not vague — specific:
- "If [specific condition], then this decision leads to [specific bad outcome]"
- "The assumption that [X] breaks if [Y] happens"
- "This looks like [past pattern] but differs in [specific way] that could matter"

### Step 4: Surface Blind Spots

Two questions:

**"What is MISSING from your experience here?"**
- Base rates (how often does this type of decision go wrong for teams like yours?)
- Counterfactuals (what happened to teams that chose differently?)
- Outcomes you weren't around for (survivorship bias)

**"What is IRRELEVANT but feels important?"**
- Surface similarity to past projects
- Emotionally salient details (the loud stakeholder, the recent crisis)
- Sunk costs (time already spent on this direction)

### Step 5: Output Judgment Memo

Format as a paste-ready memo:

```
## Judgment Check: [decision name]

**Environment:** [KIND/MIXED/WICKED] (score X/25)
[One-line explanation of why]

**Key assumption:** [the assumption this decision rests on]
**If wrong:** [what happens — specific, not vague]

**Counter-cases:**
- [strongest argument AGAINST this decision]
- [second counter-case, if exists]

**Missing:** [what's absent from the evidence base]
**Irrelevant noise:** [what feels important but isn't]

**Verdict:**
- ✅ PROCEED — kind environment, evidence supports it
- ⚠️ PROCEED WITH STRUCTURE — name the assumption, set a check-in, define "wrong"
- 🔴 PAUSE — wicked environment, key assumption untested. Before committing: [action]
```

For multi-decision documents, output one memo per decision, then a summary table:

```
| # | Decision | Score | Verdict | Key Risk |
|---|----------|-------|---------|----------|
| 1 | [name]   | 18/25 | ⚠️      | [risk]   |
| 2 | [name]   | 9/25  | 🔴      | [risk]   |
| 3 | [name]   | 22/25 | ✅      | —        |
```

## Guidelines

- **Fast on kind, thorough on wicked.** Score ≥20 → brief memo (skip counter-cases and blind spots). Score ≤14 → full check. Don't waste time on safe decisions.
- **Name specifics, not categories.** "The market might change" = useless. "If competitor X ships Y before Q3, your positioning breaks" = useful.
- **The memo is the deliverable.** Paste-able into a PR, Slack, proposal doc, or decision log.
- **Don't lecture on theory.** No Kahneman history, no cognitive bias taxonomy. Just run the check.
- **Rushing = the signal.** "I don't have time for this" is the moment the check matters most.
- **Don't show your work — the memo IS the work.** Output the judgment memo directly. Don't narrate through Steps 2-4 before the memo — the scoring table, counter-cases, and blind spots are already IN the memo. Showing the steps then repeating them in the memo doubles length for zero value.
- **For multi-decision docs: summary table FIRST.** Busy readers skip to the verdict. Lead with the table, then expand only the WICKED/MIXED decisions. Collapse causally-dependent decisions — if the primary decision pauses, downstream decisions are moot. Don't write 5 full memos when 2 memos + a footnote would do.
- **Target length:** Single decision → under 300 words. Multi-decision document → summary table + expanded memos for wicked decisions only.
- **Emojis are optional.** Omit ✅/⚠️/🔴 if the output goes into a formal document. Use PROCEED/STRUCTURE/PAUSE labels instead.

## Edge Cases

- **User doesn't answer decomposition question:** Process all detected decisions. Prioritize by reversibility (hardest to reverse first).
- **Can't generate counter-cases:** Output what exists, note: "No strong counter-case found — which itself may be a blind spot. Consider: what would a skeptic ask?"
- **Scoring feels ambiguous:** Default to the lower score. "When in doubt, it's wicked."
- **Decision already shipped:** Don't lint. Say: "This decision is already in effect. A post-mortem would be more useful than a pre-mortem."
- **More than 8 decisions in one document:** Confirm with user before proceeding. Suggest: "Focus on the 3-4 with highest irreversibility."
