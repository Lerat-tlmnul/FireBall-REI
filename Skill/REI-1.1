---
name: rei-1.1
description: REI reasoning pipeline for code and reasoning tasks (message → analysis → architecture → critique → verification). Shows each stage to the user. Verification scores the result out of 10 and loops until the score is 9/10 or higher. Use for coding tasks such as websites, scripts, and fixes, and for reasoning tasks such as logic, math, and analysis.
---

# REI-1.1: Visible Reasoning Pipeline with Scored Verification

REI runs five stages in order. Every stage is shown to the user as a clearly labeled section. Verification scores the result out of 10. If the score is below 9/10, the pipeline restarts from the message stage, using the verification feedback. The loop has no fixed limit. It ends only when the score is 9/10 or higher.

Flow:

message → analysis → architecture → critique → verification

If score < 9 → restart at message.
If score ≥ 9 → deliver the final result.

## Output format

Each stage uses a header in this form:

**[1] Message**
**[2] Analysis**
**[3] Architecture**
**[4] Critique**
**[5] Verification**

Keep each stage short and structured. The stages are visible, so the user must be able to follow the reasoning quickly. After a restart, label the new pass (for example "Pass 2") and state what the previous score was and what changed.

## Stage 1: Message

Restate the request in one or two sentences. List:

- The goal: what the user wants to obtain.
- The constraints: language, format, length, technologies, audience, scope, and any explicit requirements.
- The assumptions: any ambiguity resolved by a reasonable choice, stated explicitly.

For code tasks, also state the expected deliverable (a file, a snippet, a fix, a full page) and the environment if known.

For reasoning tasks, state the question precisely and the form of answer expected (a number, a proof, a recommendation, an explanation).

## Stage 2: Analysis

Decompose the problem. Do not propose a solution yet.

- Split the request into sub-problems.
- Mark what is known, what is unknown, and what must be checked.
- List the relevant rules, facts, or APIs.
- List the likely failure points, where a naive solution would break.

For code: identify the inputs, outputs, edge cases, and quality bars (correctness, readability, responsiveness, accessibility, performance, security as relevant).

For a website or interface: identify the visual requirements (layout, hierarchy, typography, color, spacing, responsiveness), the content, and the interactions.

For reasoning: identify the premises, the variables, the possible interpretations, and the steps where an error is most likely.

## Stage 3: Architecture

Design the solution.

- Choose an approach and justify it briefly against at least one alternative.
- Define the structure of the output: files and their responsibilities for code; sections and their order for an explanation; steps and intermediate results for a calculation or proof.
- Map each sub-problem from the analysis to a specific part of the structure.

For code: name the modules, functions, or components, and their interfaces. For a website: define the page sections, the grid or layout system, the type scale, the color palette, and the breakpoints.

## Stage 4: Critique

Attack the architecture before building anything.

- Look for logic errors, missing cases, unsupported claims, and conflicts with the constraints.
- For code: look for bugs, unhandled errors, security issues, and maintainability problems.
- For a website: look for visual problems (weak hierarchy, inconsistent spacing, poor contrast, cramped or empty areas, generic styling), and technical problems (broken responsiveness, invalid markup, inaccessible elements).
- For reasoning: look for invalid inferences, hidden assumptions, and unchecked calculations.
- Ask: what is the strongest objection to this design? Does it survive?

Revise the architecture to fix every serious flaw. List the flaws found and how each was fixed.

## Stage 5: Verification

Build the result from the revised architecture, then score it. The score is out of 10, split across four criteria. Each criterion is scored out of the points shown.

**For code and websites:**

| Criterion | Points | What counts |
|---|---|---|
| Correctness | 3 | The code runs or the page renders without errors. Every requirement is met. Edge cases are handled. |
| Code quality | 2 | Clean structure, clear naming, no dead code, no duplication, valid syntax, and no security issues. |
| Visual quality | 3 | Clear hierarchy, consistent spacing and typography, a coherent palette, good contrast, and a polished, non-generic look. Applies to any UI output. |
| Responsiveness and accessibility | 2 | Works on mobile and desktop widths. Semantic HTML, labeled controls, readable contrast, keyboard navigation. |

**For reasoning:**

| Criterion | Points | What counts |
|---|---|---|
| Correctness | 4 | Every fact, calculation, and inference is checked and holds. Uncertain points are flagged. |
| Completeness | 2 | Every sub-question from the analysis is answered. |
| Constraint compliance | 2 | Format, language, length, and scope match the message stage. |
| Clarity | 2 | The reasoning is easy to follow, with no contradictions and no unnecessary padding. |

For each criterion, write the points awarded and one line of justification. Then give the total.

Verification result:

- Score 9 or 10: PASS. Deliver the final result, with the score shown.
- Score 8 or below: FAIL. List the specific defects that cost points, then restart at the message stage. Carry the defect list forward so the next pass fixes each one. Do not rewrite everything if a targeted fix is enough, but do re-run every stage so the fix is reflected in the architecture and the critique.

Do not award a score of 9 or higher unless every criterion has been checked. A high score given without checking is a failure of the stage.

## Rules

- Stages run in order and each one is shown.
- Keep the loop going until the score is 9/10 or higher. There is no maximum number of passes.
- Never inflate a score. If a defect is real, it costs points.
- Be honest about uncertainty. If a fact cannot be verified, flag it, and count it against correctness.
- Deliver only the result that passed verification, with its final score.
