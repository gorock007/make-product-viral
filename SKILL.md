---
name: make-product-viral
description: Audit a product, website, or landing page against the 32 Principles of a Viral Product (by Mark Lu). Use when the user runs /make-product-viral, or asks to "make my product viral", score/grade/audit a landing page or marketing site for virality, conversion, or shareability, or check a project against the 32 principles. Produces a 0–100 score, per-principle verdict, and prioritized improvement suggestions.
---

# Make Product Viral

Audit the product in the current directory against the **32 Principles of a Viral Product** and return a graded report: an overall score out of 100, a verdict, a per-principle breakdown, and a prioritized list of concrete fixes.

The 32 principles describe what makes a product land, convert, and get shared. They are about the **public surface** of a product — the landing page, hero, headline, pricing, copy, OG image, demo, and call to action — not the backend code quality.

> "These are not rules. They're patterns. Use them as a compass, not a checklist." — Mark Lu

## When to use

Trigger on `/make-product-viral`, or when the user asks to grade/audit/score a landing page, "make my product viral," check virality/shareability/conversion readiness, or evaluate against the 32 principles.

## What to analyze

You are auditing the **marketing and conversion surface**, so find and read the files that represent what a visitor actually sees:

1. **Landing page / hero** — `index.html`, `app/page.tsx`, `app/(marketing)/page.tsx`, `src/pages/index.*`, `pages/index.*`, `app/page.js`, hero/landing components.
2. **Headline & copy** — the H1, subheadline, section headings, body copy across the page.
3. **Pricing** — pricing page/section/component, plan tiers, prices, CTA labels.
4. **Calls to action** — every button/link label and how many distinct CTAs exist.
5. **Meta / OG image** — `<head>` tags, `metadata` exports, `og:image`, `twitter:card`, favicon, page `<title>`.
6. **Social proof** — testimonials, logos, reviews, ratings, comparison tables.
7. **Demo / product visuals** — screenshots, embedded video, interactive demo, GIFs, before/after.
8. **Footer** — final section, share prompts, closing message.
9. **README / positioning** — for the product's intended one-line pitch, name, and target user.

### How to find them
- Start with a quick scan: list the project, identify the framework (Next.js, Astro, plain HTML, Vite, etc.), and locate the landing/marketing entry point.
- Use Grep/Glob to locate hero, pricing, CTA, testimonial, and metadata code. Read the actual rendered text and structure, not just file names.
- If a URL is given, or a dev server is running, you may use the browser tools (claude-in-chrome) to view the live page and OG image — this gives the most accurate read of the hero, colors, and "what you see first." Prefer this when available, but file analysis alone is sufficient.
- If nothing resembling a public-facing page exists (e.g. it's a pure library or backend), say so plainly and explain that the 32 principles target a product's public surface — then offer to evaluate the README/positioning instead.

## How to score

Read `references/scoring.md` for the full rubric. In short:

- Score **each** of the 32 principles on a **0–3** scale:
  - **3** — Fully embodies the principle (exemplary)
  - **2** — Mostly there (good, minor gaps)
  - **1** — Weakly present (attempted but falls short)
  - **0** — Absent or violated
  - **N/A** — Genuinely doesn't apply to this product (use sparingly, and justify it). N/A principles are excluded from the denominator.
- **Overall score = (sum of scored points) ÷ (3 × number of applicable principles) × 100**, rounded to a whole number.
- Be a tough but fair grader. Most early products score 40–65. Reserve 85+ for products that genuinely nail the public surface. Do not inflate.
- Every score of 0 or 1 **must** come with a specific, actionable fix tied to what you actually saw in their files.

## The 32 principles (condensed)

Use these for scoring. Full text and what "good" looks like for each is in `references/principles.md` — read it before grading so your verdicts are accurate.

1. **No free plan** — free users rarely convert; they add cost and noise.
2. **Three colors** — black text, white background, one accent for the Buy button.
3. **Numbers over adjectives** — "Save 4 hours every week," not "fast."
4. **Shareable footer** — finish strong; most visitors won't buy but might share.
5. **OG image = YouTube thumbnail** — design it to earn the click.
6. **One idea per screen** — one screen, one message.
7. **Fifth-grader headline** — simple words your mum understands.
8. **Hard paywall** — ask for payment before data; signups aren't validation.
9. **Copy only you could write** — specific, from experience, not generic.
10. **Show before explain** — a demo beats paragraphs.
11. **Does one thing** — be known for one thing, not a Swiss Army knife.
12. **Popcorn pricing** — three choices: Good, Better, Best.
13. **Rides a wave** — built on a trend/tech/problem people already discuss.
14. **Steals copy from customers** — write the way customers talk.
15. **Visible founder** — a face and voice; people buy from people.
16. **Pricing impossible to miss** — "Pricing" in the header.
17. **Memorable headline** — one people recall the next day.
18. **Emotional headline** — makes people laugh, say wow, or "wtf is this."
19. **Something never seen before** — nobody shares another clone.
20. **Sellable from the hero alone** — 80% won't scroll; the hero must close.
21. **Empathy before selling** — describe the problem better than they can.
22. **One call to action** — one next step, not many.
23. **Memorable name** — real words, no wordplay or names needing explanation.
24. **Sells a desire, not a feature** — money, time, health, status, less pain.
25. **Try before buy** — put the best features on the landing page.
26. **No weak words** — no "most," "many," "rarely"; make clear claims.
27. **No subscription** — one-time payments are far easier to sell.
28. **CTA says what happens next** — "Analyze My Website," not "Get Started."
29. **Has testimonials** — never launch without social proof.
30. **Describable in under 10 words** — if you can't, neither can users.
31. **Compares to competitors** — a table that makes switching obvious.
32. **Priced above competitors** — nobody talks about the second-cheapest option.

## Output format

Produce the report following `references/report-template.md`. Structure it as:

1. **Verdict banner** — Overall score `XX/100`, a one-line verdict, and a tier label (see scoring rubric: Not viral yet / Getting warm / Close / Viral-ready).
2. **Snapshot** — what the product is (in your own under-10-words attempt), and what you analyzed.
3. **Scorecard table** — all 32 principles with score (0–3 or N/A) and a one-line note each. Group with emoji status (🟢 3, 🟡 2, 🟠 1, 🔴 0, ⚪ N/A).
4. **Top fixes (prioritized)** — the 5–8 highest-leverage changes, each with: the principle(s) it addresses, what's wrong now, and a concrete before→after suggestion (rewrite the headline/CTA/etc. for them where you can).
5. **What's already working** — 3–5 strengths so it's not all criticism.

Be concrete and opinionated. When you suggest a fix, write the actual replacement copy, the actual CTA label, the actual pricing structure — don't just say "improve the headline." Reference real file paths (`file_path:line`) so the user can act immediately.

## Important

- Grade what's actually there, not what you imagine could be. Quote real headlines, CTA labels, and prices from their files.
- Don't reward intent — reward execution. "They probably meant to add testimonials" is a 0, not a 2.
- If the product deliberately breaks a principle for a defensible reason (e.g. an open-source tool with a free tier by design), note it as N/A or a justified deviation rather than auto-penalizing — but say so explicitly.
- Keep the tone direct and useful, like a sharp founder-friend reviewing the page.
