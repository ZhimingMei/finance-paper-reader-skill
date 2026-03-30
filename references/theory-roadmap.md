# Theory Roadmap — Widget Specification

Loaded by Step 7 of `SKILL.md` when the user requests a visual walkthrough of a theory paper's
model architecture. Follow every instruction here to produce the interactive expandable-card
widget via the `show_widget` visualizer tool.

---

## The canonical theory paper arc

Finance theory papers follow a predictable presentation sequence. Map each section of the paper
onto these seven stages in order:

| Stage | Purpose | What to look for |
|-------|---------|-----------------|
| **S1 — Motivation & Question** | Establish the economic puzzle and why existing models cannot explain it | Stylized facts cited, claimed gap in literature, verbal mechanism sketch |
| **S2 — Environment & Setup** | Define agents, preferences, endowments, technology, timing, information | Objective functions, constraints, parameter definitions, timeline diagram |
| **S3 — Equilibrium** | Solve for equilibrium prices, quantities, allocations | Solution concept stated, existence/uniqueness, market-clearing conditions |
| **S4 — Main Results** | State and interpret the key propositions | Proposition statements, economic intuition, key equations |
| **S5 — Comparative Statics** | Show how equilibrium outcomes change with parameters | Signs of derivatives, threshold conditions, non-monotonicities |
| **S6 — Extensions & Robustness** | Relax key assumptions; check generality | Load-bearing assumptions identified, GE effects, heterogeneity |
| **S7 — Empirical Connection** | Link model predictions to data | Calibration moments, reduced-form tests, distinguishing predictions |

---

## What each card must contain

For each stage, populate four fields:

1. **What the paper does** — what the authors actually write at this stage: the specific
   assumptions made, propositions stated, or exercises run. Precise enough that a reader
   could locate it in the paper.
2. **Critical questions** — the 2–3 sharpest referee questions for this stage, framed as
   questions (not assertions). See per-stage guidance below.
3. **Key equation** — if this stage has a central equation (agent's problem, equilibrium
   condition, main comparative static), display it in LaTeX-style math followed by a
   one-line plain-language gloss. Write "—" if the stage is purely verbal.
4. **Assessment** — one sentence only: is this stage convincing, underdeveloped,
   load-bearing but untested, or a potential referee objection?

### Per-stage critical question guidance

**S1 — Motivation**
- Is the stylized fact well-established, or is it prone to measurement error or contested?
- Is the claimed gap real — could an existing model explain the phenomenon with minor modification?
- Is the verbal mechanism stated clearly before the math, or does it only become legible after reading the propositions?

**S2 — Setup**
- Is every assumption doing real economic work, or are some present only for tractability?
- Is the objective function reasonable — are there missing motives (risk aversion, learning, limited attention, career concerns)?
- Does the timing of moves (who acts first, what is observable when) match the real-world setting, or does it drive the result?

**S3 — Equilibrium**
- Is the solution concept (Nash, competitive, rational expectations) appropriate for the game structure?
- Is the equilibrium unique? If multiple equilibria exist, is the selection criterion economically motivated or merely convenient?
- Are the equilibrium conditions interpretable without tracing through all the algebra?

**S4 — Main Results**
- Is this a deep economic insight or a mechanical consequence of the functional form assumed in S2?
- Can the driving force be stated in one sentence without math — if not, why not?
- Would the result disappear if a single assumption were changed — and is that assumption realistic?

**S5 — Comparative Statics**
- Are the signs of comparative statics unambiguous, or do they depend on parameter restrictions that may not hold empirically?
- If there is a non-monotonicity, is it economically plausible or a modeling artifact?
- Are the parameters being varied observable and measurable, so the comparative statics can be taken to data?

**S6 — Extensions**
- Which simplifying assumption from S2 is most load-bearing for the main result — and is it addressed here?
- What happens in general equilibrium when prices adjust endogenously?
- Does the result survive when agents are heterogeneous in ways that matter for this setting?

**S7 — Empirical Connection**
- Are the calibration moments the right ones to discipline the model, or were they chosen because the model fits them well?
- Do the model-implied magnitudes (elasticities, price levels, quantities) align with empirical estimates in the literature?
- Does the model make a distinguishing prediction that competing theories cannot also produce?

---

## Badge color coding

| Badge | CSS class | Use when |
|-------|-----------|---------|
| `Setup` | `badge-setup` | Defining the environment — agents, preferences, timing (S1, S2) |
| `Result` | `badge-result` | Propositions, lemmas, equilibrium characterization (S3, S4) |
| `Mechanism` | `badge-mech` | Comparative statics, economic intuition, channel identification (S5) |
| `Robustness` | `badge-robust` | Extensions, assumption sensitivity, empirical connection (S6, S7) |

