# BRACKEN Control Plane

**Configuration and coordination for BRACKEN infrastructure.**

The BRACKEN Control Plane is intended to provide the management APIs and coordination services used to configure BRACKEN nodes and services. It translates operator intent into versioned, auditable desired state and coordinates delivery of that state to the components responsible for execution.

> **Project status:** Early-stage project. API shape, storage model, authentication design, and availability model are not yet finalized.

## Responsibilities

- Define management APIs for nodes, services, and network policies.
- Validate configuration before it is distributed.
- Track desired and reported state, including configuration versions.
- Coordinate service lifecycle and configuration rollout.
- Report node health and rollout status to operators.
- Enforce authentication, authorization, and audit requirements.

## Architecture boundary

The control plane manages configuration; it should not process user packets. It communicates with the [data plane](https://github.com/vayun-networks/bracken-data-plane) and [network engine](https://github.com/vayun-networks/bracken-network-engine) through explicit interfaces. It can coordinate virtualization through [bracken-virtualization](https://github.com/vayun-networks/bracken-virtualization), while the implementation of shared contracts belongs in [bracken-core](https://github.com/vayun-networks/bracken-core).

The system must distinguish operator intent from observed state and make partial failures visible. A configuration rollout should support validation, versioning, status, and a documented recovery path rather than silently leaving nodes inconsistent.

## Design principles

- Secure APIs by default with explicit identity and authorization boundaries.
- Make changes auditable and attributable.
- Prefer idempotent operations and versioned configuration.
- Validate before applying and report convergence status.
- Design for disconnected or delayed nodes without hiding stale state.

## Planned milestones

Start with a documented API and configuration schema, then implement single-node registration and validated configuration delivery. Multi-node coordination, high availability, and advanced orchestration should follow only after basic state transitions and recovery behavior are well defined.

## Development

No server, database, API, or deployment commands are defined yet. Contributions should include API examples, compatibility notes, security considerations, and the observable behavior on success and failure.

## Related components

- [bracken-core](https://github.com/vayun-networks/bracken-core) — shared contracts
- [bracken-data-plane](https://github.com/vayun-networks/bracken-data-plane) — packet handling
- [bracken-network-engine](https://github.com/vayun-networks/bracken-network-engine) — routing and network configuration
- [bracken-observability](https://github.com/vayun-networks/bracken-observability) — platform health signals
- [bracken-deploy](https://github.com/vayun-networks/bracken-deploy) — rollout and provisioning