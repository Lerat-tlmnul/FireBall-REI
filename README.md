# FireBall REI Skill

> A structured reasoning pipeline that gives AI models deliberate, self-checked intelligence before they answer.

![FireBall REI](assets/logo.png)

## Overview

**FireBall REI** is a reasoning skill built around a five-stage loop: **message → analysis → architecture → critique → verification**. Instead of jumping straight to an answer, the model works through each stage in order, then verifies the result against the original request. If verification fails, the pipeline restarts with the failure notes carried forward.

The goal is simple: make the AI *think* before it *speaks*, and *check* before it *delivers*.

This skill is designed to give the AI genuine reasoning intelligence — not just faster answers, but better ones, because every output is decomposed, planned, attacked, and verified before it reaches the user.

## The Pipeline

| Stage | Name | What it does |
|-------|------|--------------|
| 1 | **Message** | Restates the request, identifies explicit goals, implicit constraints, and ambiguities. Resolves ambiguity with stated assumptions. |
| 2 | **Analysis** | Decomposes the problem into sub-questions. Separates known from unknown. Identifies failure modes where a naive answer would go wrong. |
| 3 | **Architecture** | Designs the answer. Chooses an approach with justification against alternatives. Maps each sub-question to a part of the output. |
| 4 | **Critique** | Attacks the plan. Finds logical gaps, missing cases, and unsupported claims. Revises the architecture and records what changed and why. |
| 5 | **Verification** | Produces the answer and checks it against five criteria: completeness, constraint compliance, correctness, consistency, usefulness. |

**On failure:** verification records which check failed and why, then the pipeline returns to Stage 1. Failure notes are carried forward so the next pass corrects the specific defect.

**Loop safety:** if the same check fails on two consecutive passes, the pipeline stops and explains what is blocking the result.

## Verification Criteria

An answer is only delivered when all five checks pass:

1. **Completeness** — every sub-question from Stage 2 is answered.
2. **Constraint compliance** — format, language, length, and scope match Stage 1.
3. **Correctness** — facts, calculations, and code are verified, not assumed.
4. **Consistency** — no part of the answer contradicts another part.
5. **Usefulness** — the answer solves the user's actual problem, not just the literal wording.

## Rules

- Stages run **in order**. No skipping, no silent merging.
- Each stage's output stays **brief and structured** — the reasoning is the work, not the prose.
- Only the **final verified answer** is shown to the user, unless they ask to see the process.
- Verification is **never marked PASS** without performing the checks.

## When to Use It

FireBall REI is designed for any task that needs structured, self-checked reasoning before the final answer:

- Multi-step problems where a naive response would miss constraints
- Tasks with strict format, language, or scope requirements
- Questions where correctness and consistency matter
- Situations where you want the model to catch its own mistakes before they reach you
- Any task that benefits from explicit decomposition, planning, and critique

## Files

- `REI-1.md` — the skill definition and pipeline specification
- `assets/logo.png` — the FireBall REI logo

## Example Flow

```text
User request
     |
     v
 [1] Message        -> problem statement + constraints
     |
     v
 [2] Analysis       -> decomposition + risks
     |
     v
 [3] Architecture   -> plan mapped to sub-questions
     |
     v
 [4] Critique       -> revised plan + flaws fixed
     |
     v
 [5] Verification   -> PASS -> deliver  |  FAIL -> back to [1]
```

## License

See the repository for license details.
