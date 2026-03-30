# Theory Roadmap: Critical Reading Framework for Finance Theory Papers

This file is loaded by the finance-paper-reader skill when evaluating **Theoretical** papers
or the **theory sections of Mixed papers**. It structures the critique to follow the canonical
presentation order of a finance theory paper, so questions arise at the right moment in the read.

---

## How to Read a Theory Paper: The Canonical Arc

A finance theory paper moves through a predictable sequence. Read — and critique — in this order:

1. **Motivation & Question** — Why does this model need to exist?
2. **Setup** — Agents, preferences, endowments, timing, information
3. **Equilibrium / Solution Concept** — How is the model solved?
4. **Main Results & Propositions** — What does the model deliver?
5. **Comparative Statics** — How do outcomes change with parameters?
6. **Extensions & Robustness** — How fragile is the framework?
7. **Empirical Connection** — Does the model match or predict data?

At each stage, ask the questions below. Formulate all concerns as questions (not assertions)
so the underlying worry is self-evident.

---

## Stage 1 — Motivation & Question

The opening should establish *why existing models cannot answer this question* and *what new
economic insight this paper delivers*. Read critically:

1. **The gap**: Is the question the paper addresses genuinely unanswered by the existing
   literature? Is the claimed gap accurate, or does it mischaracterize prior work?

2. **The mechanism story**: Before the model is written down, does the introduction convey
   the core economic intuition in plain language? If the mechanism cannot be stated without
   math, that is a warning sign about the model's transparency.

3. **Stylized facts as discipline**: What empirical regularities motivate the model? Are those
   facts well-established, or are they fragile or contested? Could an alternative set of facts
   lead to a completely different model?

4. **First-order importance**: Is the phenomenon being modeled quantitatively significant?
   Would a reasonable economist care about the answer even if the model is correct?

5. **Literature positioning**: Does the paper correctly characterize the papers it is building
   on and departing from? Are there directly related models that are not cited?

---

## Stage 2 — Setup: Agents, Preferences, Endowments, Timing, Information

This is where most theory papers succeed or fail. Every modeling choice is a claim about the
world. Read each element with the question: *Is this assumption doing real work, or is it
just convenient?*

### 2A. Agents

1. **Who is in the model?** Are all economically relevant agents included? Would adding a
   third party (a regulator, a competitor, a second type of investor) materially change the
   results?

2. **Objective functions**: What do agents maximize? Is the assumed objective (expected
   utility, profit, welfare) appropriate for the agents being modeled? Are there missing
   motives — career concerns, loss aversion, social preferences, limited attention — that
   would plausibly matter in this setting?

3. **Homogeneity**: Are agents treated as identical within a class when heterogeneity would
   be important? Conversely, is heterogeneity introduced for tractability rather than
   economic necessity?

4. **Rationality**: Do agents have rational expectations, or is bounded rationality invoked?
   If rational expectations are assumed, is that a reasonable approximation for this setting?
   If bounded rationality is assumed, is the specific form well-motivated?

### 2B. Preferences and Technology

1. **Functional forms**: Are utility functions, production functions, or cost functions
   chosen for tractability (e.g., CARA utility, Cobb-Douglas) or because they genuinely
   capture the economics? What qualitative results would change under alternative
   functional forms?

2. **Risk preferences**: Is the treatment of risk (risk neutrality, CRRA, mean-variance)
   appropriate for the agents and setting? Does the model's risk structure match how
   real agents in this market behave?

3. **Discount rates and horizons**: Is the time horizon (finite vs. infinite) well-motivated?
   Are discount rates calibrated or merely assumed? Do results hinge on the horizon choice?

### 2C. Endowments and Market Structure

1. **Endowments**: Are initial endowments (wealth, assets, information) reasonable? Could
   the results be driven by a specific endowment structure rather than the proposed mechanism?

2. **Market completeness**: Are markets complete, incomplete, or segmented? Is this
   assumption the key friction or merely a background assumption? What would happen if
   markets were more (or less) complete?

