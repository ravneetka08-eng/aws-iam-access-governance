# IAM Policy Review and Examples

> **Evidence status:** This document describes the project design and execution procedure. AWS deployment, access-test outcomes and cleanup have not been independently evidenced in the supplied material. Proposed controls are not represented as deployed controls.

## Source and redesigned policies

The source tutorial policy is retained as `source-tutorial-policy.json`. It is a transcription of the provided manual, not evidence of the deployed active policy. Its ec2:* grant is broader than the intended start/stop duties. The redesign uses action-specific permissions and explicit guardrails for selected operations.

| File | Purpose | Status |
|---|---|---|
| source-tutorial-policy.json | Document the starting exercise | Transcribed source |
| development-operator.example.json | Development lifecycle access | Proposed; requires AWS validation |
| production-operator.example.json | Production lifecycle access | Optional proposed extension |
| security-reviewer.example.json | Selected EC2/CloudTrail reads | Optional proposed extension |

## How to use examples

Replace sample account ID `123456789012` and Region `ap-southeast-2` with actual values. Review the scope before attaching. Optionally use exact instance ARNs to avoid granting access to every matching instance in the account/Region. Keep read operations' Resource * where required by AWS. Validate each selected action and condition against the EC2 service authorisation reference and AWS policy validator. Local JSON parsing does not prove authorisation correctness or deployed effectiveness.

The selected read list supports instance inventory but may not support every console panel. Diagnose missing calls and add only justified reads. The reviewer policy includes CloudTrail LookupEvents for recent management-event review; it does not grant broad IAM review, S3 log reading or configuration changes.

## Explanation of policy elements

Version identifies the policy language. Statement holds individual permission rules. Effect is Allow or Deny. Action selects API permissions. Resource specifies target ARN scope. Condition further limits applicability. Sid is a human-readable statement identifier. An explicit deny overrides an applicable allow; a missing allow produces implicit deny.

## Guardrail limits

Explicit tag/termination denies apply to the principals that receive these policies, not every identity in the account. No example authorises IAM writes, but unrelated policies could grant them. The examples do not implement federated trust or MFA enforcement. Trust policies must be designed for the actual identity provider/role architecture rather than copied from an unrelated principal.

## Deployment evidence

After AWS validation and attachment, export the actual policy, record its active version and assignment, and connect it to the tests. Retain the source-versus-redesign comparison. Do not label proposed example JSON as an account export.

## References

- [AWS IAM security best practices](https://docs.aws.amazon.com/IAM/latest/UserGuide/best-practices.html)
- [EC2 service authorisation reference](https://docs.aws.amazon.com/service-authorization/latest/reference/list_ec2.html)
- [EC2 start/stop permissions based on tags](https://docs.aws.amazon.com/IAM/latest/UserGuide/reference_policies_examples_ec2-start-stop-tags.html)
- [CloudTrail event history](https://docs.aws.amazon.com/awscloudtrail/latest/userguide/view-cloudtrail-events.html)
- [AWS policy evaluation logic](https://docs.aws.amazon.com/IAM/latest/UserGuide/reference_policies_evaluation-logic.html)

The source learning exercise is NextWork's *Cloud Security with AWS IAM*, supplied as tutorial text. The exact source URL was not included in that text. The least-privilege redesign, requirements, governance model and validation plan in this repository are extensions to that exercise.
