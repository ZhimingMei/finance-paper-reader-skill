---
name: finance-paper-reader
description: >
  Critically analyze and review academic finance and economics research papers.
  Use this skill whenever the user uploads or shares a finance/economics paper
  and asks for a review, critique, summary, referee report, discussion, or
  critical reading. Also trigger when the user asks to "read this paper", "what
  do you think of this paper", "help me understand this paper", "write a referee
  report", or any similar phrasing. Applies the full critical reading framework
  from Price (2019) and Oh (2024), adapts to paper type (empirical / theoretical
  / mixed), and identifies the finance sub-field automatically.
---

# Finance Paper Reader

A structured critical reading framework for academic finance and economics papers,
synthesizing guidance from Brendan Price (UC Davis, 2019) and Sangmin Oh
(Columbia Business School, 2024).

## Skill structure

| File | Role | When to load |
|------|------|-------------|
| `SKILL.md` (this file) | Main protocol — Steps 0–7 | Always |
| `references/empirical-by-field.md` | Field-specific red flags for empirical papers | Step 2, for Empirical/Mixed papers |
| `references/empirical-roadmap.md` | Full widget spec for interactive empirical roadmap | Step 6, on request only |
| `references/theory-roadmap.md` | Full widget spec for interactive theory roadmap | Step 7, on request only |

---

## Step 0 — Intake and Classification (Always Do This First)

Classify the paper along two dimensions before anything else.

### 0A. Paper Type

| Type | Signals |
|------|---------|
| **Empirical** | Main contribution is causal identification or reduced-form evidence; model (if any) is motivational only |
| **Theoretical** | Main contribution is a formal model; empirical work (if any) is calibration or stylized facts |
| **Mixed** | Substantial original contribution on both fronts — structural estimation, theory + new empirical tests |

→ State the paper type explicitly at the top of your review.
→ For Mixed papers, note which dimension dominates.

### 0B. Finance Sub-Field

Use the introduction and JEL codes if available.

- **Asset Pricing** — cross-section of returns, factor models, anomalies, risk premia, options
- **Asset Management** — mutual funds, hedge funds, institutional investors, delegated portfolio management
- **Corporate Finance** — capital structure, investment, payout, governance, M&A, executive compensation
- **Household Finance** — retail investors, mortgages, consumer credit, savings, financial literacy
- **Banking & Financial Intermediation** — bank lending, systemic risk, regulation, credit markets
- **Market Microstructure** — liquidity, trading, price discovery, high-frequency
- **International Finance** — exchange rates, global capital flows, cross-border investment
- **Public Finance / Labor-Finance Intersection** — tax policy, education finance, labor-capital interactions

---

## Step 1 — Structured Summary (Type-Adaptive)

*From Price (2019): "The introduction is a contract with the reader."*

Produce a **type-adaptive summary** in labeled bullet blocks — not prose. Goal: distill what the paper actually does in a way a reader will not misremember.

### Empirical papers — identify emphasis, use matching bullets:

**Identification-focused**
- **Question**: What is the paper trying to establish causally?
- **Setting**: Institutional background or natural experiment.
- **Variation**: Source of exogenous variation and why it is plausibly exogenous.
- **Design**: First-stage logic or research design.
- **Result**: Main finding in one sentence, with economic magnitude if reported.
- **Data**: Datasets used and sample period.

**Measurement-focused**
- **Question**: What concept is being measured, and why is it hard to measure directly?
- **Inputs**: Raw data sources and methods (text, NLP, administrative records, etc.).
- **Construction**: How the measure is built, step by step.
- **Validation**: How the authors show the measure captures what it claims to.
- **Result**: Main finding in one sentence, with economic magnitude if reported.
- **Data**: Datasets used and sample period.

**Descriptive / stylized-fact**
- **Question**: What new facts are being documented?
- **Sample**: Dataset, coverage, and sample period.
- **Patterns**: Main empirical regularities in 2–3 sentences.
- **Robustness**: Key checks that support the facts.