3. **Competitive vs. strategic behavior**: Do agents take prices as given, or do they
   internalize their price impact? Is the choice of price-taking vs. strategic behavior
   appropriate for the market being studied?

### 2D. Timing and Information

1. **Timing**: Is the sequence of events (who moves when, what is observed before each
   action) economically plausible? Does the timing structure drive the results — i.e.,
   would a different ordering eliminate the main finding?

2. **Information structure**: What do agents know, and when do they know it? Is the
   information structure (symmetric, asymmetric, private signals, public signals) appropriate
   for the setting? Are the informational assumptions chosen to generate the result rather
   than to reflect reality?

3. **Commitment**: Can agents commit to future actions? If so, is commitment realistic?
   If not, how are time-inconsistency problems handled?

4. **Contracting environment**: Is the contracting space (complete contracts, incomplete
   contracts, observable but non-verifiable) well-motivated? Does the paper explain why
   parties cannot write the contracts that would eliminate the friction?

---

## Stage 3 — Equilibrium and Solution Concept

1. **Equilibrium concept**: Is the solution concept (Nash equilibrium, competitive
   equilibrium, rational expectations equilibrium, perfect Bayesian equilibrium) appropriate
   for the game structure? Is it the *right* equilibrium concept, or merely the most
   tractable one?

2. **Existence and uniqueness**: Do the authors establish that an equilibrium exists?
   If not, does this matter for the interpretation of results? If there are multiple
   equilibria, which one is selected and why? Is the selection criterion convincing?

3. **Tractability assumptions**: What assumptions are made purely for tractability (e.g.,
   quadratic costs, unit mass of agents, linear demand)? Would the qualitative results
   survive relaxing these?

4. **Fixed points and clearing conditions**: For market-clearing or fixed-point arguments,
   are the conditions reasonable? Are there cases where clearing might fail?

5. **Planner's problem**: If the paper characterizes an efficient allocation as a benchmark,
   is the social planner's problem well-defined? Is the welfare criterion appropriate?

---

## Stage 4 — Main Results and Propositions

This is the heart of the paper. For each main proposition, ask:

1. **Claim clarity**: Is the proposition stated precisely? Are all variables and parameters
   defined? Could the result be misinterpreted due to imprecise language?

2. **Driving force**: What is the single economic force that generates this result? Can
   the mechanism be stated in one sentence without math? If not, why not?

3. **Mechanical vs. economic**: Is the result a deep economic insight, or does it follow
   mechanically from the setup? A result is mechanical if it is essentially assumed rather
   than derived — e.g., if the friction is parameterized in a way that directly maps to
   the outcome.
   - *Red flag*: The model delivers exactly the prediction it was built to deliver,
     with no surprising or non-obvious implications.

4. **Generality**: Under what conditions does the result hold? Are those conditions
   general or knife-edge? What breaks the result?

5. **Sign and direction**: Does the model deliver a clear directional prediction? Is the
   sign of the key comparative static surprising and non-obvious — or would any reasonable
   model deliver the same sign?

6. **New vs. repackaged**: Does the paper's main result say something qualitatively new,
   or does it restate a known result in a new notation?

---

## Stage 5 — Comparative Statics

Comparative statics are where theory papers earn their empirical credibility. Scrutinize:

1. **Economic content**: Are the comparative statics the ones an empiricist would actually
   test? Do the parameters being varied correspond to measurable quantities?

2. **Direction and magnitude**: Are the signs of comparative statics economically
   intuitive? Are there cases where the sign is ambiguous — and does the paper honestly
   acknowledge this?

3. **Non-monotonicity**: Does the model predict non-monotone relationships (e.g., an
   inverted-U)? If so, is this empirically plausible, and has the paper verified it
   against data?

4. **Parameter sensitivity**: Are the main predictions robust to parameter perturbations,
   or do they rely on specific parameter ranges? A result that holds only for extreme
   parameter values is suspect.

5. **Missing comparative statics**: Are there natural comparative statics the paper does
   *not* report? If so, is that because they are ambiguous or contrary to the paper's story?

