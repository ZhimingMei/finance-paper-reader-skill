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

## Quick Reference

| Step | What happens |
|------|-------------|
| **0 — Classify** | Detect paper type (Empirical / Theoretical / Mixed) and finance sub-field |
| **1 — Summarize** | Type-adaptive bullet summary; key equations for theory/mixed papers |
| **2 — Empirical eval** | Data, methods, identification, robustness (load `references/empirical-by-field.md`) |
| **3 — Theory eval** | Model ingredients, assumptions, real-world connection |
| **4 — General** | Contribution, literature positioning, exposition |
| **5 — Output** | Structured review: What the Paper Does → Strengths → Questions → Verdict |

**Output rules**: Summary uses labeled bullet blocks (not prose). Every concern is a question. Verdict ends with a single Key Takeaway sentence.

---

## Step 0 — Intake and Classification (Always Do This First)

Before applying any evaluation framework, classify the paper along two dimensions.

### 0A. Paper Type

Read the abstract, introduction, and section headers to determine:

| Type | Signals |
|------|---------|
| **Empirical** | Main contribution is causal identification or reduced-form evidence; model (if any) is motivational only |
| **Theoretical** | Main contribution is a formal model; empirical work (if any) is calibration or stylized facts |
| **Mixed** | Substantial original contribution on both fronts — structural estimation, theory + new empirical tests |

→ State the paper type explicitly at the top of your review, e.g.: *"This is primarily an **empirical** paper."*
→ For Mixed papers, note which dimension dominates and weight your critique accordingly.

### 0B. Finance Sub-Field

Identify the primary area from the list below. Use the introduction and JEL codes if available.

- **Asset Pricing** — cross-section of returns, factor models, anomalies, risk premia, options
- **Asset Management** — mutual funds, hedge funds, institutional investors, delegated portfolio management
- **Corporate Finance** — capital structure, investment, payout, governance, mergers & acquisitions, executive compensation
- **Household Finance** — retail investors, mortgages, consumer credit, savings, financial literacy
- **Banking & Financial Intermediation** — bank lending, systemic risk, regulation, credit markets
- **Market Microstructure** — liquidity, trading, price discovery, high-frequency
- **International Finance** — exchange rates, global capital flows, cross-border investment
- **Public Finance / Labor-Finance Intersection** — tax policy, education finance, labor market and capital market interactions

→ State the sub-field explicitly, e.g.: *"Sub-field: **Corporate Finance** (investment and financing decisions)."*

---

## Step 1 — Structured Summary (Type-Adaptive)

*From Price (2019): "The introduction is a contract with the reader."*

Read the introduction carefully and produce a **type-adaptive summary** before moving to critique. The goal is to distill what the paper actually does — not just what it claims — in a way that captures the part a reader is most likely to forget or misremember.

### For Empirical papers, identify the paper's primary empirical emphasis and use the matching bullet structure:

**Identification-focused** — use these bullets:
- **Question**: What is the paper trying to establish causally?
- **Setting**: What is the institutional background or natural experiment?
- **Variation**: What is the source of exogenous variation, and why is it plausibly exogenous?
- **Design**: What is the first-stage logic or research design?
- **Result**: Main finding in one sentence, with economic magnitude if reported.
- **Data**: Datasets used and sample period.

**Measurement-focused** — use these bullets:
- **Question**: What concept is being measured, and why is it hard to measure directly?
- **Inputs**: What raw data sources and methods (e.g., text, NLP, administrative records) are used?
- **Construction**: How is the measure built, step by step?
- **Validation**: How do the authors show the measure captures what it claims to?
- **Result**: Main finding in one sentence, with economic magnitude if reported.
- **Data**: Datasets used and sample period.

**Descriptive/stylized-fact** — use these bullets:
- **Question**: What new facts are being documented?
- **Sample**: Dataset, coverage, and sample period.
- **Patterns**: Main empirical regularities in 2–3 sentences.
- **Robustness**: Key checks that support the facts.

### For Theoretical papers, use these bullets:
- **Question**: What economic problem or puzzle does the model address?
- **Environment**: Agents, timing, and information structure — in plain language.
- **Mechanism**: The key friction or force driving the result.
- **Key Equations**: Display 1–3 central equations — the setup, friction term, or main comparative static — that a reader needs to understand the model's logic. Render in LaTeX-style math and follow each with a one-sentence plain-language gloss explaining what it says economically.
- **Propositions**: Main theoretical results and their economic intuition.
- **Empirical connection**: How the model connects to data (calibration, stylized facts, or reduced-form tests).

