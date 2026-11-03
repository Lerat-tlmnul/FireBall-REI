---
name: rei-secure-2.0-max
description: Strict, extended, traceable REI defensive security review pipeline (message → analysis → threat modeling → architecture → adversarial critique → construction → verification → counter-audit → delivery). Defensive only. Every stage is shown. Verification must reach 10/10 with every in-scope check performed and evidenced. Unlimited looping until 10/10, with mandatory regression on every pass. Use to audit a site or web application the user owns or is authorized to test.
---

# REI-Secure-2.0-Max — Strict, Extended, Traceable Defensive Security Review

REI-Secure-2.0-Max keeps the single rule of REI-Secure-1.1-Max: **only a score of 10/10 permits delivery of the report**. All stages are shown. The pipeline adds threat modeling, an explicit evidence register, an adversarial critique with pre-mortem, an independent counter-audit, and mandatory regression. There is no limit on the number of passes.

## What Changes from 1.1

- 9 stages instead of 5: threat modeling, construction, and counter-audit become full stages.
- Authorization gate enforced at stage [1], before any check runs.
- Assumption register and ambiguity register, with impact and decision.
- Traceability matrix: check → component → evidence.
- Explicit threat model: assets, trust boundaries, data flows, entry points.
- Multi-role adversarial critique and pre-mortem.
- Evidence register: no finding and no passing check without observable proof.
- Independent counter-audit that can invalidate a 10/10.
- Mandatory regression: every new pass replays the checks from previous passes.
- Depth levels to scale effort without ever lowering the 10/10 threshold.
- Stronger anti-inflation rules and stronger defensive-only guardrails.

## Scope and Authorization

This skill is for defensive review only. It identifies weaknesses and explains how to fix them.

- Before any check runs, confirm that the user owns the target or has written authorization to test it.
- If authorization is unclear, ask once. If the user cannot confirm, restrict the work to public, passive checks and record that limitation in the report and in the traceability matrix.
- Do not produce working exploits, attack payloads, credential attacks, or steps for compromising a system. When a finding is serious, describe the risk and the fix, not a method of abuse.
- The counter-audit (stage [8]) rejects any report that contains an exploitation step, an unverifiable finding, or a severity rating that is not justified by evidence.

## Loop

message → analysis → threat modeling → architecture → adversarial critique → construction → verification → counter-audit → delivery

- If verification < 10 → FAIL: list every defect, then **restart at message**.
- If verification = 10 but the counter-audit finds a defect → the 10/10 is invalidated, **restart at message**.
- If verification = 10 and the counter-audit confirms → **delivery**.
- On every restart: state the pass number (“Pass 3”), the previous score, the full list of carried-forward defects, and how each one was fixed. Replay all checks from previous passes (regression).

## Output Format

Each stage uses a header:

**[1] Message**
**[2] Analysis**
**[3] Threat Modeling**
**[4] Architecture**
**[5] Adversarial Critique**
**[6] Construction**
**[7] Verification**
**[8] Counter-Audit**
**[9] Delivery**

Each stage is structured and brief. Registers and matrices are presented as tables. Every passing check and every finding points to evidence in the evidence register.

## Depth Levels

Chosen at stage [1] and applied to all following stages. The 10/10 threshold never changes.

- **N1 — Simple**: static site or single page, low risk. Lighter critique and counter-audit, still real.
- **N2 — Standard**: default.
- **N3 — Deep**: authenticated areas, dashboards, public-facing application. Full multi-role critique, explicit access-control checks.
- **N4 — Maximal**: production system, payment or personal data, high stakes. Pre-mortem, reinforced counter-audit, extended regression checks, privacy and data-handling review, dependency review across the full client and server stack visible to the reviewer.

The depth level may never be used to skip a check: it only adds checks.

## Stage 1: Message

Restate the request. List:

- **Target**: URL or application, and its type (static site, CMS, SPA, e-commerce, dashboard, API-backed app).
- **Authorization status**: owner, authorized tester, or public-only review. Record the exact basis (who authorized, in what terms). If unclear, ask once and record the outcome.
- **Scope**: areas in scope, and areas explicitly excluded by the user.
- **Constraints**: language, format, length, audience for the report, deadline, level of technical depth expected.
- **Assumptions**: each explicit assumption, with confidence (high / medium / low) and impact if false.
- **Ambiguities**: each ambiguity, the interpretation retained, the alternative discarded, and why. Never block: decide, document, continue.
- **Depth level** retained (N1–N4) and justification.
- **Deliverable**: findings report with severity, evidence, impact, and remediation, plus the list of checks performed and the list of checks not performed.
- **Exact acceptance conditions**: what must be true for the report to count as complete.

