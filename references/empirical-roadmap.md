# Empirical Roadmap — Widget Spec

Loaded by Step 6 of `SKILL.md` when the user requests a visual walkthrough of a paper's empirical architecture.

Produce an **interactive HTML widget** using the `show_widget` visualizer tool that renders all empirical tests as expandable cards, organized into logical phases that reflect the paper's internal narrative arc.

---

## What each card must contain

For each empirical test, populate four fields:

1. **What is the test** — the specification, dependent variable, variation used, and key fixed effects. Be precise enough that a reader could sketch the regression.
2. **Why we need it** — what identification challenge or alternative story this test addresses. Frame as: "without this test, a reader could object that…"
3. **Intuition** — the economic or statistical logic in plain language. What is the underlying thought experiment?
4. **Key takeaway** — the headline number or qualitative finding. For mechanism tests, note what the result rules in or rules out.

---

## How to group tests into phases

Read the paper's section structure and group tests into 4–6 phases that tell a coherent story:

| Phase | Purpose | Typical tests |
|-------|---------|--------------|
| **Documenting the phenomenon** | Establish that the thing being studied is real and large | Descriptive plots, time-series trends, summary statistics, hedonic/measurement models |
| **Causal effect estimation** | Identify the treatment effect causally | DiD, triple-DiD, IV/2SLS, RD, event studies |
| **Ruling out alternatives** | Falsify competing explanations | Quantity vs. price tests, placebo regressions, subgroup falsifications |
| **Mechanism: first channel** | Show evidence for the primary mechanism | Distribution moment tests, reserve/balance-sheet analyses |
| **Mechanism: second channel** | Show evidence for the secondary mechanism | Cross-sectional heterogeneity by constraint/exposure |
| **Robustness** | Confirm results are not artefacts of specification choices | Alternative cutoffs, windows, subsamples, dependent variables |

Not every paper has all six phases. Omit phases that don't apply; add phases if warranted (e.g., three distinct mechanisms → three mechanism phases).

---

## Badge color coding

| Badge | CSS class | Use when |
|-------|-----------|---------|
| `Descriptive` | `badge-desc` | Documents a fact, measures a quantity, or establishes a trend — no causal claim |
| `Causal` | `badge-causal` | Uses a research design (DiD, IV, RD) to establish a causal effect |
| `Falsification` | `badge-alt` | Designed to rule out an alternative explanation |
| `Mechanism` | `badge-mech` | Provides evidence for a specific channel or mechanism |

---

## HTML widget template

Copy this structure exactly. Repeat the `.test-card` pattern for each test; repeat the `.phase-group` + `.connector` pattern for each phase transition.

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
        <!-- Use green callout ONLY when this test's result feeds into a later test -->
        <div class="takeaway">
          <div class="takeaway-label">[Optional: feeds into T_]</div>
          [Name the later test this result enables — e.g., residuals used as IV in T3.]
        </div>
      </div>
    </div>
  </div>

  <!-- ── CONNECTOR ── -->
  <div class="connector">
    <div class="connector-line"></div>
    <span>[Logical bridge — e.g., "Phenomenon established → causal effect estimation"]</span>
    <div class="connector-line"></div>
  </div>

  <!-- ── PHASE 2 ── (repeat pattern) -->
  <div class="phase-group">
    <div class="phase-label">Phase 2 — [Phase name]</div>
    <!-- repeat .test-card blocks, changing badge class as needed -->
  </div>

</div>

<script>
function toggle(card) { card.classList.toggle('open'); }
</script>
```

---

## Writing discipline

- **Card titles**: sentence case, ≤ 10 words, descriptive of the design not just the topic. Good: "Triple-difference: add geographic exposure variation." Bad: "Triple difference."
- **Cell text**: 2–4 sentences each. Dense but scannable.
- **Phase labels**: sentence case, 3–6 words. Navigation anchors, not section headings.
- **Connector text**: one short phrase naming the logical transition, reads like a sentence fragment: "Causal effect confirmed → mechanism dissection."
- **Test numbering**: T1, T2, … in reading order across all phases.
- **Green callout box**: use only when a test's result is a direct input to a later test (e.g., measurement model residuals become an IV). Do not use as a general "important" callout — the Key takeaway cell serves that purpose.
