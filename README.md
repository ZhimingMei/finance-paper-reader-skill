# Finance Paper Reader Skill

A structured critical reading framework for academic finance and economics papers, designed as a Claude skill. Synthesizes guidance from Brendan Price (UC Davis, 2019) and Sangmin Oh (Columbia Business School, 2024).

---

## What It Does

When you upload a finance or economics paper and ask Claude to review it, this skill:

1. **Classifies the paper** — Empirical, Theoretical, or Mixed — and identifies the finance sub-field (asset pricing, corporate finance, household finance, etc.)
2. **Produces a type-adaptive summary** in structured bullet points, including key equations (with plain-language glosses) for theoretical and mixed papers
3. **Raises critical questions** organized by section — every concern is framed as a question that makes the underlying worry self-evident
4. **Delivers a verdict** with a single Key Takeaway — the one thing worth remembering about the paper

---

## File Structure

```
finance-paper-reader-skill/
├── SKILL.md                          # Main skill — reading protocol and output template
└── references/
    └── empirical-by-field.md         # Field-specific red flags (loaded on demand)
```

---

## How to Use

### In Claude Code
Install the `.skill` file via the Claude Code skill manager, or clone this repo into your skills directory.

### In Claude.ai
Upload the `.skill` file through the skills interface, or copy the contents of `SKILL.md` into a custom instruction.

### Trigger phrases
Once installed, Claude will use this skill automatically when you say things like:
- *"Read this paper critically"*
- *"Write a referee report for this paper"*
- *"What do you think of this paper?"*
- *"Help me understand this paper"*

---

## Output Format

Each review follows this structure:

```
## Finance Paper Review

Paper / Type / Sub-field

### What the Paper Does
[Structured bullets: Question, Setting/Measure Construction, Strategy,
Result (with magnitude), Data — plus Key Equations for theory/mixed papers]

### Strengths
[2–4 specific bullet points]

### Questions and Concerns
[Organized by: Motivation, Data, Identification & Methods, Model,
Robustness & Interpretation, Exposition — all written as questions]

### Verdict
[2–3 sentences + Key Takeaway]
```

---

## Coverage

### Paper Types
| Type | Handling |
|------|---------|
| Empirical | Identifies emphasis (identification / measurement / descriptive); adapts summary and concern structure accordingly |
| Theoretical | Extracts key equations with glosses; evaluates model ingredients, assumptions, and real-world connection |
| Mixed | Covers both dimensions; notes which dominates |

### Finance Sub-fields
Asset Pricing · Asset Management · Corporate Finance · Household Finance · Banking & Financial Intermediation · Market Microstructure · International Finance · Public Finance / Labor-Finance Intersection

The `references/empirical-by-field.md` file contains field-specific red flags loaded when evaluating empirical or mixed papers.

---

## Based On

- Price, Brendan M. (2019). *Reading Papers: Some Tips*. UC Davis, Labor Economics ECN 250A.
- Oh, Sangmin S. (2024). *Reading Papers Critically*. Columbia Business School.

---

## License

MIT