### For Mixed papers, use two labeled groups of bullets:

**Theory**
- **Mechanism**: The core friction or force in the model.
- **Key Equations**: Display 1–3 central equations with plain-language glosses (same standard as Theoretical above).
- **Key result**: The main proposition and its intuition.

**Empirics**
- **Empirical emphasis**: Identification / measurement / descriptive (pick one).
- **Strategy**: The empirical approach in 1–2 sentences.
- **Result**: Main finding with economic magnitude if reported.
- **Data**: Datasets and sample period.

Also note which dimension — theory or empirics — is the dominant contribution.

### Always end the summary section with:
> **Key Takeaway**: One or two sentences on the single most important thing to remember about this paper — either its most important contribution, or (if the concerns are serious) the most important methodological caveat a reader should carry away.

---

## Step 2 — Empirical Evaluation

*Apply fully for Empirical papers. Apply to the empirical sections of Mixed papers. Skip for purely Theoretical papers.*

**Before diving in**: After reading the introduction, write down your *prior* threats and concerns — what would have to be true for the paper's conclusions to fail? Track whether the body of the paper addresses them.

Read the relevant sub-field reference file for field-specific red flags:
→ `references/empirical-by-field.md`

### 2A. Data

1. **Representativeness**: Is the sample representative of the population the authors claim to study? Is there selection into the sample that raises external validity concerns?
2. **Outlier sensitivity**: Could the results be driven by a few outliers or a specific sub-period?
3. **Data cleaning**: Is the cleaning procedure appropriate? Does scaling ensure stationarity? Does data transformation introduce unintended variation or spurious results?
4. **Measurement error**: Are key variables measured accurately? Are stylized facts used for motivation prone to mismeasurement?

### 2B. Methodological Choice

1. **Method justification**: Are the methods well-warranted for this setting? Is there a simpler approach the authors bypass without explaining why?
2. **Frequency and granularity**: Is the empirical design making full use of available data granularity (e.g., daily vs. monthly, firm-level vs. aggregate)? Is the chosen frequency well-motivated?
3. **Controls**: Are the control variables exhaustive? Are there obvious omitted variables that could confound results?
4. **Standard errors**: Are standard errors calculated correctly? Is clustering appropriate given the data structure? Are the authors using the right technique?

### 2C. Identification and Assumptions

1. **Exogeneity**: Is the claimed source of variation truly exogenous? Is the "plausibly exogenous" variation actually exogenous?
2. **Instrument validity**: If an IV is used — is it a strong and valid instrument? Are the exclusion restriction arguments convincing?
3. **Matching comparability**: If matching is used — is the matched sample comparable on both observable and unobservable characteristics?
4. **Mechanical results**: Are the assumptions too directly connected to the result, making the estimate mechanical?
5. **Arbitrary choices**: Are there discretionary choices (cutoffs, windows, sample restrictions) that are not justified?

### 2D. Interpretation and Robustness

1. **Estimand clarity**: What parameter is being estimated (ATE, ATT, LATE)? Is the connection to the economic quantity of interest clearly articulated?
2. **Alternate stories**: Could an alternate mechanism explain the findings? Do the authors convincingly rule out standard alternative explanations?
3. **Robustness checks**: Are the results robust across reasonable perturbations? Are there specific dimensions (subsamples, specifications, time periods) that warrant additional checks?
4. **Necessity of exercises**: Do all empirical exercises contribute? Is any part of the analysis redundant?

---

## Step 3 — Theoretical Evaluation

*Apply fully for Theoretical papers. Apply to the model sections of Mixed papers. Skip for purely Empirical papers.*

### 3A. Model Ingredients

1. **General approach**: Does the model framework accurately capture the empirical phenomenon of interest? Is the model unnecessarily complicated?
2. **Objective functions**: Is it reasonable for agents to maximize the assumed objective (e.g., are there missing motives such as risk aversion, learning, or constraints)?
3. **Game structure**: Is the assumed game form (timing, number of stages, strategic interaction) sensible?
4. **Optimality claims**: If the authors claim something is "optimal," is it clear what social or private objective is being optimized?
5. **Model novelty**: How does the model differ from existing models of the same phenomenon? Is the departure well-motivated?
6. **Missing agents or groups**: Are there relevant actors omitted from the model that could materially change results?

### 3B. Assumptions

