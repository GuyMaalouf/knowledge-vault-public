# Example Vault Structure

This is an example of what a well-organised knowledge vault looks like after a few weeks of use.

Copy this structure as a starting point and rename the topics to match your own life and work.

---

## Example Folder Structure

```
my-knowledge-vault/
│
├── _index.md                        ← MASTER MAP — always read this first
├── _meta/                           ← AI configuration (optional, advanced)
│   └── skills/                      ← Canonical skill instructions
│
├── work.md                          ← Hub: career, role, workplace context
├── work/
│   ├── current-projects.md
│   ├── key-contacts.md
│   └── goals-2025.md
│
├── research.md                      ← Hub: research projects, papers, ideas
├── research/
│   ├── literature-notes.md
│   ├── methodology.md
│   └── open-questions.md
│
├── startup.md                       ← Hub: startup idea, progress, decisions
├── startup/
│   ├── market-research.md
│   ├── mvp-notes.md
│   ├── customer-discovery.md
│   └── decisions-log.md
│
├── knowledge.md                     ← Hub: frameworks, mental models, book notes
├── knowledge/
│   ├── thinking-frameworks.md
│   ├── books-read.md
│   └── lessons-learned.md
│
└── personal.md                      ← Hub: personal context, health, goals
    personal/
    ├── life-goals.md
    └── habits-tracker.md
```

---

## Example `_index.md`

```markdown
# Knowledge Vault Index

## Work
- [[work]] — Software engineer at Acme Corp, leading the data pipeline team

## Research
- [[research]] — PhD research on distributed systems, supervised by Prof. Smith

## Startup
- [[startup]] — Building a B2B SaaS tool for regulatory compliance

## Knowledge
- [[knowledge]] — Mental models, book notes, frameworks I apply regularly

## Personal
- [[personal]] — Personal context, goals, health routines

## Meta
- Last sync: 2025-05-01
- Last tidy: 2025-04-15
- Total notes: 23
```

---

## Example Hub File: `startup.md`

```markdown
# Startup

## What it is
A compliance automation tool for small drone operators navigating EASA regulations.

## Current status
Pre-revenue. 3 customer discovery interviews done. MVP scoped.

## Key decisions
- Chose B2B over B2C (June 2024) — too much friction selling direct to hobbyists
- Focusing on Specific Category operators first (not Open or Certified)
- Solo founder for now; looking for a technical co-founder

## Key open questions
- Is the pain point strong enough to pay for? (testing with 5 more interviews)
- What is the correct pricing model — subscription or per-assessment?

## Links
- [[startup/market-research]] — competitor analysis and TAM
- [[startup/mvp-notes]] — feature list and scope decisions
- [[startup/customer-discovery]] — interview notes and synthesis
- [[startup/decisions-log]] — all major decisions with rationale
```

---

## Example Detail File: `startup/customer-discovery.md`

```markdown
# Customer Discovery Notes

## Interview 1 — Drone operator, freelance, UK (March 2025)
- Main pain: spends 8+ hours on each SORA assessment
- Currently uses Excel templates from a consultant
- Would pay €50–100/month for something automated
- Biggest concern: "will it be accepted by the CAA?"

## Interview 2 — Drone school, Germany (April 2025)
- Has 12 students per cohort, each needs their own SORA
- Buys one template, modifies it for each student — very manual
- Would pay per-cohort rather than per-month
- Key insight: schools are a better initial segment than solo operators

## Synthesis
- Pain is real and time-consuming (8+ hours per assessment)
- Price sensitivity is low if the output is "CAA-ready"
- Schools > freelancers as initial segment
```

---

This structure scales naturally. Start with 2–3 topics, add more as your work evolves. The vault grows with you.
