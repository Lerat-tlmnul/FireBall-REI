---
name: rei-2.0-max
description: Strict, extended, traceable REI pipeline (message → analysis → modeling → architecture → adversarial critique → construction → verification → counter-audit → delivery). Every stage is shown. Verification must reach 10/10 with every criterion fully met and proven. Unlimited looping until 10/10, with mandatory regression on every pass. For code, websites, reasoning, and high-stakes tasks where a flawless result is required.
---

# REI-2.0-Max — Strict, Extended, Traceable Pipeline

REI-2.0-Max keeps the single rule of REI-1.1-Max: **only a score of 10/10 permits delivery**. All stages are shown. The pipeline adds traceability, adversarial critique, explicit construction, counter-audit, and regression. There is no limit on the number of passes.

## What Changes from 1.1

- 9 stages instead of 5: modeling, construction, and counter-audit become full stages.
- Assumption register and ambiguity register, with impact and decision.
- Traceability matrix: requirement → sub-problem → component → proof.
- Multi-role adversarial critique and pre-mortem.
- Evidence register: no point without verifiable proof.
- Independent counter-audit that can invalidate a 10/10.
- Mandatory regression: every new pass replays the tests from previous passes.
- Depth levels to scale effort without ever lowering the 10/10 threshold.
- Stronger anti-inflation rules.

## Loop

message → analysis → modeling → architecture → adversarial critique → construction → verification → counter-audit → delivery

- If verification < 10 → FAIL: list every defect, then **restart at message**.
- If verification = 10 but the counter-audit finds a defect → the 10/10 is invalidated, **restart at message**.
- If verification = 10 and the counter-audit confirms → **delivery**.
- On every restart: state the pass number (“Pass 3”), the previous score, the full list of carried-forward defects, and how each one was fixed. Replay all tests from previous passes (regression).

## Output Format

Each stage uses a header:

**[1] Message**
**[2] Analysis**
**[3] Modeling**
**[4] Architecture**
**[5] Adversarial Critique**
**[6] Construction**
**[7] Verification**
**[8] Counter-Audit**
**[9] Delivery**

Each stage is structured and brief. Registers are presented as tables. Verified claims point to evidence.

## Depth Levels

Chosen at stage [1] and applied to all following stages. The 10/10 threshold never changes.

- **N1 — Simple**: short task, low risk. Critique and counter-audit are lighter but still real.
- **N2 — Standard**: default.
- **N3 — Deep**: critical code, complex reasoning, public website. Additional tests, full multi-role critique.
- **N4 — Maximal**: security, production, high stakes. Pre-mortem, reinforced counter-audit, extended regression tests, systematic security and accessibility review.

The depth level may never be used to avoid a verification: it only adds checks.

## Stage 1: Message

Restate the request in one or two sentences. List:

- **Goal**: what the result must accomplish.
- **Constraints**: language, format, length, technologies, audience, scope, explicit requirements.
- **Assumptions**: each explicit assumption, with confidence level (high / medium / low) and impact if false.
- **Ambiguities**: each ambiguity, the interpretation retained, its justification, the discarded alternative, and why. Never block: decide, document, continue.
- **Depth level** retained (N1–N4) and justification.
- **Expected deliverable** and, for code, the execution environment.
- **Exact acceptance conditions**: what must be true for the result to count as complete.

Produce the **assumption register** and the **ambiguity register**:

| # | Assumption | Confidence | Impact if false | Decision |
|---|---|---|---|---|

| # | Ambiguity | Interpretation retained | Alternative discarded | Reason |
|---|---|---|---|---|

## Stage 2: Analysis

Decompose the problem. Do not propose any solution at this stage.

- Split the request into numbered sub-problems (SP1, SP2, …).
- Mark what is **known**, **unknown**, and **must be checked**.
- List relevant rules, facts, APIs, and external constraints.
- List **failure points**: where a naive solution would break.
- **Websites**: visual requirements (layout, hierarchy, typography, color, spacing, responsiveness), content, interactions.
- **Reasoning**: premises, variables, possible interpretations, steps most likely to contain an error.
- **Code**: inputs/outputs, edge cases, errors to handle, dependencies, performance and security constraints.

Produce the initial **traceability matrix** (completed through delivery):

| Requirement | Sub-problem | Planned component | Expected proof |
|---|---|---|---|

## Stage 3: Modeling

Make the problem manipulable before designing.

- Formalize objects, inputs, outputs, states, and transitions.
- For reasoning: write premises, variables, relations, invariants, and the formal objective.
- For code: define types, contracts (preconditions, postconditions, invariants), and data structures.
- For a website: define the content model, information architecture, interface states, and user journeys.
- Identify edge cases and classify them (empty input, extreme value, concurrency, network failure, missing permission, etc.).
- Check that the model covers every sub-problem from stage [2]; report any gap.

Deliverable: a concise model (lists, tables, pseudo-structures) and the list of edge cases to handle.

## Stage 4: Architecture

Design the solution.

- Choose an approach and justify it against **at least one alternative** (cost, robustness, readability, performance, maintenance).
- Define the output structure: files and responsibilities for code; sections for explanations; steps for calculations or proofs.
- Map every sub-problem to a specific part of the structure.
- **Websites**: page sections, layout system, type scale, palette, breakpoints.
- **Code**: modules, interfaces, error handling, testing strategy.
- **Reasoning**: proof or calculation plan, order of steps, checkpoints.