### Theoretical papers — use these bullets:
- **Question**: What economic problem or puzzle does the model address?
- **Environment**: Agents, timing, and information structure — in plain language.
- **Mechanism**: The key friction or force driving the result.
- **Key Equations**: Display 1–3 central equations with LaTeX-style math, each followed by a one-sentence plain-language gloss.
- **Propositions**: Main theoretical results and their economic intuition.
- **Empirical connection**: How the model connects to data (calibration, stylized facts, or tests).

### Mixed papers — two labeled groups:

**Theory**
- **Mechanism**: Core friction or force in the model.
- **Key Equations**: 1–3 central equations with plain-language glosses.
- **Key result**: Main proposition and its intuition.

**Empirics**
- **Empirical emphasis**: Identification / measurement / descriptive (pick one).
- **Strategy**: Empirical approach in 1–2 sentences.
- **Result**: Main finding with economic magnitude if reported.
- **Data**: Datasets and sample period.

Note which dimension — theory or empirics — is the dominant contribution.

### Always end with:
> **Key Takeaway**: One or two sentences on the single most important thing to remember — the paper's biggest contribution, or its most important caveat.

---

## Step 2 — Empirical Evaluation

*Apply for Empirical and Mixed papers. Skip for purely Theoretical papers.*

Before reading the body: write down your prior threats — what would have to be true for the conclusions to fail? Track whether the paper addresses them.

→ Load `references/empirical-by-field.md` for field-specific red flags.

### 2A. Data
1. **Representativeness**: Is the sample representative? Selection into the sample that raises external validity concerns?
2. **Outlier sensitivity**: Could results be driven by outliers or a specific sub-period?
3. **Data cleaning**: Is cleaning appropriate? Does scaling ensure stationarity? Does transformation introduce spurious results?
4. **Measurement error**: Are key variables measured accurately? Are motivating stylized facts prone to mismeasurement?

### 2B. Methodological Choice
1. **Method justification**: Are methods well-warranted? Is there a simpler approach bypassed without explanation?
2. **Frequency and granularity**: Does the design use available data granularity fully? Is the chosen frequency well-motivated?
3. **Controls**: Are control variables exhaustive? Are there obvious omitted variables?
4. **Standard errors**: Are SEs calculated correctly? Is clustering appropriate for the data structure?

### 2C. Identification and Assumptions
1. **Exogeneity**: Is the claimed source of variation truly exogenous?
2. **Instrument validity**: If IV — is it strong and valid? Are exclusion restriction arguments convincing?
3. **Matching comparability**: If matching — is the matched sample comparable on observables and unobservables?
4. **Mechanical results**: Are assumptions too directly connected to the result?
5. **Arbitrary choices**: Are there unjustified discretionary choices (cutoffs, windows, sample restrictions)?

### 2D. Interpretation and Robustness
1. **Estimand clarity**: What parameter is estimated (ATE, ATT, LATE)? Is the connection to the economic quantity clear?
2. **Alternate stories**: Could an alternate mechanism explain the findings?
3. **Robustness checks**: Are results robust across reasonable perturbations?
4. **Necessity of exercises**: Do all exercises contribute, or is some analysis redundant?

---

## Step 3 — Theoretical Evaluation

*Apply for Theoretical and Mixed papers. Skip for purely Empirical papers.*

### 3A. Model Ingredients
1. **General approach**: Does the framework accurately capture the phenomenon? Is the model unnecessarily complicated?
2. **Objective functions**: Is it reasonable for agents to maximize the assumed objective? Missing motives (risk aversion, learning, constraints)?
3. **Game structure**: Is the game form (timing, stages, strategic interaction) sensible?
4. **Optimality claims**: If something is "optimal" — is it clear what objective is being optimized?
5. **Model novelty**: How does the model differ from existing models? Is the departure well-motivated?
6. **Missing agents**: Are relevant actors omitted that could materially change results?

