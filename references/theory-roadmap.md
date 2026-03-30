# Theory Roadmap — Widget Spec

Loaded by Step 7 of `SKILL.md` when the user requests a visual walkthrough of a theoretical paper's model architecture.

Produce an **interactive HTML widget** using the `show_widget` visualizer tool that renders each stage of the theory paper as an expandable card, following the canonical arc that finance economists use to present models.

---

## The canonical theory paper arc

Map each section of the paper onto these seven stages in order:

| Stage | Purpose | What to look for |
|-------|---------|-----------------|
| **S1 — Motivation & Question** | Establish the economic puzzle and why existing models cannot explain it | Stylized facts cited, gap in literature, verbal mechanism sketch |
| **S2 — Environment & Setup** | Define agents, preferences, endowments, technology, timing, information | Objective functions, constraints, parameter definitions, timeline |
| **S3 — Equilibrium** | Solve for equilibrium prices, quantities, allocations | Solution concept, existence/uniqueness, equilibrium conditions |
| **S4 — Main Results** | State and interpret the key propositions | Propositions/lemmas, economic intuition, key equations |
| **S5 — Comparative Statics** | Show how equilibrium outcomes change with parameters | Signs of derivatives, threshold conditions, non-monotonicities |
| **S6 — Extensions & Robustness** | Relax key assumptions; check generality | Which assumptions are load-bearing, GE effects, heterogeneity |
| **S7 — Empirical Connection** | Link model predictions to data | Calibration moments, reduced-form tests, distinguishing predictions |

---

## What each card must contain

For each stage, populate four fields:

1. **What the paper does** — what the authors actually write at this stage: specific assumptions made, propositions stated, exercises run. Precise enough that a reader can locate it in the paper.
2. **Critical questions** — the 2–3 sharpest questions a JF/RFS referee would ask at this stage, from Oh (2024). Always written as questions, not assertions. Examples by stage:
   - *Setup*: "Is it reasonable to assume agents maximize X while ignoring Y?" / "Does a two-period model miss important dynamics?"
   - *Equilibrium*: "Is the equilibrium unique, and if not, how is multiplicity resolved?" / "Does the solution concept fit the setting?"
   - *Results*: "Is this proposition a deep insight or a mechanical consequence of the assumed functional form?" / "Can the driving force be stated in one sentence without math?"
   - *Comparative statics*: "Are the signs unambiguous, or do they depend on parameter restrictions that may not hold empirically?"
   - *Extensions*: "Which simplifying assumption is most load-bearing for the main result?" / "What happens in general equilibrium?"
   - *Empirical connection*: "Are the calibration moments the right ones to discipline the model?" / "Does the model make a prediction that competing theories cannot also produce?"
