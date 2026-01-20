Verbal Requirements (As Provided by Stakeholder)

---VR-1---
We need a small, self-hosted platform to run internal services that cannot rely on public cloud infrastructure
Mapped Formal Requirements

FR-1: Platform SHALL host containerized services using an industry-standard container runtime

NFR-5: System SHALL avoid unnecessary orchestration complexity

NFR-6: Platform SHALL run on commodity hardware

Rationale
This requirement establishes the on-prem, self-hosted constraint and drives the choice of Docker-based containerization rather than cloud-managed services or complex orchestration platforms.

---VR-2---
The platform must support stateful workloads with persistent data
Mapped Formal Requirements

FR-2: Platform SHALL support stateful workloads with persistent data surviving container restarts

NFR-2: Loss of a single node SHALL NOT result in total service outage

Rationale
This requirement directly informs the storage architecture and persistence guarantees, ensuring data durability across container lifecycle events and predictable behavior during failures.

---VR-3---
We’ve had incidents caused by node failures and want the system to degrade gracefully rather than completely fail
Mapped Formal Requirements

FR-4: Platform SHALL continue operating in a degraded but predictable state upon failure of a single node

NFR-2: Reliability requirement for partial availability

Rationale
This verbal requirement introduces failure tolerance expectations and explicitly shapes degradation behavior, rather than demanding full high availability.

---VR-4---
Operations should be simple enough that a single engineer can deploy, troubleshoot, and recover the system
Mapped Formal Requirements

FR-6: Single operator SHALL be able to perform deployment, troubleshooting, and recovery

NFR-1: Operability documentation requirement

NFR-5: Simplicity over unnecessary complexity

Rationale
This requirement constrains tooling choices and mandates clear documentation, emphasizing operability over feature richness.

---VR-5---
Observability is required so failures can be detected before users report them
Mapped Formal Requirements

FR-5: Platform SHALL expose health, performance, and resource metrics

NFR-3: Metrics refresh interval requirement

Rationale
This requirement drives the inclusion of monitoring, metrics collection, and alerting capabilities as first-class platform features.

---VR-6---
The environment is resource-constrained and uses commodity hardware
Mapped Formal Requirements

NFR-6: Platform SHALL run on commodity hardware

NFR-5: Avoid unnecessary orchestration complexity

Rationale
This requirement limits acceptable solutions and reinforces design tradeoffs favoring efficiency and simplicity.

---VR-7---
We expect requirements to evolve, so the design should allow incremental improvements rather than a one-time build
Mapped Formal Requirements

NFR-4: Design SHALL allow additional nodes or services with minimal reconfiguration

FR-3: Services SHALL be deployable and updatable without full platform downtime

Rationale
This requirement establishes the need for modularity, versioning, and iterative development, directly influencing lifecycle and architectural decisions.
