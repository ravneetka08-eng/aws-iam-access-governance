# Access Model and Security Design

> **Evidence status:** This document describes the project design and execution procedure. AWS deployment, access-test outcomes and cleanup have not been independently evidenced in the supplied material. Proposed controls are not represented as deployed controls.

## Design approach

RBAC groups identities by responsibilities. Resource-tag-based ABAC narrows lifecycle operations to resources with the appropriate Env value. The combination expresses both who performs the job and which environment they may operate. The current source exercise has one developer group; production operator and security reviewer are proposed extensions.

## Access matrix

| Capability | Developer | Production operator | Security reviewer | Administrator |
|---|---|---|---|---|
| Selected EC2 metadata | Allow | Allow | Allow | Administrative scope |
| Start/stop development | Allow | Not granted | Not granted | Administrative scope |
| Start/stop production | Deny | Allow | Not granted | Administrative scope |
| Create/delete EC2 tags | Deny | Deny | Not granted | Approved changes only |
| Terminate instances | Deny | Deny | Not granted | Approved cleanup |
| Read CloudTrail event history | Not granted | Not granted | Allow | Administrative scope |
| Modify IAM assignments/policies | Not granted | Not granted | Not granted | Approved changes only |

“Not granted” means the proposed permissions do not allow the action. Other policies can alter effective access. “Deny” is an explicit deny for the indicated action in the supplied examples.

## Identity and authentication

For the base exercise, a dedicated IAM user receives permissions through a group. Console login must use a unique password and MFA where supported. No access key is required for this console lab. Password change at initial sign-in should remain enabled for a newly provisioned user.

For a workforce deployment, prefer federated access with temporary credentials, typically through IAM Identity Center or an existing identity provider. An IAM user is a documented educational exception. Account alias creation only improves the sign-in address; it does not add security permissions or authentication assurance.

A permissions policy answers what a principal can do. A role trust policy answers who can assume a role. A group is not an assumable role and does not issue temporary credentials. Federation must include the appropriate trust/assignment design, not simply a renamed group.

## Tags and resource scope

Use the source tutorial's case-consistent tags: `Env=development` and `Env=production`. Add `Project=iam-access-governance` for inventory and cleanup, but recognise that the supplied permission examples enforce Env, not Project. Their lifecycle scope covers all matching instances in the selected account and Region; use explicit instance ARNs if narrower resource selection is required.

IAM is global; EC2 and Event history are Region-oriented. Policy examples use Sydney (`ap-southeast-2`) as a design assumption, not a verified deployment Region. Replace it if the existing resources are elsewhere.

## Policy decisions

| Decision | Reason | Trade-off |
|---|---|---|
| Replace ec2:* with specific actions | Match developer responsibilities | Extra console reads may require reviewed additions |
| Allow selected Describe calls with Resource * | These reads are useful and commonly require wildcard resource scope | Metadata from both environments may be visible |
| Apply Env condition to start/stop | Restrict lifecycle access by environment | Tags must be governed |
| Explicitly deny production lifecycle changes | Keep this boundary despite an accidental overlapping allow | Administrators can still change the policy |
| Explicitly deny tag modification | Reduce relabelling bypass risk | Operators need an administrator for tag corrections |
| Explicitly deny termination | Prevent destructive workload removal | Cleanup remains an administrator responsibility |
| Do not grant IAM administration | Separate workload operation from identity control | Accumulated permissions still need review |

## Evaluation and limitations

An applicable explicit deny overrides an allow. An absent applicable allow results in implicit deny. Missing or unexpected Env values do not satisfy the development allow. The source wildcard policy cannot be interpreted as safe permission for every EC2 operation because supported resource types and conditions vary by action.

These policies are identity policies, not SCPs, permissions boundaries or a guarantee against administrators. This project does not enforce MFA through a policy example. MFA configuration and a genuine pre-MFA/post-MFA enforcement test are distinct activities; any claim of enforcement requires its own validated design.

## Threat cases

Accidental production shutdown is addressed by lifecycle restrictions. Deliberate retagging is addressed by tag denies. IAM self-escalation is addressed by absence of IAM write grants and assignment review. Unauthorised metadata viewing is not fully addressed because selected Describe calls remain broadly readable. Compromised administrator credentials are outside this policy boundary and require broader identity controls.

## References

- [AWS IAM security best practices](https://docs.aws.amazon.com/IAM/latest/UserGuide/best-practices.html)
- [EC2 service authorisation reference](https://docs.aws.amazon.com/service-authorization/latest/reference/list_ec2.html)
- [EC2 start/stop permissions based on tags](https://docs.aws.amazon.com/IAM/latest/UserGuide/reference_policies_examples_ec2-start-stop-tags.html)
- [CloudTrail event history](https://docs.aws.amazon.com/awscloudtrail/latest/userguide/view-cloudtrail-events.html)
- [AWS policy evaluation logic](https://docs.aws.amazon.com/IAM/latest/UserGuide/reference_policies_evaluation-logic.html)

The source learning exercise is NextWork's *Cloud Security with AWS IAM*, supplied as tutorial text. The exact source URL was not included in that text. The least-privilege redesign, requirements, governance model and validation plan in this repository are extensions to that exercise.