### 3B. Assumptions
1. **Reasonableness**: Are modeling assumptions grounded in data and institutional setting, or chosen for convenience?
2. **Functional form**: If a function is assumed monotone, convex, or separable — is this consistent with the economic mechanism?
3. **Dynamic assumptions**: Do results hinge on stationarity or that the future resembles the past?
4. **Constant parameters**: Is it reasonable to treat parameters (risk aversion, discount rates) as constant?
5. **Omitted variables**: Are there variables that belong in the model but are excluded?

### 3C. Connection to Data and Real World
1. **Calibration**: Is the model calibrated properly? Should it target additional moments?
2. **Quantitative fit**: Do model-implied magnitudes align with empirical evidence?
3. **Out-of-sample implications**: Does the model generate testable predictions beyond its scope?
4. **Alternate consistency**: Is the model consistent with stylized facts only under specific conditions that may not hold elsewhere?

---

## Step 4 — General Assessment (All Paper Types)

### 4A. Motivation and Contribution
1. **Quantitative importance**: Is the question first-order in magnitude?
2. **Literature positioning**: Is the contribution clearly differentiated? Are there missing citations?
3. **Cross-field relevance**: Is the paper relevant to another field it is missing?
4. **Policy implications**: Are policy implications, if claimed, well-supported?

### 4B. Exposition
1. **Clarity and organization**: Is the paper clearly written and logically organized?
2. **Length and repetition**: Is it too long or repetitive? Could institutional details move to an appendix?
3. **Scientific standards**: Are limitations and caveats explicitly acknowledged?
4. **Formatting and notation**: Are there distracting stylistic issues?

---

## Step 5 — Synthesis and Output

Output rules:
- Summary from Step 1 opens the review (no separate Summary section)
- Every concern is written as a **question**, not an assertion
- Verdict closes with a **Key Takeaway** sentence

```
## Finance Paper Review

**Paper**: [Title, Authors, Year/Journal]
**Type**: [Empirical / Theoretical / Mixed — dominant dimension]
**Sub-field**: [from Step 0B]

---

### What the Paper Does
[Labeled bullet summary from Step 1. Emphasis label first.
Two groups (Theory / Empirics) for Mixed papers.
Key Takeaway on its own line at the end.]

---

### Strengths
[2–4 bullets — specific, cite table/figure/section.]

---

### Questions and Concerns
[Each concern: 1 sentence context + question + optional resolution test. 2–5 sentences total.]

#### Motivation & Contribution
#### Data [Empirical/Mixed only]
#### Identification & Methods [Empirical/Mixed only]
#### Model [Theoretical/Mixed only]
#### Robustness & Interpretation
#### Exposition [only if notable issues]

---

### Verdict
[2–3 sentences. Core claim convincing? 1–2 must-fix issues.
End with **Key Takeaway** — the one sentence to remember.]
```

---

## Step 6 — Empirical Roadmap (On Request)

*Trigger when the user asks for a "roadmap," "map," "walk me through the empirical tests," or any phrasing requesting a structured visual of the paper's empirical architecture. Do not produce automatically.*

→ Load `references/empirical-roadmap.md` for the full widget spec, phase structure, badge system, HTML template, and writing discipline. Follow those instructions exactly to produce the interactive expandable-card widget via the `show_widget` visualizer tool.

---

## Step 7 — Theory Roadmap (On Request)

*Trigger when the user asks for a "theory roadmap," "model walkthrough," "walk me through the model," or any phrasing requesting a structured visual of a theoretical paper's model architecture. Also trigger for Mixed papers when the user wants the model unpacked. Do not produce automatically.*

→ Load `references/theory-roadmap.md` for the full widget spec, 7-stage canonical arc, badge system, HTML template, and writing discipline. Follow those instructions exactly to produce the interactive expandable-card widget via the `show_widget` visualizer tool.

---

## Tips for Efficient Reading (from Price 2019)

- **Know your goal**: Read some papers in full depth; skim others. Focus on what you need — identification strategy, data, or literature fit.
- **Use references strategically**: Frequently-cited papers are worth investigating. How later papers characterize an earlier one clarifies its significance and assumptions.
- **Keep the big picture**: The paper's story informs everything — sample construction, specification choice, robustness checks, sequencing of results. Don't lose the forest for the trees.
