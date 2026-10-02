# Risk Assessment and Limitations



## Assessment method

This is a project-specific qualitative risk method, not a complete enterprise risk management framework. Likelihood and impact are each scored from 1 to 3. Likelihood: 1 unlikely under the stated scenario, 2 plausible, 3 readily achievable with current exposure. Impact: 1 minor lab rework, 2 material disruption or unauthorised change, 3 severe workload/identity compromise in the fictional business scenario. Score equals likelihood multiplied by impact: 1–2 Low, 3–4 Medium, 6–9 High.

Inherent estimates reflect the fictional scenario before the proposed treatments. Residual estimates are conditional design forecasts, not observed or accepted risk ratings. Reassess after test evidence. One student represents the owners; independent business acceptance is not established.

## Risk register

| ID | Risk and cause | Inherent L/I/score | Treatment | Owner | Validation | Forecast residual |
|---|---|---|---|---|---|---|
| R-01 | Production interruption through excessive lifecycle access | 3/3/9 High | Narrow actions, tag scope and explicit production deny | Service owner | TC-04/05 | 1/3/3 Medium |
| R-02 | Tag-based bypass through resource relabelling | 2/3/6 High | Deny CreateTags/DeleteTags; govern administrator tagging | Identity administrator | TC-06/07 | 1/3/3 Medium |
| R-03 | Destructive deletion outside operator duties | 2/3/6 High | Explicit terminate deny and safe negative test | Service owner | TC-08 | 1/3/3 Medium |
| R-04 | Privilege accumulation from overlapping assignments | 2/3/6 High | Assignment review and mover validation | Identity administrator | TC-09/16 | 1/3/3 Medium |
| R-05 | Credential misuse through weak authentication or public secrets | 2/3/6 High | MFA, unique identity, no unnecessary keys, publication review | Identity administrator | Authentication evidence and repository review | 1/3/3 Medium |
| R-06 | Failure to investigate due to missing or expired evidence | 2/2/4 Medium | Timely CloudTrail review and sanitised export | Security reviewer | TC-13 | 1/2/2 Low |
| R-07 | Departing identity retains an access path or session | 2/3/6 High | Remove assignments; handle sessions and retest | Identity administrator | TC-10 | 1/3/3 Medium |
| R-08 | Unplanned cloud charges from resources left behind | 2/2/4 Medium | Cost checks, short execution window and verified cleanup | Project owner | Cleanup inventory/billing | 1/2/2 Low |
| R-09 | Single-account administrator can change both environments | 2/3/6 High | Document boundary; propose separate accounts for production | Project owner | Architecture review | 2/3/6 High |
| R-10 | Incorrect portfolio claims obscure unfinished controls | 2/2/4 Medium | Separate design, implementation and validation status | Project owner | Evidence register review | 1/2/2 Low |

## Treatment workflow

Finding → analysis → affected requirement → treatment owner → configuration change → retest → evidence → residual reassessment → documented decision. For any failed production or tag restriction, stop treating the lab as validated until the effective policy issue is resolved. Preserve the original failing record and link the corrected retest.

## Technical limitations

Selected EC2 Describe calls expose metadata beyond only the development instance. The lifecycle allow matches all development-tagged instances within its account/Region ARN scope, unless narrowed to exact resources. Environment tags do not isolate network paths, workloads, storage or administrative control. IAM user/group setup is educational and does not demonstrate workforce federation. The supplied policies do not enforce MFA, implement a permissions boundary or limit an administrator who can change them.

CloudTrail Event history has a limited retention window and focuses on management events. Exported evidence needs its own retention and access arrangements. Dry-run/simulator tests offer narrower evidence than live non-destructive operations. An account with restricted services may prevent full deployment; that outcome must remain explicit.

## Enterprise evolution

For a real organisation, consider separate production/development accounts, central identity federation, independently approved privileged roles, central audit retention, organisation guardrails, automated policy validation and scheduled access reviews. These are recommended design directions, not delivered controls in this lab.