3. **Key equation** — if this stage has a central equation (agent's problem, equilibrium condition, main comparative static), display it in LaTeX-style math followed by a one-line plain-language gloss. Write "—" if the stage is purely verbal.
4. **Assessment** — one sentence: is this stage convincing, load-bearing, underdeveloped, or a potential referee objection?

---

## Badge color coding

| Badge | CSS class | Use when |
|-------|-----------|---------|
| `Setup` | `badge-setup` | Defining the environment, agents, preferences, timing |
| `Result` | `badge-result` | Propositions, lemmas, equilibrium characterization |
| `Mechanism` | `badge-mech` | Comparative statics, economic intuition, channel identification |
| `Robustness` | `badge-robust` | Extensions, sensitivity to assumptions, empirical connection |

---

## HTML widget template

Copy this structure exactly. One card per stage (S1–S7). Do not skip stages — if a stage is absent from the paper, include its card and note "Not addressed in the paper" in the What the paper does cell.

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
  .cell-eq   { font-size: 13px; line-height: 1.7;  color: var(--color-text-secondary); font-style: italic; }
  .mechanism {
    margin-top: 10px; border-radius: var(--border-radius-md);
    padding: 10px 12px; background: #E1F5EE;
    border-left: 3px solid #1D9E75;
    font-size: 13px; line-height: 1.55; color: #085041;
  }
  @media (prefers-color-scheme: dark) {
    .mechanism { background: #04342C; border-left-color: #5DCAA5; color: #9FE1CB; }
  }
  .mechanism-label { font-weight: 500; margin-bottom: 3px; }
  .connector {
    display: flex; align-items: center; gap: 8px;
    padding: 4px 14px; color: var(--color-text-tertiary); font-size: 12px;
  }
  .connector-line { flex: 1; height: 0.5px; background: var(--color-border-tertiary); }
  .phase-group { margin-bottom: 4px; }
</style>

<div class="roadmap">

  <!-- ── S1 — MOTIVATION ── -->
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
            <div class="cell-text">[Stylized facts cited, gap in literature, verbal mechanism sketch]</div>
          </div>
          <div class="cell">
            <div class="cell-label">Critical questions</div>
            <div class="cell-text">Is the stylized fact well-established or prone to measurement error? Is the gap in the literature real — could an existing model explain the phenomenon with minor modification? Is the verbal mechanism stated clearly before the math, or does it only emerge after the propositions?</div>
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

  <!-- ── S2 — SETUP ── -->
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
            <div class="cell-text">Is every assumption doing real economic work, or are some present only for tractability? Is the objective function reasonable — are there missing motives (risk aversion, learning, limited attention)? Does the timing of moves match the real-world institutional setting?</div>
          </div>
        </div>
        <div class="row">
          <div class="cell">
            <div class="cell-label">Key equation</div>
            <div class="cell-eq">[Agent's optimization problem or budget constraint in LaTeX, + one-line gloss]</div>
          </div>
          <div class="cell">
            <div class="cell-label">Assessment</div>
            <div class="cell-text">[One-sentence verdict: are assumptions well-motivated or merely convenient?]</div>
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

  <!-- ── S3 — EQUILIBRIUM ── -->
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
            <div class="cell-text">[Solution concept used (Nash, competitive, rational expectations), equilibrium conditions stated, how multiplicity is handled]</div>
          </div>
          <div class="cell">
            <div class="cell-label">Critical questions</div>
            <div class="cell-text">Is the solution concept appropriate — does Nash make sense if players are atomistic? Is the equilibrium unique? If multiple equilibria exist, is the selection criterion economically motivated or merely convenient? Are the equilibrium conditions interpretable without tracing through all the algebra?</div>
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

  <!-- ── S4 — MAIN RESULTS ── -->
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
            <div class="cell-text">[State the proposition(s) in plain language — what is the paper claiming is true in the model, and what intuition is given]</div>
          </div>
          <div class="cell">
            <div class="cell-label">Critical questions</div>
            <div class="cell-text">Is this a deep economic insight or a mechanical consequence of the functional form chosen in Stage 2? Can the driving force be stated in one sentence without math? Would the result disappear if a single assumption were changed — and is that assumption realistic? Is the result surprising relative to the existing literature?</div>
          </div>
        </div>
        <div class="row">
          <div class="cell">
            <div class="cell-label">Key equation</div>
            <div class="cell-eq">[Main proposition equation or key expression in LaTeX, + one-line gloss]</div>
          </div>
          <div class="cell">
            <div class="cell-label">Assessment</div>
            <div class="cell-text">[One-sentence verdict: genuine insight or known result re-dressed?]</div>
          </div>
        </div>
        <!-- Mechanism callout: REQUIRED for Stage 4 -->
        <div class="mechanism">
          <div class="mechanism-label">Mechanism in one sentence</div>
          [Complete: "The result holds because [economic force A] dominates [economic force B] when [condition C] is satisfied." If you cannot complete this sentence without math, that is itself a red flag about the paper's transparency.]
        </div>
      </div>
    </div>
  </div>

  <div class="connector">
    <div class="connector-line"></div>
    <span>Results established → parameter sensitivity</span>
    <div class="connector-line"></div>
  </div>

  <!-- ── S5 — COMPARATIVE STATICS ── -->
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
            <div class="cell-text">[Which parameters are varied, direction and sign of effects, threshold conditions or non-monotonicities]</div>
          </div>
          <div class="cell">
            <div class="cell-label">Critical questions</div>
            <div class="cell-text">Are the signs of the comparative statics unambiguous, or do they depend on parameter restrictions that may not hold empirically? If there is a non-monotonicity, is it economically plausible or a modeling artifact? Are the key parameters observable — i.e., can the comparative statics be taken to data? Does varying a "key" parameter actually change the mechanism, or just scale the effect?</div>
          </div>
        </div>
        <div class="row">
          <div class="cell">
            <div class="cell-label">Key equation</div>
            <div class="cell-eq">[Key derivative or threshold condition in LaTeX, + one-line gloss]</div>
          </div>
          <div class="cell">
            <div class="cell-label">Assessment</div>
            <div class="cell-text">[One-sentence verdict: are comparative statics empirically meaningful and unambiguous?]</div>
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

  <!-- ── S6 — EXTENSIONS ── -->
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
            <div class="cell-text">[Which assumptions are relaxed — heterogeneity, dynamics, general equilibrium, alternative information structures]</div>
          </div>
          <div class="cell">
            <div class="cell-label">Critical questions</div>
            <div class="cell-text">Which simplifying assumption from Stage 2 is most load-bearing — and is it addressed here? What happens in general equilibrium when prices adjust endogenously? Would heterogeneity across agents (risk aversion, wealth, information) strengthen or weaken the result? Are there missing extensions a referee would immediately flag?</div>
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

  <!-- ── S7 — EMPIRICAL CONNECTION ── -->
  <div class="phase-group">
    <div class="phase-label">Stage 7 — Empirical Connection</div>
    <div class="test-card" onclick="toggle(this)">
      <div class="card-header">
        <span class="badge badge-robust">Robustness</span>
        <span class="card-title">[Calibration, stylized facts matched, or reduced-form tests]</span>
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
            <div class="cell-text">Are the calibration moments the right ones to discipline the model, or chosen because they are easy to match? Do model-implied magnitudes (elasticities, price levels, quantities) align with empirical estimates in the literature? Does the model make a distinguishing prediction that competing theories cannot also produce? Does the model work out-of-sample?</div>
          </div>
        </div>
        <div class="row">
          <div class="cell">
            <div class="cell-label">Key equation</div>
            <div class="cell-eq">[Calibrated parameter values or model-implied moment, or "—"]</div>
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

---

## Writing discipline

- **Card titles**: sentence case, ≤ 12 words, describe the economic content not just the stage name. Good: "Agents maximize CARA utility subject to a borrowing constraint." Bad: "Setup."
- **Critical questions cell**: always written as questions, 2–4 sentences. The questions a JF/RFS referee would actually ask.
- **Key equation cell**: follow every equation with a one-line plain-language gloss. Write "—" if none applies.
- **Assessment cell**: one sentence only. Use language like "convincing," "underdeveloped," "load-bearing but untested," "a potential referee objection."
- **Stage numbering**: S1–S7 in order. Never skip — if a stage is absent from the paper, include the card and note "Not addressed in the paper" in What the paper does. Absence is itself a concern.
- **Mechanism callout** (green box, Stage 4 only): forces a one-sentence plain-language statement of the core mechanism. If this sentence cannot be written without math, flag it explicitly — that is a transparency failure in the paper.
