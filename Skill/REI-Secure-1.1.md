---
name: rei-secure-1.1
description: REI security review pipeline for websites and web applications (message → analysis → architecture → critique → verification). Defensive only. Shows each stage, scores security verification out of 10, and loops until 9/10 or higher. Use to audit a site the user owns or is authorized to test, for headers, HTTPS, authentication, input handling, exposed data, dependencies, and misconfiguration.
---

# REI-Secure-1.1: Defensive Security Review Pipeline

REI-Secure applies the REI reasoning loop to defensive security review of websites and web applications. Each stage is shown to the user. Verification scores the review out of 10. If the score is below 9/10, the pipeline restarts from the message stage with the verification feedback. There is no fixed limit on passes. The loop ends when the score is 9/10 or higher.

Flow:

message → analysis → architecture → critique → verification

If score < 9 → restart at message.
If score ≥ 9 → deliver the final security report.

## Scope and authorization

This skill is for defensive review. It identifies weaknesses and explains how to fix them. Before starting, confirm that the user owns the target or has written authorization to test it. If authorization is unclear, ask once. If the user cannot confirm, limit the work to public, passive checks (reading publicly served headers, pages, and documentation) and say so.

Do not produce working exploits, attack payloads, credential attacks, or steps for compromising a system. When a finding is serious, describe the risk and the fix, not a method to abuse it.

## Output format

Each stage uses a header:

**[1] Message**
**[2] Analysis**
**[3] Architecture**
**[4] Critique**
**[5] Verification**

Keep each stage short. After a restart, label the new pass (for example "Pass 2"), give the previous score, and list what changed.

## Stage 1: Message

Restate the review request in one or two sentences. List:

- The target: the URL or application, and its type (static site, CMS, SPA, e-commerce, dashboard, API-backed app).
- The authorization status: owner, authorized tester, or public-only review.
- The scope: which areas to review (all, or specific ones such as login or forms).
- The deliverable: a findings report with severity, evidence, and remediation.

## Stage 2: Analysis

Map the attack surface at a defensive level. Do not propose exploits.

- Identify the components visible from public information: pages, forms, login flows, cookies, third-party scripts, hosting and CDN signals, client-side frameworks, and exposed files or endpoints.
- List the data handled: personal data, credentials, payment information, session tokens, and internal data.
- Identify the trust boundaries: browser, server, third-party services, and admin areas.
- List the review areas to check, using the categories in the verification table below.

## Stage 3: Architecture

Plan the review.

- Define the checks for each area: what is observed, what is the expected secure state, and what evidence will be recorded.
- Order the checks by impact, so high-risk areas are reviewed first.
- Define the report structure: summary, findings table with severity (critical, high, medium, low, informational), evidence, impact, and remediation for each finding.

## Stage 4: Critique

Challenge the review plan before running it.

- Is the scope complete? Are there high-impact areas missing, such as authentication, data exposure, or dependencies?
- Are the checks defensible? Each finding needs observable evidence, not guesses.
- Are severity ratings justified by impact and likelihood?
- Does the plan avoid anything outside the authorized scope or any exploitation step?

Revise the plan to fix each gap. List the gaps found and how each was closed.

## Stage 5: Verification

Produce the report from the revised plan, then score it. The score is out of 10.

| Criterion | Points | What counts |
|---|---|---|
| Transport and headers | 2 | HTTPS enforced with valid TLS and HSTS. Security headers checked: Content-Security-Policy, X-Content-Type-Options, frame protection, Referrer-Policy, Permissions-Policy. Cookies checked for Secure, HttpOnly, and SameSite flags. |
| Input and output handling | 2 | Forms and inputs reviewed for validation and output encoding. Reflected content, client-side injection risks, and unsafe file handling identified at a defensive level. |
| Authentication and session | 2 | Login, password reset, session lifetime, logout, and access control on protected pages. Verbose error messages and account enumeration checked. |
| Data exposure and configuration | 2 | Exposed files, directory listings, debug pages, default pages, source maps, backup files, and secrets in client code. Error pages and server banners checked. |
| Dependencies and third parties | 1 | Client libraries and their versions checked against known advisories. Third-party scripts reviewed for necessity and integrity (SRI). |
| Report quality | 1 | Each finding has severity, observable evidence, impact, and a concrete fix. Scope and limitations are stated. No overstated claims. |

For each criterion, write the points awarded and one line of justification. Then give the total.

Verification result:

- Score 9 or 10: PASS. Deliver the report with the score.
- Score 8 or below: FAIL. List the specific gaps that cost points, then restart at the message stage. Carry the gap list forward. Re-run every stage so the fix is reflected in the scope, the plan, and the critique.

Additional checks before any PASS:

- Every finding cites evidence that was actually observed. No finding is invented.
- Every finding has a remediation.
- Limitations are stated: what was not tested, and why.
- No step in the report describes how to exploit a finding.

## Rules

- Stages run in order and each one is shown.
- Defensive use only. Refuse any request that turns the review into an attack.
- Never inflate a score or a severity. Unverified findings are marked as unverified and count against the report quality.
- If a check cannot be performed, record it as not tested. Do not report it as passed.
- Loop until the score is 9/10 or higher. There is no maximum number of passes.
- Deliver only the report that passed verification, with its final score.
