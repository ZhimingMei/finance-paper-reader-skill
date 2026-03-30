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

## Step 6 — Empirical Roadmap (On Request)

*Trigger this step when the user asks for a "roadmap," "map," "overview," or "walk me through the empirical tests" — or any phrasing that requests a structured visual summary of the paper's empirical architecture. Do not produce this automatically as part of the standard review.*

When triggered, produce an **interactive HTML widget** using the `show_widget` visualizer tool that renders all empirical tests as expandable cards, organized into logical phases that reflect the paper's internal narrative arc.

### What the roadmap must contain

For each empirical test, populate four fields:

1. **What is the test** — the specification, dependent variable, variation used, and key fixed effects. Be precise enough that a reader could sketch the regression.
2. **Why we need it** — what identification challenge or alternative story this test is designed to address. Frame it as "without this test, a reader could object that…"
3. **Intuition** — the economic or statistical logic in plain language. What is the underlying thought experiment?
4. **Key takeaway** — the headline number or qualitative finding. For mechanism tests, note what the result rules in or rules out.

### How to group tests into phases

Read the paper's section structure and group tests into 4–6 phases that tell a coherent story. Typical phase structure for empirical finance papers:

| Phase | Purpose | Typical tests |
|-------|---------|--------------|
| **Documenting the phenomenon** | Establish that the thing being studied is real and large | Descriptive plots, time-series trends, summary statistics, hedonic/measurement models |
| **Causal effect estimation** | Identify the treatment effect causally | DiD, triple-DiD, IV/2SLS, RD, event studies |
| **Ruling out alternatives** | Falsify competing explanations | Quantity vs. price tests, HHI/concentration tests, placebo regressions, subgroup falsifications |
| **Mechanism: first channel** | Show evidence for the primary mechanism | Distribution moment tests, reserve/balance-sheet analyses |
| **Mechanism: second channel** | Show evidence for the secondary mechanism | Cross-sectional heterogeneity by constraint/exposure, profit/margin trends |
| **Robustness** | Confirm results are not artefacts of specification choices | Alternative cutoffs, treatment windows, subsamples, alternative dependent variables |

Not every paper has all six phases. Omit phases that don't apply; add phases if the paper's structure warrants it (e.g., a paper with three distinct mechanisms needs three mechanism phases).

### Badge color coding

Assign one of four badge types to each test based on its primary purpose:

| Badge | Color | Use when |
|-------|-------|---------|
| `Descriptive` | Purple | The test documents a fact, measures a quantity, or establishes a trend — no causal claim |
| `Causal` | Teal | The test uses a research design (DiD, IV, RD) to establish a causal effect |
| `Falsification` | Coral/Orange | The test is designed to rule out an alternative explanation |
| `Mechanism` | Amber | The test provides evidence for a specific channel or mechanism |

### Widget implementation

Use the following HTML/CSS structure. Copy the pattern exactly — spacing, card behavior, badge colors, connector lines, and phase labels are all calibrated for readability.

