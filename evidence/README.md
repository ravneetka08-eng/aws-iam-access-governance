# Evidence Register and Publication Standard

> **Evidence status:** This document describes the project design and execution procedure. AWS deployment, access-test outcomes and cleanup have not been independently evidenced in the supplied material. Proposed controls are not represented as deployed controls.

## Evidence currently available

The supplied VS Code screenshot supports the existence of the project folder/file layout. The supplied tutorial text supports the source exercise and original policy. Neither establishes actual IAM attachments, deployed resource states, successful tests or cleanup. Raw supplied inputs are not copied into this public repository because they include irrelevant interface text and potential identifying information.

## Required evidence register

| ID | Evidence item | Supports | Current status |
|---|---|---|---|
| E-01 | Sanitised EC2 inventory and environment tags | Resource scope and environment distinction | Not supplied |
| E-02 | Active policy JSON and validation findings | Deployed permissions | Not supplied |
| E-03 | Group/role assignment and other-grant review | Effective identity access | Not supplied |
| E-04 | Caller identity and selected metadata visibility | TC-01 | Not supplied |
| E-05 | Development stop and state change | TC-02 | Not supplied |
| E-06 | Development start and state change | TC-03 | Not supplied |
| E-07 | Production stop denial and unchanged target | TC-04 | Not supplied |
| E-08 | Production start denial | TC-05 | Not supplied |
| E-09 | Production retag denial and original tag retained | TC-06 | Not supplied |
| E-10 | Development tag deletion denial | TC-07 | Not supplied |
| E-11 | Termination dry-run/simulator output | TC-08 | Not supplied |
| E-12 | IAM administration denial | TC-09 | Not supplied |
| E-13 | Access removal and session results | TC-10 | Not supplied |
| E-14 | Missing-tag test and restoration | TC-11 | Not supplied |
| E-15 | Mismatched-tag test and restoration | TC-12 | Not supplied |
| E-16 | Correlated sanitised CloudTrail records | TC-13 | Not supplied |
| E-17 | Production role tests | TC-14 | Not supplied |
| E-18 | Reviewer read/write tests | TC-15 | Not supplied |
| E-19 | Mover request, assignment changes and results | TC-16 | Not supplied |
| E-20 | Explicit deny evaluation | TC-17 | Not supplied |
| E-21 | Authentication configuration evidence | MFA configuration claim | Not supplied |
| E-22 | Final inventories and billing review | Cleanup | Not supplied |

## Collection standard

Use folders `configuration`, `access-tests` and `audit-events`. Suggested filenames: `TC-04-production-stop-denied.png` and `TC-04-cloudtrail-sanitised.json`. Each evidence caption must describe timestamp/timezone, caller label, target label, action, expected/actual result and limitation. Preserve sufficient context to connect it to a requirement, not just a coloured success banner.

Export original evidence privately before redaction. Keep public identifiers consistently pseudonymised across screenshots and JSON so reviewers can correlate records. Do not invent event IDs, request IDs, timestamps or errors. Where hashing is used, distinguish the original private artifact hash from the redacted public artifact hash; their bytes differ.

## Publication review

Exclude passwords, access keys, session tokens, private keys, MFA seed/QR codes, recovery data and credential downloads. Account IDs and resource IDs are not passwords but may be sanitised to reduce unnecessary disclosure. Redact email addresses, login aliases and unrelated resource details when appropriate. A .gitignore does not detect secrets and does not remove material already committed.

## Evidence sufficiency

A source tutorial demonstrates instructions, not your execution. A policy screenshot demonstrates a configuration view, not the complete effective permissions. A simulator output predicts access under its inputs, not every live account control. A pass requires the observed operation and supporting context. If evidence is missing, keep the result unverified and describe the available design deliverable accurately.
