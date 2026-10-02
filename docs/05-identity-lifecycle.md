# Identity Lifecycle and Access Review



## Purpose and workflow

Access governance extends beyond creating a user. It establishes a business reason, assigns only approved permissions, removes obsolete entitlements and verifies that access ends when required. All approvals in this lab are simulated and must be described as such.

| Stage | Responsible function | Required record | Exit criterion |
|---|---|---|---|
| Request | Service owner | Job duties, environment and access duration | Business need defined |
| Review | Security reviewer | Least-privilege and segregation check | Excess access removed from request |
| Assign | Identity administrator | Identity, group/role, policy version and MFA status | Assignment recorded |
| Validate | Operator and reviewer | Positive/negative tests | Intended effective access established |
| Review/change | Owner and administrator | Old/new role and entitlements | Obsolete access removed |
| Remove | Administrator | Disable/revoke/remove actions and times | Relevant fresh/existing-session tests completed |

## Joiner procedure

1. Record a synthetic request JML-01 for developer duties and a defined access period.
2. Review the access matrix and identify the developer group/role.
3. Administrator provisions the identity or federation assignment without sharing administrator credentials.
4. Configure unique authentication and MFA. In a user lab, enforce password change at first sign-in.
5. Verify attachments and absence of unexpected policies.
6. Perform TC-01 to TC-09 and preserve evidence.
7. Record the assignment and review trigger. The workflow is documented; no actual approval or completion is claimed here.

## Mover procedure

A simulated promotion from developer to production operator is an access change, not permission accumulation. Record JML-02 and the new responsibilities. Remove the old assignment unless an explicit reviewed business need requires both. Assign the new role, inspect remaining policies and review session behaviour. Test that production access works while old development privileges are no longer available. If old credentials retain access, record and address that condition rather than declaring the move complete.

## Leaver procedure

Record JML-03 and removal time. For an IAM user, remove permissions and group memberships, disable console access and remove any existing access keys. For federated identities, disable the identity/assignment and use supported session-revocation controls where applicable. Account for already-issued role sessions and relevant role policies; do not assume upstream disablement immediately expires all AWS credentials.

Check other possible assignments and credential paths. Test new sign-in and existing session/API access. Record session expiry/revocation and propagation timing. Delete the synthetic identity after retaining sanitised evidence and confirming it is not needed by other lab work.

## Access-review procedure

At project milestones and after policy/tag changes, compare actual identities and assignments with the role matrix. Record requested versus actual permissions, direct grants, group/role membership, MFA state, unused credentials, environment tags and policy versions. Remove unnecessary permissions, then retest affected requirements. The cadence is a proposed lab practice; it is not evidence of an operating organisational review program.

## Exceptions

An IAM user exception is acceptable for this learning scope when federation is unavailable. Record reason, restrictions, absence of access keys, authentication controls and cleanup trigger. Do not describe unavailable controls as implemented. Additional permissions needed by a console screen require action-specific rationale and a repeat of negative tests.

## Lifecycle acceptance

Lifecycle completion requires supported records for joiner, mover and leaver actions and effective-access results. Current status: procedures documented; execution not evidenced.
