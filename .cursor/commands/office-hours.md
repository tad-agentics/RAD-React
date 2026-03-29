---
name: office-hours
description: Product diagnostic — reframe the app idea before writing any code. Run before /init to challenge assumptions and sharpen the product vision.
---

# /office-hours — Product Diagnostic

> Optional but recommended. Run this before `/init` to stress-test the product idea.
> If Phase 1 artifacts (northstar, EDS) already exist, this command reads them and challenges assumptions.
> If they don't exist yet, this command helps the human think through the product from scratch.

## Step 1 — Understand the idea

If `artifacts/docs/northstar-*.html` exists, read it. Otherwise, ask the human:

"What are you building? Who is it for? What's the one thing it needs to do well?"

## Step 2 — The 5-question diagnostic

Work through each question. Use AskUserQuestion format for each (re-ground, simplify, recommend, options).

### Q1: Who is the specific user?

Not "people who want X" — a specific person. Name, age range, job, daily frustration. The more specific, the better the product.

"Describe one real person who would use this app tomorrow if it existed. What's their day like? Where does this app fit?"

### Q2: What's the job to be done?

Not a feature list. The job the user is hiring this app to do. Format: "When [situation], I want to [motivation], so I can [expected outcome]."

### Q3: What does the 10-star version look like?

Brian Chesky's framework. The 5-star version works. The 10-star version is magical. Describe both:
- 5-star: the user completes the core task without friction
- 7-star: the user is delighted by something unexpected
- 10-star: the user tells everyone they know about it

What would make someone text their friend about this app?

### Q4: What are you intentionally NOT building?

Every app has an anti-scope. Name 3–5 features that sound reasonable but you are choosing to skip. For each: why skip it? What would change your mind?

### Q5: What's the unfair advantage?

Why will this app win where others haven't? Possible answers: unique data, unique distribution, unique insight into the user, existing audience, cost structure, speed of iteration. "No advantage yet" is an honest answer — in that case, the advantage must be speed: ship fast, learn fast.

## Step 3 — Synthesis

After working through all 5 questions, write a summary:

```markdown
## Office Hours Summary

**User:** [specific person description]
**Job to be done:** When [situation], I want to [motivation], so I can [outcome]
**10-star moment:** [the magical thing]
**Not building:** [3–5 explicit exclusions with reasoning]
**Unfair advantage:** [honest assessment]

### Recommendation
[1–2 sentences: go/pivot/rethink, with reasoning]
```

Save to `agent-workspace/temp/office-hours-summary.md` (gitignored — this is pre-planning scratchwork).

If the human has Phase 1 artifacts, compare the summary against the northstar. Flag any misalignment between what the northstar says and what the diagnostic reveals. These misalignments are the most valuable output — they prevent building the wrong thing.

## Step 4 — Next step

"Ready to start building? Run `/init` to scaffold the project."
