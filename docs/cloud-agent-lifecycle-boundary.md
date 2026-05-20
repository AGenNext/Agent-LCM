# Cloud agent lifecycle boundary

Agent-LCM owns lifecycle management for AGenNext agents, runtimes, and managed infrastructure.

## Decision

Agent-LCM coordinates lifecycle stages across provisioning, deployment, operations, upgrade, recovery, and decommissioning.

It does not replace Agent-deploy, Agent-Runtime, Agent-Security, or Agent-Compliance.

## Boundary

| Component | Responsibility |
|---|---|
| Agent-LCM | Lifecycle states, transitions, lifecycle policies |
| Agent-deploy | CI/CD and deployment execution |
| Agent-Runtime | Runtime execution and profile operation |
| Agent-Security | Security gates and hardening validation |
| Agent-Compliance | Compliance evidence and control mapping |
| Agent-Traces | Timeline and audit events |
| Agent-Runs | Past execution debugging and replay |

## Lifecycle stages

Agent-LCM owns lifecycle definitions for:

- planned
- provisioned
- hardened
- deployed
- active
- degraded
- recovering
- upgrading
- suspended
- decommissioning
- decommissioned

## Cloud agent lifecycle

For a k8smicro deployment on OVH/Kimsufi:

```txt
planned
  ↓
server_registered
  ↓
security_preflight_passed
  ↓
k3s_installed
  ↓
surrealdb_deployed
  ↓
runtime_active
  ↓
monitored
  ↓
upgraded / recovered / decommissioned
```

## Flow

```txt
Cloud Architect Agent creates lifecycle plan
  ↓
Agent-LCM tracks lifecycle state
  ↓
Agent-Eval validates plan quality
  ↓
Agent-Security validates gates
  ↓
Agent-deploy performs deployment
  ↓
Agent-Runtime executes runtime workflows
  ↓
Agent-Traces records lifecycle events
```

## Rule

Agent-LCM owns lifecycle state and lifecycle policy.

Execution remains in Agent-Runtime and Agent-deploy.
