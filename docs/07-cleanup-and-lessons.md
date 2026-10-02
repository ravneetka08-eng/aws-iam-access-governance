# Cleanup, Handover and Lessons

> **Evidence status:** This document describes the project design and execution procedure. AWS deployment, access-test outcomes and cleanup have not been independently evidenced in the supplied material. Proposed controls are not represented as deployed controls.

## Cleanup objective

Remove project-specific chargeable resources and unnecessary identity access while retaining sanitised proof of the work. Stopping an instance is not equivalent to removing all associated cost exposure. Deletion must apply only to inventoried project resources; shared aliases, groups, policies and logging configurations must remain intact unless their removal is explicitly within scope.

## Teardown sequence

1. Export deployed policy JSON and preserve completed test/audit evidence.
2. Record the project resource inventory and confirm ownership through names, IDs and Project tags.
3. Remove operator assignments and perform leaver validation before deleting evidence-bearing identities.
4. Terminate the two simulated EC2 workloads through the administrator.
5. Check EBS volumes, snapshots, allocated IP addresses and any additional resources created for the lab. Delete only unused project-owned items.
6. Remove the project's IAM users, credentials and MFA devices as appropriate. Remove groups after membership/attachments are cleared. Detach and delete project policies after confirming no other identities use them.
7. Remove project-specific federation assignments/permission sets only if implemented and no longer needed.
8. Review custom trail/logging storage and retention if such resources were created. Built-in Event history is not a trail resource to delete.
9. Preserve a pre-existing account alias; remove a new project-only alias only if appropriate.
10. Review final inventories and billing, allowing for usage reporting delay. Record outstanding costs/resources and follow-up actions.

## Cleanup evidence register

| Item | Expected end state | Observed status |
|---|---|---|
| Lab EC2 instances | Terminated | Not evidenced |
| Unused project volumes/snapshots/addresses | Removed or justified retention | Not evidenced |
| Operator access | Removed and tested | Not evidenced |
| Project-only identities/groups/policies | Removed | Not evidenced |
| Optional logging resources | Removed or retained with rationale | Not evidenced |
| Billing and resource inventory | Reviewed | Not evidenced |

## Design lessons established by analysis

The tutorial is useful for learning policy attachment and environment-tag restrictions. It does not, by itself, demonstrate a complete least-privilege program. Start/stop duties justify specific actions, rather than a wildcard service grant. Tags form part of the authorisation model and therefore need change control. Read visibility and write authority are separate. A policy document's intended behaviour must be evaluated alongside every other source of effective access.

Lifecycle management includes session behaviour, not only deletion of a user or group membership. Audit evidence must identify the caller, target and operation, and a screenshot of an empty console is insufficient proof of denied API access. A single-account lab should be described honestly even when its workflow borrows professional governance practices.

These are design conclusions. No actual troubleshooting incident or successful test is asserted without corresponding evidence.

## Handover and submission checks

Confirm that each README link opens, policy examples are labelled accurately, proposed controls are distinguishable from deployed controls, test results have evidence and risk ratings are conditional until validated. Remove credentials, identifying login details and irrelevant screenshots. Retain source attribution. A completed implementation submission additionally requires actual account-specific configuration records and the executed test/cleanup results.

## Git publication

Open the existing repository in VS Code, copy this package's contents into it and review changes. Do not overwrite your `.git` directory or delete your own collected evidence. Run `git status` and `git diff`, stage the reviewed changes, commit with `Document IAM design, implementation manual and validation plan`, then push. The commit should not imply successful implementation when only documentation has changed.