Update the traceability matrix with the final components.

## Stage 5: Adversarial Critique

Attack the architecture before any construction.

- **Multi-role**: skeptical examiner, end user, attacker, maintainer, domain expert.
- **Pre-mortem**: imagine the result fails; list plausible causes and correct the architecture accordingly.
- Look for: logic errors, missing cases, unsupported claims, conflicts with constraints.
- **Code**: bugs, unhandled errors, security flaws, maintenance debt.
- **Websites**: visual weaknesses (hierarchy, spacing, contrast, generic styling) and technical issues (responsiveness, markup validity, accessibility).
- **Reasoning**: invalid inferences, hidden assumptions, unchecked calculations.
- Ask: “What is the strongest objection to this design, and does it survive?”

Revise the architecture to fix every flaw. List each flaw and its fix:

| # | Flaw identified | Role / method | Fix applied |
|---|---|---|---|

## Stage 6: Construction

Build the result from the revised architecture.

- Build each component in the order defined by the structure.
- Strictly respect the contracts and identified edge cases.
- For code: write complete, executable code with no TODOs or placeholders.
- For a website: produce complete, semantic, accessible HTML/CSS/JS.
- For reasoning: carry out the steps, keeping calculations verifiable.
- Do not invent: any unverifiable data is flagged as such.
- Record in the **evidence register** what was executed, tested, or recalculated.

| # | Evidence | Type (test / execution / recalculation / source) | Result |
|---|---|---|---|

## Stage 7: Verification

Evaluate the constructed result, then score it out of 10.

**For code and websites:**

| Criterion | Points | Full credit requires |
|---|---|---|
| Correctness | 3 | The code runs or the page renders without errors. Every requirement is met. Edge cases are handled and demonstrated. |
| Code quality | 2 | Valid syntax, clear naming, no dead code, no duplication, no security issues, consistent structure. |
| Visual quality | 3 | Clear hierarchy, consistent spacing and typography, coherent palette, good contrast, polished and non-generic result. |
| Responsiveness and accessibility | 2 | Works at mobile and desktop widths. Semantic HTML, labeled controls, readable contrast, keyboard navigation. |

**For reasoning:**

| Criterion | Points | Full credit requires |
|---|---|---|
| Correctness | 4 | Every fact, calculation, and inference is checked and holds. Uncertain points are flagged and do not affect the conclusion. |
| Completeness | 2 | Every sub-question from the analysis is fully answered. |
| Constraint compliance | 2 | Format, language, length, and scope match stage [1] exactly. |
| Clarity | 2 | Reasoning is easy to follow, with no contradictions and no padding. |

**Scoring rules for 10/10:**

- Each criterion is scored separately. Partial credit is allowed only if the missing part is explained and fixed in the next pass.
- A single unresolved defect in any criterion means the total is below 10.
- For each criterion, write the points awarded and a one-line justification with evidence (for code, the test or check performed; for reasoning, the recalculation or source).
- A check that was not performed cannot earn points. Perform it or do not award the score.

**Verification result:**

- Score 10: PASS provisionally, proceed to counter-audit.
- Score 9 or lower: FAIL. List every defect that cost points, then restart at stage [1].

## Stage 8: Counter-Audit

Independent audit of the result and of the stage [7] scoring. Goal: invalidate any undeserved 10/10.

- Replay regression tests from all previous passes.
- Verify that every row of the traceability matrix has real evidence in the evidence register.
- Check the scoring criterion by criterion: no point awarded without proof.
- Look for undetected defects: missed edge cases, partially met requirements, unverifiable claims, security flaws, accessibility issues.
- For code: run the tests, check error cases, review sensitive parts.
- For a website: check mobile and desktop rendering, markup validity, keyboard navigation, contrast.
- For reasoning: redo critical calculations, verify inferences, hunt hidden assumptions.

**Counter-audit verdict:**

- If a defect is found: the 10/10 is **invalidated**. List the defect, then restart at stage [1].
- If no defect is found: confirm the 10/10 and proceed to delivery.

| # | Check performed | Method | Result |
|---|---|---|---|

## Stage 9: Delivery

Deliver only the result that reached 10/10 and was confirmed by the counter-audit.

- Show the final score: **10/10**, with the breakdown by criterion.
- Show the counter-audit verdict: **confirmed**.
- Provide the complete final result, ready to use.
- Briefly recall the assumptions and ambiguities documented in stage [1].
- State the number of passes performed and the defects fixed across passes.
- Deliver nothing if the score is not 10/10 or if the counter-audit has not confirmed.

## Rules

- Stages run in order and each one is shown.
- The loop continues until the score is 10/10. There is no maximum number of passes.
- Never inflate a score. A real defect always costs points.
- Be honest about uncertainty. An unverifiable fact counts as a defect.
- No point without proof: a check that was not performed earns nothing.
- The counter-audit can invalidate a 10/10; its confirmation is mandatory before delivery.
- Regression is mandatory on every pass: previous tests are replayed.
- The depth level adds checks; it never reduces the 10/10 threshold.
- Deliver only the result that reached 10/10 and was confirmed by the counter-audit.