---

## Stage 6 — Extensions and Robustness

1. **Key simplifications**: What are the 2–3 most important simplifying assumptions in
   the baseline model? Does the paper relax each of them in extensions? If not, which
   relaxations would be most threatening?

2. **Dynamic vs. static**: If the model is static (or two-period), what is lost by not
   solving a fully dynamic model? Does the paper acknowledge this?

3. **General equilibrium effects**: If the model is partial equilibrium, are there
   plausible general equilibrium feedbacks that could reverse or attenuate the results?

4. **Heterogeneity**: Does the model's mechanism survive when agents are heterogeneous?
   Many results that hold in representative-agent models break down with heterogeneity.

5. **Alternative frictions**: Are there other frictions — not in the model — that could
   generate the same predictions? If so, the model's mechanism may not be identified
   even if the empirical predictions are confirmed.

---

## Stage 7 — Empirical Connection

Theory papers are ultimately judged on whether they illuminate real phenomena. Ask:

1. **Disciplining moments**: What data moments were used to motivate or calibrate the
   model? Are these moments the right ones — the most informative about the mechanism —
   or were they chosen because the model fits them well?

2. **Calibration discipline**: If the model is calibrated, are the parameter values
   taken from prior literature or estimated independently? Are they reasonable?
   Does the calibrated model match moments it was *not* targeted to match?

3. **Untested predictions**: Does the model make predictions the paper does not test?
   Are some of those predictions potentially falsifiable — and would the authors test them
   if they were falsified?

4. **Distinguishing from alternatives**: Does the paper identify a prediction that is
   unique to this model and cannot be generated by competing theories? This is the
   strongest form of empirical discipline for a theory paper.

5. **Out-of-sample validity**: Does the model generate implications for settings,
   time periods, or countries outside the original calibration? Have these been checked?

---

## Finance Sub-Field Theory Conventions

Different sub-fields have settled conventions for what a theory paper must deliver.
Evaluate against the relevant standard:

### Asset Pricing
- Must price at least one asset or portfolio correctly; SDF/stochastic discount factor
  derivation is expected.
- Equity premium, risk-free rate, and return volatility are standard calibration moments.
- *Key question*: Does the SDF have plausible volatility (Hansen-Jagannathan bound)?

### Corporate Finance
- Must model a friction (asymmetric information, agency, incomplete contracts) that
  explains why the Modigliani-Miller irrelevance theorem fails.
- *Key question*: Is the friction the smallest necessary departure from MM, or is it
  over-engineered?

### Market Microstructure
- Must specify an information structure and market mechanism (auction, dealer, limit
  order book).
- *Key question*: Is the price formation mechanism realistic for the market being studied?

### Banking & Intermediation
- Must explain why financial intermediaries exist (liquidity transformation, monitoring,
  information production).
- *Key question*: Why can't markets do what the intermediary does?

### Household Finance / Behavioral
- Must specify deviations from standard preferences precisely (loss aversion, present
  bias, inattention).
- *Key question*: Is the behavioral assumption well-identified, or is it a reduced-form
  stand-in for a missing constraint?

---

## Common Theory Paper Failure Modes

Flag these when present:

| Failure Mode | Signal |
|-------------|--------|
| **Assumption = Result** | The main proposition is essentially stated in the setup; no non-trivial derivation |
| **Kitchen sink model** | So many ingredients that the mechanism cannot be isolated |
| **Knife-edge equilibrium** | Result holds only at a specific parameter value or under a precise functional form |
| **Missing benchmark** | No comparison to a frictionless / first-best case, so welfare loss is unquantified |
| **Untestable mechanism** | Model generates correct predictions, but the mechanism cannot be distinguished from alternatives |
| **Calibration to fit** | Parameters chosen to match targeted moments; no out-of-sample validation |
| **Missing agent** | A natural counterparty or third party is absent, and its absence drives the result |
| **Timing drives everything** | Results would reverse under a slightly different information or action sequence |
