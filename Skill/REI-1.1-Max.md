---
name: rei-1.1-max
description: REI reasoning pipeline, strict variant, for code and reasoning tasks (message → analysis → architecture → critique → verification). Shows each stage. Verification must reach 10/10 with every criterion fully met. Loops without limit until 10/10. Use for code, websites, and reasoning tasks where a flawless result is required.
---

# REI-1.1-Max: Strict Visible Reasoning Pipeline

REI-1.1-Max runs the REI pipeline with a single pass condition: a verification score of 10/10. Every stage is shown to the user. Verification scores the result out of 10 across the criteria below. A score of 9 or lower is a failure. The loop restarts from the message stage with the full list of defects, and it has no limit on passes. It ends only at 10/10.

Flow:

message → analysis → architecture → critique → verification

If score < 10 → restart at message.
If score = 10 → deliver the final result.

## Output format

Each stage uses a header:

**[1] Message**
**[2] Analysis**
**[3] Architecture**
**[4] Critique**
**[5] Verification**

Keep each stage structured and brief. After a restart, label the pass (for example "Pass 3"), give the previous score, list every defect carried forward, and state how each one was fixed.

## Stage 1: Message

Restate the request in one or two sentences. List:

- The goal.
- The constraints: language, format, length, technologies, audience, scope, explicit requirements.
- The assumptions, each stated explicitly.
- The expected deliverable and, for code, the environment.
- The exact acceptance conditions: what must be true for the result to count as complete.

## Stage 2: Analysis

Decompose the problem. Do not propose a solution yet.

- Split the request into sub-problems.
- Mark what is known, unknown, and must be checked.
- List the relevant rules, facts, and APIs.
- List the failure points, where a naive solution would break.
- For websites: visual requirements (layout, hierarchy, typography, color, spacing, responsiveness), content, and interactions.
- For reasoning: premises, variables, possible interpretations, and the steps most likely to contain an error.

## Stage 3: Architecture

Design the solution.

- Choose an approach and justify it against at least one alternative.
- Define the output structure: files and responsibilities for code, sections for explanations, steps for calculations or proofs.
- Map every sub-problem to a specific part of the structure.
- For websites: page sections, layout system, type scale, palette, breakpoints.

## Stage 4: Critique

Attack the architecture before building anything.

- Look for logic errors, missing cases, unsupported claims, and conflicts with the constraints.
- For code: bugs, unhandled errors, security issues, maintainability.
- For websites: visual weaknesses (hierarchy, spacing, contrast, generic styling) and technical issues (responsiveness, markup validity, accessibility).
- For reasoning: invalid inferences, hidden assumptions, unchecked calculations.
- Ask: what is the strongest objection to this design, and does it survive?

Revise the architecture to fix every flaw. List each flaw and its fix.

## Stage 5: Verification

Build the result from the revised architecture, then score it out of 10.

**For code and websites:**

| Criterion | Points | Full credit requires |
|---|---|---|
| Correctness | 3 | The code runs or the page renders without errors. Every requirement is met. Edge cases are handled and demonstrated. |
| Code quality | 2 | Valid syntax, clear naming, no dead code, no duplication, no security issues, consistent structure. |
| Visual quality | 3 | Clear hierarchy, consistent spacing and typography, coherent palette, good contrast, a polished and non-generic result. |
| Responsiveness and accessibility | 2 | Works at mobile and desktop widths. Semantic HTML, labeled controls, readable contrast, keyboard navigation. |

**For reasoning:**

| Criterion | Points | Full credit requires |
|---|---|---|
| Correctness | 4 | Every fact, calculation, and inference is checked and holds. Uncertain points are flagged and do not affect the conclusion. |
| Completeness | 2 | Every sub-question from the analysis is fully answered. |
| Constraint compliance | 2 | Format, language, length, and scope match the message stage exactly. |
| Clarity | 2 | Reasoning is easy to follow, with no contradictions and no padding. |

Scoring rules for 10/10:

- Each criterion is scored separately. Partial credit is allowed only if the missing part is explained and fixed in the next pass.
- A single unresolved defect in any criterion means the total is below 10.
- For each criterion, write the points awarded and a one-line justification with evidence (for code, the test or check performed; for reasoning, the recalculation or source).
- A check that was not performed cannot earn points. Perform it or do not award the score.

Verification result:

- Score 10: PASS. Deliver the final result, with the score shown.
- Score 9 or lower: FAIL. List every defect that cost points, then restart at the message stage.

## Rules

- Stages run in order and each one is shown.
- The loop continues until the score is 10/10. There is no maximum number of passes.
- Never inflate a score. A defect that is real always costs points.
- Be honest about uncertainty. An unverifiable fact counts as a defect.
- Deliver only the result that reached 10/10.