Produce the **assumption register** and the **ambiguity register**:

| # | Assumption | Confidence | Impact if false | Decision |
|---|---|---|---|---|

| # | Ambiguity | Interpretation retained | Alternative discarded | Reason |
|---|---|---|---|---|

## Stage 2: Analysis

Map the attack surface at a defensive level. Do not propose exploits.

- Identify visible components: pages, forms, login flows, cookies, third-party scripts, hosting and CDN signals, client-side frameworks, exposed files and endpoints.
- List the data handled: personal data, credentials, payment information, session tokens, internal data.
- Identify trust boundaries: browser, server, third-party services, admin areas.
- List every in-scope check, using the categories in the verification table.
- Mark what is **observed directly**, **inferred from evidence**, **unknown**, and **must be checked**.
- List **failure points**: where a naive review would miss a real weakness (client-only assumptions, third-party trust, default configurations, error paths, cache behavior).

Produce the initial **traceability matrix** (completed through delivery):

| Check | Component or surface | Method | Expected evidence |
|---|---|---|---|

## Stage 3: Threat Modeling

Make the risk model explicit before planning the review. Defensive framing only.

- **Assets**: what the application protects (accounts, personal data, payment data, session tokens, admin capabilities, integrity of content).
- **Actors**: anonymous visitor, authenticated user, privileged user, third-party service, operator.
- **Entry points**: every surface where data or control crosses a trust boundary (URL parameters, form fields, headers, cookies, file uploads, API calls, webhooks, third-party scripts).
- **Trust boundaries**: browser ↔ server, server ↔ third party, user area ↔ admin area, public ↔ authenticated.
- **Data flows**: for each asset, where it enters, where it is stored, where it is transmitted, where it is rendered.
- **Threats mapped to checks**: for each threat, which verification category in stage [7] will address it.
- **Out of model**: threats that are explicitly out of scope for this review (for example, server-side code review that the user excluded), recorded so they cannot be silently counted as passed.

Deliverable: a concise threat model (lists and tables) and the list of threats mapped to verification categories. Any threat not covered by an in-scope check is recorded as **not covered**, not as passed.

## Stage 4: Architecture

Plan the review.

- For each check: what is observed, the expected secure state, and the evidence to record.
- Order checks by impact, highest first.
- Specify for each check whether it is **active** (performed against the running target within authorization) or **passive** (public information only), and record the reason when a check is passive.
- Define the report structure: executive summary, findings table (critical, high, medium, low, informational), and for each finding its evidence, impact, and remediation. Include the list of checks performed, the list of checks not performed, and the authorization basis.
- Update the traceability matrix with the final check list and the method for each.

## Stage 5: Adversarial Critique

Attack the plan before running it.

- **Multi-role**: skeptical reviewer, end user, attacker (as a threat perspective only — no exploitation), maintainer, privacy officer.
- **Pre-mortem**: imagine the report is rejected because it missed a serious weakness or overstated a minor one; list plausible causes and correct the plan.
- Is the scope complete? Are high-impact areas missing: authentication, session handling, access control, data exposure, dependencies?
- Is every check defensible, with observable evidence rather than guesses?
- Are severity ratings justified by impact and likelihood, with a stated method?
- Does the plan stay within authorization, and avoid any exploitation step?
- Are out-of-scope areas clearly recorded so they cannot be silently counted as passed?

Revise the plan to close each gap. List each gap and its fix:

| # | Gap identified | Role / method | Fix applied |
|---|---|---|---|

## Stage 6: Construction

Produce the report from the revised plan.

- Run every in-scope check from stage [4] within the authorization confirmed at stage [1].
- For each check, record the observable evidence actually seen (headers observed, response behavior, cookie attributes, page content, library version string, file presence, error page content) in the **evidence register**.
- For each finding: title, category, severity with justification method, observable evidence, impact, and a concrete remediation.
- Do not invent findings, severities, or evidence. If a check could not be performed, record it as **not performed** with the reason.
- Do not include any exploitation step, payload, or method of abuse.
- Do not describe a fix that itself introduces a new weakness; where a trade-off exists, state it.

| # | Evidence | Check category | Observation | Result (pass / finding / not performed) |
|---|---|---|---|---|

## Stage 7: Verification

Evaluate the constructed report and score it out of 10.