```html
<style>
  * { box-sizing: border-box; }
  .roadmap { padding: 16px 0 24px; font-family: var(--font-sans); }
  .phase-label {
    font-size: 11px; font-weight: 500; letter-spacing: 0.06em; text-transform: uppercase;
    color: var(--color-text-tertiary); margin: 0 0 8px 0; padding-left: 4px;
  }
  .test-card {
    border: 0.5px solid var(--color-border-tertiary);
    border-radius: var(--border-radius-lg);
    background: var(--color-background-secondary);
    margin-bottom: 10px; overflow: hidden;
    transition: border-color 0.15s; cursor: pointer;
  }
  .test-card:hover { border-color: var(--color-border-primary); }
  .test-card.open { border-color: var(--color-border-secondary); }
  .card-header { display: flex; align-items: center; gap: 10px; padding: 12px 14px; }
  .badge {
    flex-shrink: 0; font-size: 11px; font-weight: 500;
    padding: 2px 8px; border-radius: 20px; white-space: nowrap;
  }
  .badge-desc   { background: #EEEDFE; color: #3C3489; }
  .badge-causal { background: #E1F5EE; color: #085041; }
  .badge-mech   { background: #FAEEDA; color: #633806; }
  .badge-alt    { background: #FAECE7; color: #4A1B0C; }
  @media (prefers-color-scheme: dark) {
    .badge-desc   { background: #3C3489; color: #CECBF6; }
    .badge-causal { background: #085041; color: #9FE1CB; }
    .badge-mech   { background: #633806; color: #FAC775; }
    .badge-alt    { background: #4A1B0C; color: #F5C4B3; }
  }
  .card-title {
    font-size: 14px; font-weight: 500;
    color: var(--color-text-primary); flex: 1; line-height: 1.35;
  }
  .card-num {
    flex-shrink: 0; font-size: 11px; font-weight: 500;
    color: var(--color-text-tertiary); min-width: 22px; text-align: right;
  }
  .chevron {
    flex-shrink: 0; font-size: 12px; color: var(--color-text-tertiary);
    transition: transform 0.2s; line-height: 1;
  }
  .test-card.open .chevron { transform: rotate(90deg); }
  .card-body {
    display: none; padding: 0 14px 14px;
    border-top: 0.5px solid var(--color-border-tertiary);
  }
  .test-card.open .card-body { display: block; }
  .row { display: grid; grid-template-columns: 1fr 1fr; gap: 10px; margin-top: 10px; }
  .cell {
    border: 0.5px solid var(--color-border-tertiary);
    border-radius: var(--border-radius-md); padding: 10px 12px;
    background: var(--color-background-primary);
  }
  .cell-label {
    font-size: 11px; font-weight: 500; letter-spacing: 0.05em;
    text-transform: uppercase; color: var(--color-text-tertiary); margin-bottom: 5px;
  }
  .cell-text { font-size: 13px; line-height: 1.55; color: var(--color-text-secondary); }
  .takeaway {
    margin-top: 10px; border-radius: var(--border-radius-md);
    padding: 10px 12px; background: #E1F5EE;
    border-left: 3px solid #1D9E75;
    font-size: 13px; line-height: 1.55; color: #085041;
  }
  @media (prefers-color-scheme: dark) {
    .takeaway { background: #04342C; border-left-color: #5DCAA5; color: #9FE1CB; }
  }
  .takeaway-label { font-weight: 500; margin-bottom: 3px; }
  .connector {
    display: flex; align-items: center; gap: 8px;
    padding: 4px 14px; color: var(--color-text-tertiary); font-size: 12px;
  }
  .connector-line { flex: 1; height: 0.5px; background: var(--color-border-tertiary); }
  .phase-group { margin-bottom: 4px; }
</style>

<div class="roadmap">

  <!-- ── PHASE 1 ── -->
  <div class="phase-group">
    <div class="phase-label">Phase 1 — [Phase name]</div>

    <div class="test-card" onclick="toggle(this)">
      <div class="card-header">
        <span class="badge badge-desc">Descriptive</span>
        <span class="card-title">[Test name]</span>
        <span class="card-num">T1</span>
        <span class="chevron">›</span>
      </div>
      <div class="card-body">
        <div class="row">
          <div class="cell">
            <div class="cell-label">What is the test</div>
            <div class="cell-text">[Specification details]</div>
          </div>
          <div class="cell">
            <div class="cell-label">Why we need it</div>
            <div class="cell-text">[Identification challenge addressed]</div>
          </div>
        </div>
        <div class="row">
          <div class="cell">
            <div class="cell-label">Intuition</div>
            <div class="cell-text">[Plain-language logic]</div>
          </div>
          <div class="cell">
            <div class="cell-label">Key takeaway</div>
            <div class="cell-text">[Headline finding or ruling-in/out]</div>
          </div>
        </div>
        <!-- Optional: add a green callout box when the test feeds into a later design -->
        <div class="takeaway">
          <div class="takeaway-label">[Optional callout label]</div>
          [Use this box when the test result is also an input to a subsequent test —
           e.g., a measurement model whose residuals become an IV.]
        </div>
      </div>
    </div>

  </div>

  <!-- ── CONNECTOR ── (between phases) -->
  <div class="connector">
    <div class="connector-line"></div>
    <span>[Short phrase describing the logical bridge, e.g. "Phenomenon established → causal effect estimation"]</span>
    <div class="connector-line"></div>
  </div>

  <!-- ── PHASE 2 ── -->
  <div class="phase-group">
    <div class="phase-label">Phase 2 — [Phase name]</div>
    <!-- repeat .test-card pattern, changing badge class as needed -->
  </div>

</div>

<script>
function toggle(card) { card.classList.toggle('open'); }
</script>
```

