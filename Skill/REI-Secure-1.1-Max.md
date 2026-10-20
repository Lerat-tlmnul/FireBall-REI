---
name: rei-secure-1.1-max
description: REI strict security review pipeline for websites and web applications (message → analysis → architecture → critique → verification). Defensive only. Shows each stage. Verification must reach 10/10 with every in-scope check performed. Loops without limit until 10/10. Use to audit a site the user owns or is authorized to test.
---

# REI-Secure-1.1-Max: Strict Defensive Security Review Pipeline

REI-Secure-1.1-Max applies the strict REI loop to defensive security review of websites and web applications. The only pass condition is a verification score of 10/10. Every stage is shown to the user. A score of 9 or lower restarts the pipeline from the message stage with the full list of defects. There is no limit on passes.

Flow:

message → analysis → architecture → critique → verification

If score < 10 → restart at message.
If score = 10 → deliver the final security report.

## Scope and authorization

This skill is for defensive review. It identifies weaknesses and explains how to fix them. Before starting, confirm that the user owns the target or has written authorization to test it. If authorization is unclear, ask once. If the user cannot confirm, limit the work to public, passive checks and state that limitation in the report.

Do not produce working exploits, attack payloads, credential attacks, or steps for compromising a system. When a finding is serious, describe the risk and the fix, not a method of abuse.

## Output format

Each stage uses a header:

**[1] Message**
**[2] Analysis**
**[3] Architecture**
**[4] Critique**
**[5] Verification**

After a restart, label the pass (for example "Pass 3"), give the previous score, list every defect carried forward, and state how each was fixed.

## Stage 1: Message

Restate the request. List:

- The target: URL or application, and its type (static site, CMS, SPA, e-commerce, dashboard, API-backed app).
- The authorization status: owner, authorized tester, or public-only review.
- The scope: which areas are in scope, and which are explicitly excluded by the user.
- The deliverable: a findings report with severity, evidence, impact, and remediation.

## Stage 2: Analysis

Map the attack surface at a defensive level. Do not propose exploits.

- Identify the visible components: pages, forms, login flows, cookies, third-party scripts, hosting and CDN signals, client-side frameworks, exposed files and endpoints.
- List the data handled: personal data, credentials, payment information, session tokens, internal data.
- Identify trust boundaries: browser, server, third-party services, admin areas.
- List every in-scope check, using the categories in the verification table.

## Stage 3: Architecture

Plan the review.

- For each check: what is observed, the expected secure state, and the evidence to record.
- Order checks by impact, highest first.
- Define the report structure: summary, findings table (critical, high, medium, low, informational), and for each finding its evidence, impact, and remediation. Include a list of checks performed and a list of checks not performed.

## Stage 4: Critique

Challenge the plan before running it.

- Is the scope complete? Are high-impact areas missing: authentication, data exposure, dependencies?
- Is every check defensible, with observable evidence rather than guesses?
- Are severity ratings justified by impact and likelihood?
- Does the plan stay within authorization, and avoid any exploitation step?

Revise the plan to close each gap. List each gap and how it was closed.

## Stage 5: Verification

Produce the report from the revised plan, then score it out of 10.

| Criterion | Points | Full credit requires |
|---|---|---|
| Transport and headers | 2 | HTTPS enforced with valid TLS and HSTS. Content-Security-Policy, X-Content-Type-Options, frame protection, Referrer-Policy, and Permissions-Policy checked. Cookie flags (Secure, HttpOnly, SameSite) checked. |
| Input and output handling | 2 | Forms and inputs reviewed for validation and output encoding. Reflected content, client-side injection risks, and file handling assessed at a defensive level. |
| Authentication and session | 2 | Login, password reset, session lifetime, logout, and access control on protected pages checked. Account enumeration and verbose errors assessed. |
| Data exposure and configuration | 2 | Exposed files, directory listings, debug pages, source maps, backup files, and secrets in client code checked. Error pages and server banners assessed. |
| Dependencies and third parties | 1 | Client libraries checked against known advisories by version. Third-party scripts reviewed for necessity and integrity (SRI). |
| Report quality | 1 | Each finding has severity, observable evidence, impact, and a concrete fix. Scope, limitations, and the list of checks not performed are stated. |

Scoring rules for 10/10:

- Each criterion is scored separately. Points are awarded only for checks actually performed and evidenced.
- Checks excluded by the user's scope are not penalized. Any in-scope check that was not performed prevents a 10.
- For each criterion, write the points awarded and a one-line justification citing the evidence.
- Every finding must cite evidence that was actually observed. Invented or unverified findings are defects.
- Every finding must have a remediation.
- No step in the report may describe how to exploit a finding.
- Severity ratings must be justified. Overstated severity is a defect.

Verification result:

- Score 10: PASS. Deliver the report with the score.
- Score 9 or lower: FAIL. List every defect that cost points, then restart at the message stage.

## Rules

- Stages run in order and each one is shown.
- Defensive use only. Refuse any request that turns the review into an attack.
- The loop continues until the score is 10/10. There is no maximum number of passes.
- Never inflate a score or a severity.
- Record any check that cannot be performed as not performed. Never report it as passed.
- Deliver only the report that reached 10/10.
