# Project Scope and Security Requirements

> **Evidence status:** This document describes the project design and execution procedure. AWS deployment, access-test outcomes and cleanup have not been independently evidenced in the supplied material. Proposed controls are not represented as deployed controls.

## Business context

A fictional organisation is onboarding a junior cloud operator who needs to start and stop development compute resources. The same AWS lab account contains a simulated production instance. Broad EC2 privileges could let the operator interrupt production or alter resource settings beyond their responsibilities. Resource labels are also security-relevant: an operator who can relabel production as development may undermine tag-based restrictions.

The intended business outcome is useful development access with a clear, tested boundary around production operations and identity administration.

## Scope

Included: two representative EC2 instances, consistent tags, custom permissions, an isolated test identity, group/role assignments, access validation, management-event review, lifecycle workflows and cleanup. Excluded: real patient/customer data, application deployment, operating-system access, penetration testing of external systems, full multi-account landing zones and compliance certification.

The basic exercise uses an IAM user and group. The target design discusses three functional roles and federation. These enhancements remain design proposals until implementation evidence is added.

## User stories

| ID | User story | Acceptance criterion |
|---|---|---|
| US-01 | As a developer, I need to control approved development instance state | Start and stop succeed for the correctly tagged lab instance |
| US-02 | As a service owner, I need production protected from developer changes | Developer start and stop requests against production are denied |
| US-03 | As an identity administrator, I need environment tags protected | Developer CreateTags and DeleteTags are denied |
| US-04 | As a security reviewer, I need attributable access evidence | Test records identify caller, operation, time, target and audit reference |
| US-05 | As a manager, I need role changes to remove obsolete access | Mover tests show old permissions removed and new permissions validated |
| US-06 | As an administrator, I need departing users' access removed | Leaver tests record fresh-session and existing-session behaviour |

## Requirements and traceability

| Requirement | Control | Test |
|---|---|---|
| REQ-01 Selected metadata reads | Explicit Describe action list | TC-01 |
| REQ-02 Development start/stop | Account/Region scope and Env condition | TC-02, TC-03 |
| REQ-03 Production changes blocked | Explicit production lifecycle deny | TC-04, TC-05 |
| REQ-04 Tag manipulation blocked | Explicit CreateTags/DeleteTags deny | TC-06, TC-07 |
| REQ-05 Destructive/admin actions blocked | Explicit terminate deny; IAM writes not granted | TC-08, TC-09 |
| REQ-06 Missing/incorrect tags fail safely | StringEquals allow condition | TC-11, TC-12 |
| REQ-07 Auditable operation | CloudTrail correlation and evidence register | TC-13 |
| REQ-08 Effective removal | Lifecycle procedure and session review | TC-10 |
| REQ-09 Role separation | Separate reviewed permission sets | TC-14, TC-15 |

## Governance and ownership

| Function | Responsibility | Lab representation |
|---|---|---|
| Project owner | Scope, cost and completion decisions | Student acting as owner |
| Service owner | Approves workload access and test timing | Simulated stakeholder |
| Identity administrator | Creates identities, assignments and policies | Separate administrator session |
| Operator | Exercises approved access | Isolated test identity |
| Security reviewer | Reviews evidence and residual risks | Student acting as reviewer |

Simulated roles do not demonstrate independent organisational approval. Keep a written decision record when one person performs several functions.

## Assumptions and constraints

The student account permits the required IAM and EC2 actions. If it does not, document the restriction and use policy design/simulation as a limited alternative; do not label simulation as live validation. Exact Region, instance sizing, costs and deployed names are not established by the supplied evidence. No actual production workload may be used for negative tests.

## Completion gate

Completion requires a resource inventory, deployed policy exports, caller identity evidence, pass/fail records for required tests, audit correlation, reviewed risks and a cleanup record. Design documentation alone is a deliverable but does not close implementation or validation requirements.