### Rules for the takeaway (green callout) box

Use the green callout box **only** when a test does double duty — its result is both standalone evidence and a direct input to a later test. The most common case: a measurement model whose residuals become an IV. The callout should name the later test explicitly so a reader can trace the dependency. Do not use it as a general "important result" box — the `Key takeaway` cell already serves that purpose.

### Writing discipline

- **Card titles**: sentence case, ≤ 10 words, descriptive of the design not just the topic. Good: "Triple-difference: add geographic exposure variation." Bad: "Triple difference."
- **Cell text**: 2–4 sentences each. Aim for 13px readability — dense but scannable.
- **Phase labels**: sentence case, short (3–6 words). They are navigation anchors, not section headings.
- **Connector text**: one short phrase that names the logical transition. It should read like a sentence fragment: "Causal effect confirmed → mechanism dissection."
- **Test numbering**: T1, T2, … in reading order across all phases. Robustness tests get their own numbers if they appear in the paper as distinct exercises; generic robustness checks that are described in a single paragraph can be grouped into one card.

---

## Step 7 — Theory Roadmap (On Request)

*Trigger this step when the user asks for a "theory roadmap," "model walkthrough," "walk me through the model," or any phrasing that requests a structured visual summary of a theoretical paper's architecture. Also trigger for the theory section of Mixed papers when the user specifically wants the model unpacked. Do not produce this automatically as part of the standard review.*

When triggered, produce an **interactive HTML widget** using the `show_widget` visualizer tool that renders each stage of the theory paper as an expandable card, organized into the canonical presentation arc that finance economists follow.

### The canonical theory paper arc

Finance theory papers follow a predictable structure. Map each section of the paper onto these stages in order:

| Stage | Purpose | What to look for |
|-------|---------|-----------------|
| **1 — Motivation & Question** | Establish the economic puzzle and why existing models cannot explain it | Stylized facts cited, gap in literature, verbal mechanism sketch |
| **2 — Environment & Setup** | Define agents, preferences, endowments, technology, timing, information | Objective functions, constraints, parameter definitions, timeline |
| **3 — Equilibrium** | Solve for equilibrium prices, quantities, allocations | Solution concept, existence/uniqueness, equilibrium conditions |
| **4 — Main Results** | State and interpret the key propositions | Propositions/lemmas, economic intuition, key equations |
| **5 — Comparative Statics** | Show how equilibrium outcomes change with parameters | Signs of derivatives, threshold conditions, non-monotonicities |
| **6 — Extensions & Robustness** | Relax key assumptions; check generality | Which assumptions are load-bearing, GE effects, heterogeneity |
| **7 — Empirical Connection** | Link model predictions to data | Calibration moments, reduced-form tests, distinguishing predictions |

### What each card must contain

For each stage, populate four fields:

1. **What the paper does** — what the authors actually write in this stage: the specific assumptions made, propositions stated, or exercises run. Be precise enough that a reader could locate it in the paper.
2. **Critical questions** — the 2–3 sharpest questions a referee would ask at this stage, drawn from Oh (2024). Frame as questions, not assertions. Examples by stage:
   - *Setup*: "Is it reasonable to assume agents maximize X while ignoring Y?" / "Does a two-period model miss important dynamics?"
   - *Equilibrium*: "Is the equilibrium unique, and if not, how is multiplicity resolved?" / "Does the solution concept (Nash, competitive) fit the setting?"
   - *Results*: "Is this proposition a deep insight or a mechanical consequence of the functional form assumed?" / "Can the driving force be stated in one sentence without math?"
   - *Comparative statics*: "Are the signs unambiguous, or do they depend on parameter restrictions that may not hold empirically?" / "Is the non-monotonicity economically plausible?"
   - *Extensions*: "Which simplifying assumption is most load-bearing for the main result?" / "What happens in general equilibrium?"
   - *Empirical connection*: "Are the calibration moments the right ones to discipline the model?" / "Does the model make a prediction that competing theories cannot also produce?"
3. **Key equation** — if this stage has a central equation (e.g., the agent's problem, the equilibrium condition, the main comparative static), display it in LaTeX-style math followed by a one-line plain-language gloss. Write "—" if the stage is purely verbal.
4. **Assessment** — a one-sentence verdict on this stage: is it convincing, load-bearing, underdeveloped, or a potential weakness?

### How to group stages

Use all seven stages for a pure theory paper. For a Mixed paper, condense stages 1–3 into a single "Model Setup" card if the empirics dominate, and focus card depth on stages 4–7. Omit a stage only if the paper genuinely skips it (e.g., no calibration → omit Stage 7).

### Badge color coding

Assign one of four badge types to each card based on its primary character:

| Badge | Color | Use when |
|-------|-------|---------|
| `Setup` | Purple | Defining the environment, agents, preferences, timing |
| `Result` | Teal | Propositions, lemmas, equilibrium characterization |
| `Mechanism` | Amber | Comparative statics, economic intuition, channel identification |
| `Robustness` | Coral | Extensions, sensitivity to assumptions, empirical connection |

### Widget implementation

Use the following HTML/CSS structure — it mirrors the empirical roadmap exactly so both widgets have a consistent visual language.

```html
<style>
  * { box-sizing: border-box; }
  .roadmap { padding: 16px 0 24px; font-family: var(--font-sans); }
  .phase-label {
    font-size: 11px; font-weight: 500; letter-spacing: 0.06em; text-transform: uppercase;
    color: var(--color-text-tertiary); margin: 0 0 8px 0; padding-left: 4px;
  }
  .test-card {
    border: 0.5px solid var(--color-border-tertiary);
    border-radius: var(--border-radius-lg);
    background: var(--color-background-secondary);
    margin-bottom: 10px; overflow: hidden;
    transition: border-color 0.15s; cursor: pointer;
  }
  .test-card:hover { border-color: var(--color-border-primary); }
  .test-card.open { border-color: var(--color-border-secondary); }
  .card-header { display: flex; align-items: center; gap: 10px; padding: 12px 14px; }
  .badge {
    flex-shrink: 0; font-size: 11px; font-weight: 500;
    padding: 2px 8px; border-radius: 20px; white-space: nowrap;
  }
  .badge-setup  { background: #EEEDFE; color: #3C3489; }
  .badge-result { background: #E1F5EE; color: #085041; }
  .badge-mech   { background: #FAEEDA; color: #633806; }
  .badge-robust { background: #FAECE7; color: #4A1B0C; }
  @media (prefers-color-scheme: dark) {
    .badge-setup  { background: #3C3489; color: #CECBF6; }
    .badge-result { background: #085041; color: #9FE1CB; }
    .badge-mech   { background: #633806; color: #FAC775; }
    .badge-robust { background: #4A1B0C; color: #F5C4B3; }
  }
  .card-title {
    font-size: 14px; font-weight: 500;
    color: var(--color-text-primary); flex: 1; line-height: 1.35;
  }
  .card-num {
    flex-shrink: 0; font-size: 11px; font-weight: 500;
    color: var(--color-text-tertiary); min-width: 22px; text-align: right;
  }
  .chevron {
    flex-shrink: 0; font-size: 12px; color: var(--color-text-tertiary);
    transition: transform 0.2s; line-height: 1;
  }
  .test-card.open .chevron { transform: rotate(90deg); }
  .card-body {
    display: none; padding: 0 14px 14px;
    border-top: 0.5px solid var(--color-border-tertiary);
  }
  .test-card.open .card-body { display: block; }
  .row { display: grid; grid-template-columns: 1fr 1fr; gap: 10px; margin-top: 10px; }
  .row-full { margin-top: 10px; }
  .cell {
    border: 0.5px solid var(--color-border-tertiary);
    border-radius: var(--border-radius-md); padding: 10px 12px;
    background: var(--color-background-primary);
  }
  .cell-label {
    font-size: 11px; font-weight: 500; letter-spacing: 0.05em;
    text-transform: uppercase; color: var(--color-text-tertiary); margin-bottom: 5px;
  }
  .cell-text { font-size: 13px; line-height: 1.55; color: var(--color-text-secondary); }
  .cell-eq { font-size: 13px; line-height: 1.7; color: var(--color-text-secondary); font-style: italic; }
  .assessment {
    margin-top: 10px; border-radius: var(--border-radius-md);
    padding: 10px 12px; background: #E1F5EE;
    border-left: 3px solid #1D9E75;
    font-size: 13px; line-height: 1.55; color: #085041;
  }
  @media (prefers-color-scheme: dark) {
    .assessment { background: #04342C; border-left-color: #5DCAA5; color: #9FE1CB; }
  }
  .assessment-label { font-weight: 500; margin-bottom: 3px; }
  .connector {
    display: flex; align-items: center; gap: 8px;
    padding: 4px 14px; color: var(--color-text-tertiary); font-size: 12px;
  }
  .connector-line { flex: 1; height: 0.5px; background: var(--color-border-tertiary); }
  .phase-group { margin-bottom: 4px; }
</style>

<div class="roadmap">

  <!-- ── STAGE 1 — MOTIVATION ── -->
  <div class="phase-group">
    <div class="phase-label">Stage 1 — Motivation & Question</div>

    <div class="test-card" onclick="toggle(this)">
      <div class="card-header">
        <span class="badge badge-setup">Setup</span>
        <span class="card-title">[What economic puzzle does the paper address?]</span>
        <span class="card-num">S1</span>
        <span class="chevron">›</span>
      </div>
      <div class="card-body">
        <div class="row">
          <div class="cell">
            <div class="cell-label">What the paper does</div>
            <div class="cell-text">[Stylized facts cited, gap in literature claimed, verbal mechanism sketch]</div>
          </div>
          <div class="cell">
            <div class="cell-label">Critical questions</div>
            <div class="cell-text">Is the stylized fact well-established, or prone to measurement error? Is the gap in the literature real — could an existing model explain the phenomenon with minor modification? Is the verbal mechanism stated before the math, or does it only become clear after the propositions?</div>
          </div>
        </div>
        <div class="row">
          <div class="cell">
            <div class="cell-label">Key equation</div>
            <div class="cell-eq">[LaTeX equation if applicable, or "—"]</div>
          </div>
          <div class="cell">
            <div class="cell-label">Assessment</div>
            <div class="cell-text">[One-sentence verdict on this stage]</div>
          </div>
        </div>
      </div>
    </div>
  </div>

  <div class="connector">
    <div class="connector-line"></div>
    <span>Puzzle established → model environment</span>
    <div class="connector-line"></div>
  </div>

  <!-- ── STAGE 2 — SETUP ── -->
  <div class="phase-group">
    <div class="phase-label">Stage 2 — Environment & Setup</div>

    <div class="test-card" onclick="toggle(this)">
      <div class="card-header">
        <span class="badge badge-setup">Setup</span>
        <span class="card-title">[Agents, preferences, endowments, timing, information]</span>
        <span class="card-num">S2</span>
        <span class="chevron">›</span>
      </div>
      <div class="card-body">
        <div class="row">
          <div class="cell">
            <div class="cell-label">What the paper does</div>
            <div class="cell-text">[Specific assumptions: who are the agents, what do they maximize, what are the constraints, what is the timing/information structure]</div>
          </div>
          <div class="cell">
            <div class="cell-label">Critical questions</div>
            <div class="cell-text">Is every assumption doing real economic work, or are some present only for tractability? Is the objective function reasonable — are there missing motives (e.g., risk aversion, learning, limited attention)? Does the timing of moves (who acts first, what is observable when) match the real-world setting?</div>
          </div>
        </div>
        <div class="row">
          <div class="cell">
            <div class="cell-label">Key equation</div>
            <div class="cell-eq">[Agent's optimization problem or budget constraint in LaTeX, + one-line gloss]</div>
          </div>
          <div class="cell">
            <div class="cell-label">Assessment</div>
            <div class="cell-text">[One-sentence verdict: are assumptions well-motivated or convenient?]</div>
          </div>
        </div>
      </div>
    </div>
  </div>

  <div class="connector">
    <div class="connector-line"></div>
    <span>Environment defined → equilibrium characterization</span>
    <div class="connector-line"></div>
  </div>

  <!-- ── STAGE 3 — EQUILIBRIUM ── -->
  <div class="phase-group">
    <div class="phase-label">Stage 3 — Equilibrium</div>

    <div class="test-card" onclick="toggle(this)">
      <div class="card-header">
        <span class="badge badge-result">Result</span>
        <span class="card-title">[Equilibrium concept, existence, uniqueness]</span>
        <span class="card-num">S3</span>
        <span class="chevron">›</span>
      </div>
      <div class="card-body">
        <div class="row">
          <div class="cell">
            <div class="cell-label">What the paper does</div>
            <div class="cell-text">[Solution concept used (Nash, competitive, rational expectations, etc.), equilibrium conditions stated, how multiplicity is handled if it arises]</div>
          </div>
          <div class="cell">
            <div class="cell-label">Critical questions</div>
            <div class="cell-text">Is the solution concept appropriate for the game structure — does Nash make sense if players are atomistic? Is the equilibrium unique? If multiple equilibria exist, is the selection criterion economically motivated or merely convenient? Are the equilibrium conditions interpretable without tracing through all the algebra?</div>
          </div>
        </div>
        <div class="row">
          <div class="cell">
            <div class="cell-label">Key equation</div>
            <div class="cell-eq">[Equilibrium condition or market-clearing equation in LaTeX, + one-line gloss]</div>
          </div>
          <div class="cell">
            <div class="cell-label">Assessment</div>
            <div class="cell-text">[One-sentence verdict: is the equilibrium well-characterized and the solution concept appropriate?]</div>
          </div>
        </div>
      </div>
    </div>
  </div>

  <div class="connector">
    <div class="connector-line"></div>
    <span>Equilibrium solved → main theoretical results</span>
    <div class="connector-line"></div>
  </div>

  <!-- ── STAGE 4 — MAIN RESULTS ── -->
  <div class="phase-group">
    <div class="phase-label">Stage 4 — Main Results</div>

    <div class="test-card" onclick="toggle(this)">
      <div class="card-header">
        <span class="badge badge-result">Result</span>
        <span class="card-title">[Key proposition and its economic content]</span>
        <span class="card-num">S4</span>
        <span class="chevron">›</span>
      </div>
      <div class="card-body">
        <div class="row">
          <div class="cell">
            <div class="cell-label">What the paper does</div>
            <div class="cell-text">[State the proposition(s) in plain language — what is the paper claiming is true in the model, and what is the intuition given for why]</div>
          </div>
          <div class="cell">
            <div class="cell-label">Critical questions</div>
            <div class="cell-text">Is this a deep economic insight or a mechanical consequence of the functional form chosen in Stage 2? Can the driving force be stated in one sentence without math? Would the result disappear if a single assumption were changed — and is that assumption realistic? Is the result surprising relative to the existing literature, or does it merely confirm what practitioners already know?</div>
          </div>
        </div>
        <div class="row">
          <div class="cell">
            <div class="cell-label">Key equation</div>
            <div class="cell-eq">[Main proposition equation or comparative static in LaTeX, + one-line gloss]</div>
          </div>
          <div class="cell">
            <div class="cell-label">Assessment</div>
            <div class="cell-text">[One-sentence verdict: is this a genuine insight or a known result re-dressed?]</div>
          </div>
        </div>
        <div class="assessment">
          <div class="assessment-label">Mechanism in one sentence</div>
          [Fill in: "The result holds because [economic force A] dominates [economic force B] when [condition C] is satisfied." If you cannot complete this sentence, that is itself a concern about the paper's transparency.]
        </div>
      </div>
    </div>
  </div>

  <div class="connector">
    <div class="connector-line"></div>
    <span>Results established → parameter sensitivity</span>
    <div class="connector-line"></div>
  </div>

  <!-- ── STAGE 5 — COMPARATIVE STATICS ── -->
  <div class="phase-group">
    <div class="phase-label">Stage 5 — Comparative Statics</div>

    <div class="test-card" onclick="toggle(this)">
      <div class="card-header">
        <span class="badge badge-mech">Mechanism</span>
        <span class="card-title">[How do outcomes change with key parameters?]</span>
        <span class="card-num">S5</span>
        <span class="chevron">›</span>
      </div>
      <div class="card-body">
        <div class="row">
          <div class="cell">
            <div class="cell-label">What the paper does</div>
            <div class="cell-text">[Which parameters are varied, direction and sign of effects, any threshold conditions or non-monotonicities]</div>
          </div>
          <div class="cell">
            <div class="cell-label">Critical questions</div>
            <div class="cell-text">Are the signs of the comparative statics unambiguous, or do they depend on parameter restrictions that may not hold empirically? If there is a non-monotonicity, is it economically plausible or a modeling artifact? Are the parameters that matter most for the result observable or measurable — i.e., can the comparative statics be taken to data? Does varying a "key" parameter actually change the mechanism, or just scale the effect?</div>
          </div>
        </div>
        <div class="row">
          <div class="cell">
            <div class="cell-label">Key equation</div>
            <div class="cell-eq">[Key derivative or threshold condition in LaTeX, + one-line gloss]</div>
          </div>
          <div class="cell">
            <div class="cell-label">Assessment</div>
            <div class="cell-text">[One-sentence verdict: are the comparative statics empirically meaningful and unambiguous?]</div>
          </div>
        </div>
      </div>
    </div>
  </div>

  <div class="connector">
    <div class="connector-line"></div>
    <span>Mechanism pinned down → assumption stress-testing</span>
    <div class="connector-line"></div>
  </div>

  <!-- ── STAGE 6 — EXTENSIONS ── -->
  <div class="phase-group">
    <div class="phase-label">Stage 6 — Extensions & Robustness</div>

    <div class="test-card" onclick="toggle(this)">
      <div class="card-header">
        <span class="badge badge-robust">Robustness</span>
        <span class="card-title">[Which simplifying assumptions are relaxed, and what survives?]</span>
        <span class="card-num">S6</span>
        <span class="chevron">›</span>
      </div>
      <div class="card-body">
        <div class="row">
          <div class="cell">
            <div class="cell-label">What the paper does</div>
            <div class="cell-text">[Which assumptions are relaxed, what extensions are considered — heterogeneity, dynamics, general equilibrium, alternative information structures]</div>
          </div>
          <div class="cell">
            <div class="cell-label">Critical questions</div>
            <div class="cell-text">Which simplifying assumption from Stage 2 is most load-bearing for the main result — and is it addressed here? What happens in general equilibrium: do the partial-equilibrium results survive when prices adjust endogenously? Does heterogeneity across agents matter — would the result be stronger or weaker if agents differed in risk aversion, wealth, or information? Are there missing extensions that a referee would immediately flag?</div>
          </div>
        </div>
        <div class="row">
          <div class="cell">
            <div class="cell-label">Key equation</div>
            <div class="cell-eq">[Modified equilibrium condition under extension, or "—" if purely verbal]</div>
          </div>
          <div class="cell">
            <div class="cell-label">Assessment</div>
            <div class="cell-text">[One-sentence verdict: are the most important assumptions stress-tested, or are key ones left untouched?]</div>
          </div>
        </div>
      </div>
    </div>
  </div>

  <div class="connector">
    <div class="connector-line"></div>
    <span>Model stress-tested → connection to data</span>
    <div class="connector-line"></div>
  </div>

  <!-- ── STAGE 7 — EMPIRICAL CONNECTION ── -->
  <div class="phase-group">
    <div class="phase-label">Stage 7 — Empirical Connection</div>

    <div class="test-card" onclick="toggle(this)">
      <div class="card-header">
        <span class="badge badge-robust">Robustness</span>
        <span class="card-title">[How does the model connect to data — calibration, stylized facts, or reduced-form tests?]</span>
        <span class="card-num">S7</span>
        <span class="chevron">›</span>
      </div>
      <div class="card-body">
        <div class="row">
          <div class="cell">
            <div class="cell-label">What the paper does</div>
            <div class="cell-text">[Calibration moments chosen and values, reduced-form tests run, stylized facts matched, model-implied magnitudes reported]</div>
          </div>
          <div class="cell">
            <div class="cell-label">Critical questions</div>
            <div class="cell-text">Are the calibration moments the right ones to discipline the model — or are they chosen because they are easy to match? Do the model-implied magnitudes (elasticities, price levels, quantities) align with empirical estimates in the literature? Does the model make a distinguishing prediction that competing theories cannot also produce — i.e., is there a "smoking gun" test? Does the model work out-of-sample, generating correct predictions for phenomena outside its original scope?</div>
          </div>
        </div>
        <div class="row">
          <div class="cell">
            <div class="cell-label">Key equation</div>
            <div class="cell-eq">[Calibrated parameter values or model-implied moment equation, or "—"]</div>
          </div>
          <div class="cell">
            <div class="cell-label">Assessment</div>
            <div class="cell-text">[One-sentence verdict: does the model earn its connection to the real world, or is the empirical link superficial?]</div>
          </div>
        </div>
      </div>
    </div>
  </div>

</div>

<script>
function toggle(card) { card.classList.toggle('open'); }
</script>
```

### Writing discipline

- **Card titles**: sentence case, ≤ 12 words, describe the economic content not just the stage name. Good: "Agents maximize CARA utility subject to a borrowing constraint." Bad: "Setup."
- **Critical questions cell**: always write as questions (not assertions), 2–4 sentences. The questions should be the ones a referee at the *Journal of Finance* or *Review of Financial Studies* would actually ask.
- **Key equation cell**: if an equation appears, follow it immediately with a one-line plain-language gloss in parentheses. If none applies, write "—" rather than leaving blank.
- **Assessment cell**: one sentence only. Use language like "convincing," "underdeveloped," "load-bearing but untested," "a potential referee objection."
- **Stage numbering**: S1–S7 in order. Do not skip numbers; if a stage is absent from the paper, still include its card and note "Not addressed in the paper" in the What the paper does cell — this is itself a potential concern.
- **Mechanism callout box** (green): use in Stage 4 to force a one-sentence plain-language statement of the core mechanism. This is the single most important discipline in reading a theory paper — if the mechanism cannot be stated without math, that is a red flag.

---

## Tips for Efficient Reading (from Price 2019)

- **Know your goal**: Read some papers in full depth; skim others. If you're evaluating the identification strategy, focus there. If you're understanding how a paper fits the literature, focus on the introduction.
- **Use references strategically**: Papers that are frequently cited are worth investigating. Reading how later papers characterize an earlier paper can clarify its significance and assumptions.
- **Keep the big picture**: Don't lose the forest for the trees. The "story" of the paper should inform everything — sample construction, specification choice, robustness checks, and sequencing of results.
