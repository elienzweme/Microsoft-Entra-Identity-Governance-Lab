# Microsoft Entra Identity Governance Lab

## Overview

This project demonstrates the implementation of identity governance
controls in Microsoft Entra ID using Access Reviews.

The lab simulates an enterprise access-certification process in which
privileged group membership is periodically reviewed to determine
whether users continue to require administrative access.

The project demonstrates:

- Microsoft Entra ID Governance
- Access Reviews
- Privileged group access certification
- Reviewer recommendations
- Human approval and denial decisions
- Business justification
- Least-privilege remediation
- Removal of unnecessary access
- Audit logging and verification

## Business Scenario

The SG-IAM-Administrators security group provides administrative
access within the identity environment.

The group initially contained:

| Identity | Initial State | Business Context |
|---|---|---|
| Elie Admin | Member | Authorized IAM administrator |
| Test User01 | Member | Simulated stale/inactive access |

An access certification campaign was created to determine whether
both identities continued to require membership.

## Access Review

Access Review:

AR002-SG-IAM-Administrators-Access-Certification

Resource:

SG-IAM-Administrators

Scope:

Everyone

Reviewer:

Lab Admin

Review type:

One-time access certification

Decision assistance:

30-day sign-in activity

Justification:

Required

Automatic application of results:

Disabled

This configuration intentionally separated the review decision from
remediation so that both stages could be demonstrated and audited.

## Review Decisions

Microsoft Entra provided activity-based recommendations.

| Identity | Recommendation | Reviewer Decision |
|---|---|---|
| Elie Admin | Approve | Approved |
| Test User01 | Deny | Denied |

Elie Admin had recently signed in and retained a legitimate
administrative requirement.

Test User01 was identified as inactive and no longer had a valid
business requirement for IAM administrative access.

## Remediation

After completion of the review, the results were manually applied.

The denied decision caused Microsoft Entra Identity Governance to
remove Test User01 from SG-IAM-Administrators.

Before remediation:

SG-IAM-Administrators
├── Elie Admin
└── Test User01

After remediation:

SG-IAM-Administrators
└── Elie Admin

The membership was removed through the Identity Governance workflow
rather than through manual group administration.

## Audit Validation

Microsoft Entra audit logs were reviewed to validate the governance
workflow.

Successful audit events included:

- Create access review
- Approve decision
- Deny decision
- Access review ended
- Apply decision
- Apply review

The Apply Decision event reported:

applyResult: Success

The final group membership was independently verified to confirm that
the denied identity had been removed.

## Governance Workflow

Privileged Group Membership
        ↓
Access Review
        ↓
Microsoft Entra Recommendation
        ↓
Human Reviewer
        ↓
Approve / Deny
        ↓
Complete Review
        ↓
Apply Results
        ↓
Remove Unnecessary Access
        ↓
Audit Verification

## Security Principles Demonstrated

### Least Privilege

Administrative access is retained only when a continuing business
requirement exists.

### Access Certification

Existing access is periodically reassessed rather than assumed to
remain valid indefinitely.

### Human Oversight

Microsoft Entra recommendations support the reviewer but do not
replace the reviewer's decision.

### Separation of Decision and Remediation

Review decisions were completed before remediation was applied.

### Auditability

Review decisions and remediation activities were recorded in
Microsoft Entra audit logs.

## Technologies

- Microsoft Entra ID
- Microsoft Entra ID Governance
- Access Reviews
- Microsoft Entra Security Groups
- Microsoft Entra Audit Logs
- Microsoft Entra Privileged Identity Management (PIM)

## Next Phase

The next phase extends the governance architecture with Privileged
Identity Management and change-management integration.

Planned workflow:

Access Certification
        ↓
PIM Eligible Assignment
        ↓
Jira Change Request
        ↓
PIM Activation Request
        ↓
SG-PIM-Approvers
        ↓
Just-in-Time Privileged Access
        ↓
Conditional Access
        ↓
Audit Validation
