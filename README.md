# Decision Linter

**Like ESLint for your thinking.** A 2-minute judgment check before consequential decisions.

> *"I already know the answer"* is the red flag, not the green light.

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
/decision-linter should I add a free tier to grow faster?
```

Or describe any decision naturally — it auto-triggers when it detects high-stakes, low-reversibility choices.

## Uninstall

```
/plugin uninstall decision-linter@decision-linter
/plugin marketplace remove dixalex/decision-linter
```

## What it does

- **Scores assumptions** as Kind (trust gut) or Wicked (impose structure) on 5 dimensions
- **Runs consider-the-opposite** — the only debiasing technique proven on experienced professionals
- **Surfaces blind spots** — what's missing from your experience, what's irrelevant but feels important
- **Outputs a paste-ready memo** for PRs, Slack, proposals, or decision logs
- **Decomposes documents** — dump a spec or plan and it checks each decision independently

## Examples

### "Should I add a free tier?"

> I'm a solo founder with a SaaS at $29/month. 80 paying customers. Growth stalled at ~5 new/month. Considering a free tier to get more users into the funnel. My competitor just launched a free plan.

**Output:**

> **Environment:** WICKED (9/25)
> Competitor pressure + stalled growth feel urgent and obvious. They aren't.
>
> **Key assumption:** Growth stalled because of a top-of-funnel volume problem — more users in = more paid out.
>
> **If wrong:** Growth stalled because of activation or retention. Free users flood support, dilute your ICP signal, and you spend 6 months optimizing a funnel that was never the bottleneck.
>
> **Counter-case:** Your conversion rate from current trials might already be low — more volume through a leaky funnel produces more churn, not more revenue. The competitor launching free doesn't mean it worked for them; it means they made a bet you're now copying without their data.
>
> **Missing:** Why 5/month? Reach problem (not enough finding you) or conviction problem (finding you but not converting)? Base rate: median B2B freemium conversion is 2-5%. At 5 new paid/month, you need 100-250 free users/month to hold the same rate.
>
> **Verdict:** PAUSE — Before committing: (1) Diagnose the stall — reach or conviction? Pull funnel drop-off data. (2) Talk to 5 churned or non-converting prospects. (3) If it's reach, also consider price test, content, or outbound before adding free-tier complexity.

---

### "Rewrite our Node.js API in Rust"

> Our API handles 2,000 req/s. Team wants to rewrite in Rust for performance. 4 engineers, none with Rust experience. Timeline: 3 months.

**Output:**

> **Environment:** WICKED (8/25)
>
> **Key assumption:** 4 engineers with zero Rust experience can reach production-quality proficiency within 3 months while rewriting a 2,000 req/s system.
>
> **If wrong:** The rewrite ships late or not at all. The Node.js system sits unmaintained. The team ships something that performs worse because they don't yet know idiomatic Rust.
>
> **Counter-case:** 2,000 req/s is not a performance problem. Node.js handles 10,000+ trivially for I/O-bound workloads. The bottleneck is almost certainly in the database or architecture — not the runtime. Rust won't fix a slow query.
>
> **Missing:** Profiling data showing where the actual bottleneck is. Base rate on rewrites (Joel Spolsky's "Things You Should Never Do").
>
> **Verdict:** PAUSE — Profile first. Define "better performance" as a metric. If Rust is still the answer, pilot on one isolated service.

---

### "Client wants a full rebuild in 6 weeks"

> Client wants us to rebuild their legacy PHP app as React + Node. Budget: $48K (6 weeks at $8K/week). Current app works but is slow. Their 2-dev team maintains it after handoff. They want all existing features.

**Output:**

> **Environment:** WICKED (9/25)
>
> **Key assumption:** All existing features can be replicated in React + Node in 6 weeks by your team, then maintained by their 2 developers.
>
> **If wrong:** Week 6 delivery is a partial port. Client accepts because they've paid $48K. Their devs inherit an incomplete React app AND still have the PHP system. You've created two systems to maintain instead of one.
>
> **Counter-case:** "Keep all existing features" is the scope commitment most likely to kill this. Feature-complete rewrites nearly always exceed estimates by 50-100%. You're pricing as if you know the full scope. You don't.
>
> **Missing:** What does "slow" actually mean? If it's DB queries or server config, a rewrite solves nothing. Can their 2 PHP devs maintain React + Node? If not, handoff creates a maintainability cliff.
>
> **Verdict:** PAUSE — Scope a discovery sprint first. Confirm their team can maintain the new stack. Propose phased modernization over big-bang rewrite.

## Based on

Cognitive science research: Kahneman-Klein (conditions for intuitive expertise), Hogarth (kind vs wicked environments), Tetlock (superforecasting), Morewedge (debiasing interventions). Poor decisions cost companies [$250M/year](https://www.newyorkbex.com/new-research-poor-decisions-cost-companies-250m-year) (Fortune 500) and [80% of new products fail](https://hbs.edu) mostly due to bad decisions, not bad execution.
