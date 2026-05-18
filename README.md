# Agent LCM

Agent LCM is the lifecycle management adapter layer between enterprise HRMS/IAM systems and Agent Platform.

LCM means Lifecycle Management.

## Purpose

Agent LCM maps company identity, employment, role, team, access, and lifecycle events into Agent Platform.

It ensures agents, humans, workspaces, roles, permissions, and approvals are synchronized with enterprise systems.

## Responsibility

Agent LCM owns:

- HRMS adapter contracts
- IAM adapter contracts
- SCIM-style provisioning contracts
- user lifecycle mapping
- agent lifecycle mapping
- role and group mapping
- workspace/team mapping
- access provisioning
- access deprovisioning
- suspension and termination handling
- identity verification state
- audit trail requirements
- joiner/mover/leaver workflows

## Example Upstream Systems

HRMS:

- Workday
- BambooHR
- Darwinbox
- Zoho People
- SAP SuccessFactors
- Rippling

IAM/IdP:

- Okta
- Microsoft Entra ID
- Google Workspace
- Auth0
- Keycloak
- JumpCloud

## Relationship to Agent Platform

```text
Enterprise HRMS/IAM
  → Agent-LCM adapters
  → Agent-Platform identity and access model
  → Agent-Runtime access enforcement
  → Agent-Dashboard visibility
```

## Boundary

Agent-LCM does not own runtime execution.

Agent-LCM owns lifecycle and identity synchronization.

Agent-Runtime enforces access decisions at runtime.

## Core Principle

```text
Enterprise identity changes must propagate to agent platform access quickly, safely, and audibly.
```

## Final Rule

No human, agent, tool, or workspace access should remain active after the upstream lifecycle state says it should be suspended, removed, or reviewed.
