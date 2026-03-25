# Empirical Red Flags by Finance Sub-Field

A reference for field-specific methodological concerns. Load the relevant section
when evaluating empirical or mixed papers.

---

## Asset Pricing

- **Factor zoo**: Is the proposed factor / anomaly already spanned by known factors (FF3, FF5, q-factor, etc.)? Does the paper test against a comprehensive set of benchmarks?
- **Data mining**: Is the anomaly discovered in-sample and tested in-sample? Is there an out-of-sample test (either time-series holdout or international markets)?
- **Return predictability**: Are standard errors adjusted for persistence in predictors (Stambaugh 1999 bias)? Is in-sample R² economically significant or just statistically so?
- **Short-leg vs. long-leg**: Are returns driven by the short leg (hard-to-short stocks)? Is the result implementable after transaction costs?
- **Risk vs. mispricing**: Does the paper distinguish whether the return premium is compensation for risk or evidence of mispricing? Is the test convincing?
- **Measurement of expected returns**: Are return proxies (e.g., implied cost of capital) well-validated? Do results survive with alternative expected return measures?

---

## Asset Management

- **Survivorship bias**: Does the fund sample suffer from survivorship bias? Are dead/merged funds included?
- **Look-ahead bias**: Is fund-level information (e.g., holdings, fees, manager tenure) matched to returns without forward-looking contamination?
- **Flow-performance relationship**: Is the nonlinearity in the flow-performance relationship accounted for? Is there a convexity argument?
- **Benchmark assignment**: Is the benchmark to which fund performance is compared appropriate? Are results sensitive to benchmark choice?
- **Skill vs. luck**: Does the paper adequately distinguish managerial skill from luck? Bootstrap or false discovery rate methods are standard.
- **Horizon of evaluation**: Is the evaluation horizon appropriate? Short windows may capture noise; long windows introduce composition changes.

---

## Corporate Finance

- **Endogeneity of financial policy**: Capital structure, investment, and payout decisions are all endogenous. Is the identification strategy credible in ruling out reverse causality and omitted variables?
- **Measurement of investment opportunities**: Is Tobin's Q or a similar proxy measuring investment opportunities well, or is it contaminated by financial constraints or market mispricing?
- **Selection into treatment**: If studying a shock (e.g., credit supply, regulation), are treated and control firms comparable pre-shock? Are parallel trends assumptions tested?
- **Firm fixed effects**: Are firm fixed effects included where appropriate? Do results survive within-firm identification?
- **Sample period sensitivity**: Are results driven by a particular business cycle period (e.g., financial crisis, credit boom)?
- **Agency vs. efficiency**: When interpreting corporate decisions, does the paper distinguish between agency problems and efficient responses to information or constraints?

---

## Household Finance

- **Sample representativeness**: Administrative data (e.g., credit bureau, tax records) may over-represent certain demographics. Survey data (e.g., SCF, HRS) has known coverage gaps for top wealth holders.
- **Attrition and selection**: In panel data, is attrition selective? Does dropout correlate with outcomes of interest?
- **Measurement of financial literacy / preferences**: Self-reported financial knowledge and risk aversion are noisy. Are results robust to alternate measures?
- **Wealth vs. income effects**: Are income effects and wealth effects properly distinguished in consumption or portfolio responses?
- **Inertia and default effects**: Behavioral interpretations (inertia, present bias) should be tested against rational explanations (transaction costs, information acquisition).
- **Credit market access**: For credit-related outcomes, is the paper carefully distinguishing supply-side credit rationing from demand-side decisions?

---

## Banking & Financial Intermediation

- **Loan-level vs. bank-level**: Bank-level regressions can mask heterogeneity across loan types and borrowers. Is the right unit of observation used?
- **Supply vs. demand for credit**: Is the identification separating credit supply shifts (bank-side) from credit demand shifts (borrower-side)? Khwaja-Mian style within-borrower designs are the standard.
- **Regulatory endogeneity**: Regulatory changes are often endogenous to bank health or macroeconomic conditions. Is the timing and targeting of regulation handled carefully?
- **Interconnectedness**: In systemic risk papers, are network spillovers and second-order effects accounted for?
- **Internal capital markets**: For bank holding companies, are internal capital market allocations considered?

---

## Market Microstructure

- **Adverse selection vs. inventory**: Are bid-ask spread components properly attributed? Does the paper distinguish adverse selection costs from inventory management?
- **High-frequency data alignment**: Are trades and quotes properly aligned in time? Is the algorithm for classifying buyer- vs. seller-initiated trades (e.g., Lee-Ready) appropriate?
- **Market impact estimation**: Is price impact estimated with sufficient care for the direction and timing of trades?
- **Liquidity proxies**: If using low-frequency proxies for liquidity (Amihud, Roll), are the proxies validated for the specific setting?
- **Fragmentation and venue effects**: For multi-venue settings, is the paper accounting for order routing and venue selection?

---

## International Finance

- **Exchange rate regime**: Is the exchange rate regime (fixed, floating, managed) properly accounted for in the identification strategy?
- **Capital flow measurement**: Are gross vs. net capital flows distinguished? Are measurement issues in BOP data acknowledged?
- **Country fixed effects**: Are country-level time-invariant characteristics controlled for? Is the identification within-country over time?
- **Contagion vs. fundamentals**: In crisis papers, is contagion distinguished from fundamental co-movement?
- **Currency risk**: Is currency risk properly hedged or included in return calculations for international portfolio studies?

---

## Household Finance / Public Finance Intersection

*(Relevant for papers on education finance, employer benefits, tax-advantaged savings)*

- **Administrative vs. survey data**: IPEDS and similar administrative datasets are designed for compliance, not research. Selection into reporting, rounding conventions, and definitional changes over time all matter.
- **Program participation vs. eligibility**: Is the paper measuring actual take-up of a program, or just eligibility? Selection into take-up is a common confound.
- **Tax incidence**: When studying tax policy, is the paper considering who actually bears the incidence (workers, firms, consumers)?
- **Peer effects and general equilibrium**: Education and labor market interventions can have peer effects and general equilibrium effects that attenuate or amplify partial-equilibrium estimates.
