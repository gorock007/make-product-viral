# Make Product Viral 🚀

A [Claude Code](https://claude.com/claude-code) skill that audits your product's landing page against the **32 Principles of a Viral Product** and hands you a graded report — then fixes the problems for you.

```
/make-product-viral
```

```
🚀 Make Product Viral — Report

  54/100 · 🟠 Getting warm

Your hero explains what the product is but never says why anyone
should care. The CTA says "Get Started" — started with what?

| #  | Principle                    | Score | Note                                    |
|----|------------------------------|:-----:|-----------------------------------------|
| 3  | Numbers over adjectives      |  🔴 0 | "Blazing fast, powerful" — zero numbers |
| 20 | Sellable from the hero alone |  🟠 1 | Value prop is 3 scrolls down            |
| 28 | CTA says what happens next   |  🔴 0 | "Get Started" ×4 → try "Analyze My Site"|
| 29 | Has testimonials             |  🔴 0 | None found anywhere on the page         |
...
```

## What it does

It grades the **public surface** of your product — hero, headline, pricing, OG image, demo, CTA, testimonials, footer copy — not your backend code quality. You get:

- An overall **score out of 100** and a tier verdict
- A **scorecard of all 32 principles**, each scored 0–3 with a one-line reason
- **5–8 prioritized fixes**, each with real before→after copy written for *your* product
- A short list of **what's already working**, so it's not all criticism

Every score is anchored to something it actually read in your files, quoted with a `file:line` reference. It's built to be a tough grader — most early products land in the 40–65 range.

The best part is what happens after the report: tell Claude which fixes you want and it edits your code directly.

## Install

Skills live in `~/.claude/skills/`. Drop this folder in there and Claude Code auto-discovers it — no config, no restart.

**With git:**

```bash
git clone https://github.com/gorock007/make-product-viral.git ~/.claude/skills/make-product-viral
```

**Without git** — [download the ZIP](https://github.com/gorock007/make-product-viral/archive/refs/heads/main.zip), unzip it, and move the folder to `~/.claude/skills/make-product-viral` (make sure `SKILL.md` sits at the top level of that folder, not inside a nested subfolder).

**Verify it's installed** — start Claude Code and run:

```
/make-product-viral
```

If the command doesn't appear, check that the path is exactly `~/.claude/skills/make-product-viral/SKILL.md`.

### Project-local install

To make it available to your team inside one repo instead of globally, put it in `.claude/skills/make-product-viral/` within that project and commit it.

## Usage

Run it from inside your project directory:

```
/make-product-viral
```

Or just ask in plain language:

- *"make my product viral"*
- *"score my landing page against the 32 principles"*
- *"audit my hero section for virality"*

It works with Next.js, Astro, Vite, plain HTML, and most other web projects — it finds your landing page by looking for the usual entry points (`index.html`, `app/page.tsx`, `src/pages/index.*`, and friends).

If you have a dev server running or a live URL, mention it. With the [Claude in Chrome](https://claude.com/chrome) extension the skill will look at the rendered page, which gives a far more accurate read on colors, the hero, and what a visitor genuinely sees first.

## The 32 principles

1. No free plan
2. Three colors
3. Numbers over adjectives
4. Shareable footer
5. OG image = YouTube thumbnail
6. One idea per screen
7. Fifth-grader headline
8. Hard paywall
9. Copy only you could write
10. Show before explain
11. Does one thing
12. Popcorn pricing
13. Rides a wave
14. Steals copy from customers
15. Visible founder
16. Pricing impossible to miss
17. Memorable headline
18. Emotional headline
19. Something never seen before
20. Sellable from the hero alone
21. Empathy before selling
22. One call to action
23. Memorable name
24. Sells a desire, not a feature
25. Try before buy
26. No weak words
27. No subscription
28. CTA says what happens next
29. Has testimonials
30. Describable in under 10 words
31. Compares to competitors
32. Priced above competitors

Full text of each — with what a 3 and a 0 actually look like — is in [`references/principles.md`](references/principles.md).

> "These are not rules. They're patterns. Use them as a compass, not a checklist." — Mark Lu

## How scoring works

Each principle is scored 0–3 (or N/A where it genuinely doesn't apply, like the paywall principles for a deliberately free open-source tool):

```
overall = sum(scores) / (3 × applicable principles) × 100
```

| Score | Tier |
|-------|------|
| 0–39 | 🔴 Not viral yet |
| 40–59 | 🟠 Getting warm |
| 60–79 | 🟡 Close |
| 80–100 | 🟢 Viral-ready |

The full rubric lives in [`references/scoring.md`](references/scoring.md).

## Structure

```
make-product-viral/
├── SKILL.md                    # the skill: workflow + condensed principles
└── references/
    ├── principles.md           # all 32 in full, with grading anchors
    ├── scoring.md              # 0–3 rubric, 0–100 math, tier labels
    └── report-template.md      # output format
```

These are plain markdown files. Edit them — reweight a principle, add your own, change the tone of the report — and the skill changes with them.

## Credit

This skill was inspired by [Marc Lou's original post on X](https://x.com/marclou/status/2065385672991752210) and his **32 Principles of a Viral Product**. The principles were distilled from 5 years of building 35 startups in public. This skill packages them as a repeatable audit; the thinking is his.

## License

MIT — see [LICENSE](LICENSE).