---

## HTML widget template

Use this structure exactly — it mirrors the empirical roadmap for visual consistency. Repeat
the `.stage-card` block for each of the seven stages. Include all seven stages; if the paper
skips one, note "Not addressed in the paper" in the What the paper does cell — the absence
is itself informative.

```html
<style>
  * { box-sizing: border-box; }
  .roadmap { padding: 16px 0 24px; font-family: var(--font-sans); }
  .phase-label {
    font-size: 11px; font-weight: 500; letter-spacing: 0.06em; text-transform: uppercase;
    color: var(--color-text-tertiary); margin: 0 0 8px 0; padding-left: 4px;
  }
  .stage-card {
    border: 0.5px solid var(--color-border-tertiary);
    border-radius: var(--border-radius-lg);
    background: var(--color-background-secondary);
    margin-bottom: 10px; overflow: hidden;
    transition: border-color 0.15s; cursor: pointer;
  }
  .stage-card:hover { border-color: var(--color-border-primary); }
  .stage-card.open { border-color: var(--color-border-secondary); }
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
  .stage-card.open .chevron { transform: rotate(90deg); }
  .card-body {
    display: none; padding: 0 14px 14px;
    border-top: 0.5px solid var(--color-border-tertiary);
  }
  .stage-card.open .card-body { display: block; }
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
  .mechanism-box {
    margin-top: 10px; border-radius: var(--border-radius-md);
    padding: 10px 12px; background: #E1F5EE;
    border-left: 3px solid #1D9E75;
    font-size: 13px; line-height: 1.55; color: #085041;
  }
  @media (prefers-color-scheme: dark) {
    .mechanism-box { background: #04342C; border-left-color: #5DCAA5; color: #9FE1CB; }
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
    <div class="phase-label">S1 — Motivation & Question</div>
    <div class="stage-card" onclick="toggle(this)">
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
            <div class="cell-text">[Stylized facts cited; gap in literature claimed; verbal mechanism sketch in the introduction]</div>
          </div>
          <div class="cell">
            <div class="cell-label">Critical questions</div>
            <div class="cell-text">[2–3 referee-level questions for this stage — see per-stage guidance above]</div>
          </div>
        </div>
        <div class="row">
          <div class="cell">
            <div class="cell-label">Key equation</div>
            <div class="cell-eq">[LaTeX equation if applicable, or "—"]</div>
          </div>
          <div class="cell">
            <div class="cell-label">Assessment</div>
            <div class="cell-text">[One sentence: convincing / underdeveloped / load-bearing but untested / potential referee objection]</div>
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
    <div class="phase-label">S2 — Environment & Setup</div>
    <div class="stage-card" onclick="toggle(this)">
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
            <div class="cell-text">[Who are the agents; what do they maximize; what are the constraints; what is the timing and information structure]</div>
          </div>
          <div class="cell">
            <div class="cell-label">Critical questions</div>
            <div class="cell-text">[2–3 referee-level questions — see per-stage guidance above]</div>
          </div>
        </div>
        <div class="row">
          <div class="cell">
            <div class="cell-label">Key equation</div>
            <div class="cell-eq">[Agent's optimization problem or budget constraint — LaTeX + one-line gloss]</div>
          </div>
          <div class="cell">
            <div class="cell-label">Assessment</div>
            <div class="cell-text">[One sentence verdict]</div>
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
    <div class="phase-label">S3 — Equilibrium</div>
    <div class="stage-card" onclick="toggle(this)">
      <div class="card-header">
        <span class="badge badge-result">Result</span>
        <span class="card-title">[Solution concept, existence, uniqueness]</span>
        <span class="card-num">S3</span>
        <span class="chevron">›</span>
      </div>
      <div class="card-body">
        <div class="row">
          <div class="cell">
            <div class="cell-label">What the paper does</div>
            <div class="cell-text">[Solution concept used; equilibrium conditions stated; how multiplicity is handled if it arises]</div>
          </div>
          <div class="cell">
            <div class="cell-label">Critical questions</div>
            <div class="cell-text">[2–3 referee-level questions — see per-stage guidance above]</div>
          </div>
        </div>
        <div class="row">
          <div class="cell">
            <div class="cell-label">Key equation</div>
            <div class="cell-eq">[Equilibrium condition or market-clearing equation — LaTeX + one-line gloss]</div>
          </div>
          <div class="cell">
            <div class="cell-label">Assessment</div>
            <div class="cell-text">[One sentence verdict]</div>
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
    <div class="phase-label">S4 — Main Results</div>
    <div class="stage-card" onclick="toggle(this)">
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
            <div class="cell-text">[State the proposition(s) in plain language — what the model claims is true and the intuition given for why]</div>
          </div>
          <div class="cell">
            <div class="cell-label">Critical questions</div>
            <div class="cell-text">[2–3 referee-level questions — see per-stage guidance above]</div>
          </div>
        </div>
        <div class="row">
          <div class="cell">
            <div class="cell-label">Key equation</div>
            <div class="cell-eq">[Main proposition equation or key comparative static — LaTeX + one-line gloss]</div>
          </div>
          <div class="cell">
            <div class="cell-label">Assessment</div>
            <div class="cell-text">[One sentence verdict]</div>
          </div>
        </div>
        <!-- Green callout: always include for S4. Forces a one-sentence mechanism statement. -->
        <div class="mechanism-box">
          <div class="mechanism-label">Mechanism in one sentence</div>
          [Complete this: "The result holds because [economic force A] dominates [economic force B]
          when [condition C] is satisfied." If you cannot complete this sentence without math,
          that is itself a concern about the paper's transparency.]
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
    <div class="phase-label">S5 — Comparative Statics</div>
    <div class="stage-card" onclick="toggle(this)">
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
            <div class="cell-text">[Which parameters are varied; direction and sign of effects; any threshold conditions or non-monotonicities]</div>
          </div>
          <div class="cell">
            <div class="cell-label">Critical questions</div>
            <div class="cell-text">[2–3 referee-level questions — see per-stage guidance above]</div>
          </div>
        </div>
        <div class="row">
          <div class="cell">
            <div class="cell-label">Key equation</div>
            <div class="cell-eq">[Key derivative or threshold condition — LaTeX + one-line gloss]</div>
          </div>
          <div class="cell">
            <div class="cell-label">Assessment</div>
            <div class="cell-text">[One sentence verdict]</div>
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
    <div class="phase-label">S6 — Extensions & Robustness</div>
    <div class="stage-card" onclick="toggle(this)">
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
            <div class="cell-text">[Which assumptions are relaxed; what extensions are considered — heterogeneity, dynamics, general equilibrium, alternative information structures]</div>
          </div>
          <div class="cell">
            <div class="cell-label">Critical questions</div>
            <div class="cell-text">[2–3 referee-level questions — see per-stage guidance above]</div>
          </div>
        </div>
        <div class="row">
          <div class="cell">
            <div class="cell-label">Key equation</div>
            <div class="cell-eq">[Modified condition under extension — LaTeX + gloss, or "—"]</div>
          </div>
          <div class="cell">
            <div class="cell-label">Assessment</div>
            <div class="cell-text">[One sentence verdict]</div>
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
    <div class="phase-label">S7 — Empirical Connection</div>
    <div class="stage-card" onclick="toggle(this)">
      <div class="card-header">
        <span class="badge badge-robust">Robustness</span>
        <span class="card-title">[Calibration, stylized facts matched, distinguishing predictions]</span>
        <span class="card-num">S7</span>
        <span class="chevron">›</span>
      </div>
      <div class="card-body">
        <div class="row">
          <div class="cell">
            <div class="cell-label">What the paper does</div>
            <div class="cell-text">[Calibration moments chosen and values; reduced-form tests run; stylized facts matched; model-implied magnitudes reported]</div>
          </div>
          <div class="cell">
            <div class="cell-label">Critical questions</div>
            <div class="cell-text">[2–3 referee-level questions — see per-stage guidance above]</div>
          </div>
        </div>
        <div class="row">
          <div class="cell">
            <div class="cell-label">Key equation</div>
            <div class="cell-eq">[Calibrated parameter values or model-implied moment equation, or "—"]</div>
          </div>
          <div class="cell">
            <div class="cell-label">Assessment</div>
            <div class="cell-text">[One sentence verdict]</div>
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

- **Card titles**: sentence case, ≤12 words, describe the economic content not just the stage
  name. Good: *"Agents maximize CARA utility subject to a borrowing constraint."* Bad: *"Setup."*
- **Critical questions cell**: always 2–3 questions, framed as questions. Use the per-stage
  guidance above — these should be the questions a JF or RFS referee would actually ask.
- **Key equation cell**: follow every equation immediately with a one-line plain-language gloss
  in parentheses. Write "—" rather than leaving blank.
- **Assessment cell**: one sentence only. Use: "convincing," "underdeveloped," "load-bearing
  but untested," "a potential referee objection."
- **Stage numbering**: S1–S7 in order. Never skip a number — if a stage is absent from the
  paper, include the card and note "Not addressed in the paper" in the What the paper does cell.
- **Mechanism callout** (S4 only): always include the green box in S4. Force a one-sentence
  plain-language mechanism statement. This is the single most important discipline in reading
  a theory paper — inability to complete the sentence without math is a red flag.