| Criterion | Points | Full credit requires |
|---|---|---|
| Transport and headers | 2 | HTTPS enforced, TLS validity observed, HSTS checked. CSP, X-Content-Type-Options, frame protection, Referrer-Policy, and Permissions-Policy checked. Cookie flags (Secure, HttpOnly, SameSite) checked. Every result recorded with the observed header or behavior. |
| Input and output handling | 2 | Forms and inputs reviewed for validation and output encoding. Reflected content, client-side injection risks, and file handling assessed defensively. Each assessment backed by an observed surface, not an assumption. |
| Authentication and session | 2 | Login, password reset, session lifetime, logout, and access control on protected pages checked. Account enumeration and verbose errors assessed. Each result cited to an observed behavior. |
| Access control | 1 | Protected pages and privileged endpoints checked for authorization at the object and function level. Horizontal and vertical access assessed where the authorization allows it. |
| Data exposure and configuration | 1 | Exposed files, directory listings, debug pages, source maps, backup files, and secrets in client code checked. Error pages and server banners assessed. |
| Dependencies and third parties | 1 | Client libraries checked against known advisories by version. Third-party scripts reviewed for necessity and integrity (SRI). Versions and advisory sources cited. |
| Report quality and traceability | 1 | Every finding has severity with a stated method, observable evidence, impact, and a concrete remediation. Scope, authorization, limitations, and the list of checks not performed are stated. Traceability matrix and evidence register are complete. |

**Scoring rules for 10/10:**

- Each criterion is scored separately. Points are awarded only for checks actually performed and evidenced.
- Checks excluded by the user's scope are not penalized, provided they are recorded as out of scope. Any in-scope check that was not performed prevents a 10.
- For each criterion, write the points awarded and a one-line justification citing evidence in the evidence register.
- Every finding must cite evidence that was actually observed. Invented or unverified findings are defects.
- Every finding must have a remediation.
- No step in the report may describe how to exploit a finding.
- Severity ratings must be justified. Overstated or understated severity is a defect.
- A check that was not performed cannot earn points. Perform it or do not award the score.

**Verification result:**

- Score 10: PASS provisionally, proceed to counter-audit.
- Score 9 or lower: FAIL. List every defect that cost points, then restart at stage [1].

## Stage 8: Counter-Audit

Independent audit of the report and of the stage [7] scoring. Goal: invalidate any undeserved 10/10.

- Replay regression checks from all previous passes.
- Verify that every row of the traceability matrix has real evidence in the evidence register, or is explicitly recorded as not performed with a reason.
- Verify that every check counted as passed has an observed observation, not an assumption.
- Verify that every finding's severity is justified by the stated method and the evidence.
- Search for undetected weaknesses: missed entry points from the threat model, missed access-control checks, missed data exposure, third-party scripts without integrity, verbose errors that leak information.
- Confirm that no exploitation step, payload, or method of abuse appears anywhere in the report.
- Confirm that out-of-scope areas are recorded as out of scope and are not counted as passed.
- Confirm that the authorization basis recorded at stage [1] is present and consistent with the checks actually performed.

**Counter-audit verdict:**

- If a defect is found: the 10/10 is **invalidated**. List the defect, then restart at stage [1].
- If no defect is found: confirm the 10/10 and proceed to delivery.

| # | Counter-check | Method | Result |
|---|---|---|---|

## Stage 9: Delivery

Deliver only the report that reached 10/10 and was confirmed by the counter-audit.

- Show the final score: **10/10**, with the breakdown by criterion.
- Show the counter-audit verdict: **confirmed**.
- Provide the complete report: executive summary, findings table, per-finding evidence, impact, and remediation, list of checks performed, list of checks not performed, authorization basis, scope and limitations.
- Briefly recall the assumptions and ambiguities documented in stage [1].
- State the number of passes performed and the defects fixed across passes.
- Deliver nothing if the score is not 10/10 or if the counter-audit has not confirmed.

## Rules

- Stages run in order and each one is shown.
- Defensive use only. Refuse any request that turns the review into an attack. Refuse to produce exploits, payloads, credential attacks, or abuse steps.
- Authorization is confirmed at stage [1] before any check runs. If it cannot be confirmed, the review is limited to public, passive checks and this limitation is recorded.
- The loop continues until the score is 10/10. There is no maximum number of passes.
- Never inflate a score or a severity. A real defect always costs points.
- No point without evidence: a check that was not performed earns nothing and is recorded as not performed.
- Record any check that cannot be performed as not performed. Never report it as passed.
- The counter-audit can invalidate a 10/10; its confirmation is mandatory before delivery.
- Regression is mandatory on every pass: previous checks are replayed.
- The depth level adds checks; it never reduces the 10/10 threshold.
- Deliver only the report that reached 10/10 and was confirmed by the counter-audit.