1. **Reasonableness**: Are modeling assumptions chosen arbitrarily, or are they grounded in the data and institutional setting?
2. **Functional form**: If a function is assumed to be monotone, convex, or separable — is this consistent with the underlying economic mechanism?
3. **Dynamic assumptions**: If the model is dynamic, do the results hinge on stationarity or the assumption that the future resembles the past?
4. **Constant parameters**: Is it reasonable to treat parameters (e.g., risk aversion, discount rates) as constant rather than time-varying or heterogeneous?
5. **Omitted variables in model**: Are there variables that belong in the model but are excluded?

### 3C. Connection to Data and Real World

1. **Calibration**: Is the model calibrated properly? Should calibration target additional moments from the data?
2. **Quantitative fit**: Do model-implied magnitudes (elasticities, levels, ratios) align with empirical evidence? Are implied values economically plausible?
3. **Out-of-sample implications**: Does the model generate testable predictions beyond the paper's scope? Do the authors omit interesting implications?
4. **Alternate consistency**: Is the model consistent with stylized facts only under specific conditions that may not hold in other environments?

---

## Step 4 — General Assessment (All Paper Types)

### 4A. Motivation and Contribution

1. **Quantitative importance**: Is the question first-order in magnitude? Is the story plausibly large enough to matter?
2. **Literature positioning**: Is the contribution clearly differentiated from prior work? Are there related papers the authors fail to cite or engage with?
3. **Cross-field relevance**: Is the paper relevant to another field that it is missing? Should it consider other moments or literatures jointly?
4. **Policy implications**: Are the policy implications, if claimed, well-supported by the analysis?

### 4B. Exposition

1. **Clarity and organization**: Is the paper clearly written and logically organized? Are there disconnects between sections or ambiguous statements?
2. **Length and repetition**: Is the paper too long? Is it repetitive? Could institutional details be moved to an appendix?
3. **Scientific standards**: Are limitations and caveats explicitly acknowledged? Is the relation to prior literature clearly articulated?
4. **Formatting and notation**: Are there distracting stylistic issues (inconsistent notation, unexplained acronyms, formatting problems)?

---

## Step 5 — Synthesis and Output

Structure your final output using the template below. Key changes from a generic review:
- **No standalone Summary section** — the structured summary from Step 1 opens the review directly
- **Concerns are written as questions**, not assertions — this surfaces the *reason* for the concern, not just the conclusion
- **Verdict is the closing section** and must include a Key Takeaway

```
## Finance Paper Review

**Paper**: [Title, Authors, Year/Journal if known]
**Type**: [Empirical / Theoretical / Mixed — with note on dominant dimension]
**Sub-field**: [Area from Step 0B]

---

### What the Paper Does
[Type-adaptive bullet summary from Step 1. State the emphasis label first
(e.g., "Emphasis: Measurement-focused"), then use the matching bullet
structure. For mixed papers, use two labeled groups (Theory / Empirics).
Close with the Key Takeaway on its own line.]

---

### Strengths
[2–4 bullet points: what the paper does well. Be specific — cite the table,
figure, or section.]

---

### Questions and Concerns
[Organized by the sections below. Include only sections relevant to paper type.
Write EVERY concern as a question, not a statement. The question should make
the underlying worry self-evident to a reader who hasn't read the paper.

Good format: "The workstyle measure is constructed using static O*NET scores
from 2025 applied over a 2003–2019 panel. If the actual workstyle of an
occupation shifted meaningfully over this period, would the measure capture
those changes, or is it systematically mis-specified for earlier years?"

Bad format: "The O*NET scores are time-invariant, which is a limitation."

Each concern should be 2–5 sentences: one sentence of context, the question
itself, and (optionally) what evidence or test would resolve it.]

#### Motivation & Contribution
#### Data [Empirical/Mixed only]
#### Identification & Methods [Empirical/Mixed only]
#### Model [Theoretical/Mixed only]
#### Robustness & Interpretation
#### Exposition [only if notable issues]

---

### Verdict
[2–3 sentences: Is the core claim convincing? What are the 1–2 must-fix issues
that determine whether the paper succeeds or fails? End with the **Key Takeaway**
— one sentence on the single most important contribution or caveat a reader
should remember from this paper.]
```

---

## Tips for Efficient Reading (from Price 2019)

- **Know your goal**: Read some papers in full depth; skim others. If you're evaluating the identification strategy, focus there. If you're understanding how a paper fits the literature, focus on the introduction.
- **Use references strategically**: Papers that are frequently cited are worth investigating. Reading how later papers characterize an earlier paper can clarify its significance and assumptions.
- **Keep the big picture**: Don't lose the forest for the trees. The "story" of the paper should inform everything — sample construction, specification choice, robustness checks, and sequencing of results.
