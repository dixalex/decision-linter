# Decision Linter

**Like ESLint for your thinking.** A 2-minute judgment check before consequential decisions.

> *"$15K for three simultaneous migrations of a production e-commerce platform is not a budget — it's a deposit."*
> — Decision Linter output on a Q3 plan

## Who this is for

**Solo founders and indie hackers** — You're the CTO, PM, and designer. Every decision is yours. No one pushes back when your gut is wrong. This is your pushback.

**Small team tech leads (2-8 engineers)** — You make architecture calls that won't show consequences for months. Your team trusts your judgment, which means your blind spots become the team's blind spots.

**Agency founders and freelancers** — You scope projects, choose stacks, and commit timelines for clients. A bad call costs the client, then costs you the relationship.

**Senior engineers moving into leadership** — You've been promoted for technical skills, but now the decisions are about people, products, and priorities — where engineering instincts can mislead you.

**PMs and QAs making product bets** — Feature prioritization, scope decisions, shipping with known risks — judgment calls where data is always incomplete.

## Quick Start

```
/plugin marketplace add dixalex/decision-linter
/plugin install decision-linter@decision-linter
```

Then:
```
/decision-linter should we rewrite our API in Rust?
```

Or describe any decision naturally — it auto-triggers when it detects high-stakes, low-reversibility choices.

## What it does

- **Scores assumptions** as Kind (trust gut) or Wicked (impose structure) on 5 dimensions
- **Runs consider-the-opposite** — the only debiasing technique proven on experienced professionals
- **Surfaces blind spots** — what's missing from your experience, what's irrelevant but feels important
- **Outputs a paste-ready memo** for PRs, Slack, proposals, or decision logs
- **Decomposes documents** — dump a spec or plan and it checks each decision independently

## Examples

### "Rewrite our Node.js API in Rust"

> Our Node.js API handles 2,000 req/s. The team wants to rewrite it in Rust for better performance. We have 4 engineers, none with Rust experience. Timeline: 3 months.

**Output:**

> **Environment:** WICKED (8/25)
>
> **Key assumption:** 4 engineers with zero Rust experience can reach production-quality proficiency within 3 months while delivering a correct, performant rewrite of a 2,000 req/s system.
>
> **If wrong:** The rewrite ships late or not at all. The Node.js system sits unmaintained during the rewrite window. The team ships something that performs worse than Node.js because they don't yet know how to write idiomatic Rust.
>
> **Counter-case:** 2,000 req/s is not a performance problem. Node.js handles 10,000+ req/s trivially for I/O-bound workloads. If the bottleneck is real, it's almost certainly in the database, external calls, or architecture — not the runtime. Rust won't fix a slow query.
>
> **Missing:** Profiling data showing where the actual bottleneck is. Base rate on team rewrites (Joel Spolsky's "Things You Should Never Do"). What happens to the Node.js system during the 3-month rewrite window.
>
> **Irrelevant noise:** "Rust is faster than Node" — true in benchmarks, irrelevant without proof the runtime is the bottleneck. Team excitement about learning Rust (emotionally salient, not a business case).
>
> **Verdict:** PAUSE — Before committing: (1) Profile the current system. (2) Define what "better performance" means — what metric, what target. (3) If Rust is still the answer, pilot on one isolated service, not a full rewrite.

---

### "Launch MVP without tests — app handles payments"

> We're launching our MVP on Monday. We have no automated tests. The founder says "we'll add tests after launch." The app handles user payments.

**Output:**

> **Environment:** WICKED (7/25)
>
> **Key assumption:** The payment flows work correctly and will continue to work correctly after future changes, without any automated verification.
>
> **If wrong:** A user gets double-charged, a payment goes through without fulfillment, a refund path is broken. At minimum: chargebacks and lost trust. At worst: regulatory exposure, account suspension by the payment processor.
>
> **Counter-case:** "Moving fast" is not free in payment systems — it transfers the cost to users. Stripe holds merchants liable for disputed charges. "Add tests after launch" has a near-zero completion rate in practice: post-launch pressure to add features is always higher than the pressure to test what already appears to work.
>
> **Missing:** Base rate on "tests after launch" actually getting written (industry evidence is grim). Whether the payment processor has testing requirements that activate at launch volume.
>
> **Irrelevant noise:** "We need to move fast" — no one has calculated what a single payment incident costs vs. 2 days of writing happy-path integration tests. The MVP framing — payments are not an MVP feature that can be "good enough for now."
>
> **Verdict:** PAUSE — Before committing: (1) Write integration tests for 2 paths only: successful payment + declined card. This is 4-8 hours, not a sprint. (2) If Monday is non-negotiable: launch to invite-only 5-10 users where you can monitor every transaction manually.

---

### Multi-decision: "Q3 Plan" document dump

> Q3 Plan: Switch from PostgreSQL to MongoDB because it's more flexible. Drop REST for GraphQL. Move from AWS to GCP because one engineer prefers it. Budget: $15K. Team: 3 developers.

**Output — summary table first:**

> | # | Decision | Score | Verdict | Key Risk |
> |---|----------|-------|---------|----------|
> | 1 | PostgreSQL → MongoDB | 8/25 | PAUSE | "More flexible" is not a problem statement |
> | 2 | REST → GraphQL | 12/25 | PAUSE | 3-dev team absorbing N+1, caching complexity alongside two other migrations |
> | 3 | AWS → GCP | 6/25 | PAUSE | Single engineer preference is not a migration rationale |
>
> **Decision 1 — PostgreSQL → MongoDB:**
> E-commerce has highly relational data: orders → line items → products → inventory → customers. MongoDB's document model forces denormalization (duplication, consistency risk). Before committing: write down the 3 specific problems PostgreSQL is causing today. If you can't name 3, this decision is being made on vibes.
>
> **Decision 3 — AWS → GCP:**
> Engineer preference is not a business rationale. This is the highest-stakes decision in the document with the weakest justification. $15K for three simultaneous migrations of a production e-commerce platform is not a budget — it's a deposit. Require a written technical case before proceeding.

## Based on

Cognitive science research: Kahneman-Klein (conditions for intuitive expertise), Hogarth (kind vs wicked environments), Tetlock (superforecasting), Morewedge (debiasing interventions). Poor decisions cost companies [$250M/year](https://www.newyorkbex.com/new-research-poor-decisions-cost-companies-250m-year) (Fortune 500) and [80% of new products fail](https://hbs.edu) mostly due to bad decisions, not bad execution.
