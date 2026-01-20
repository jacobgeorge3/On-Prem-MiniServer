---Scenario 1: Worker Node Failure---

Event
Physical node hosting stateful containers becomes unreachable.

Expected Behavior

Stateless services continue running on remaining node.

Stateful services become unavailable but do not corrupt data.

Monitoring system reports node failure within 30 seconds.

Validation Steps

Power off worker node

Observe service availability

Check metrics and alerts

Restore node and verify data integrity

Outcome

System entered degraded state without full outage.

Validated Requirements: 
FR-4: The platform SHALL continue operating in a degraded but predictable state upon failure of a single node.

Validation
Stateless services remain available while stateful services become unavailable without data corruption, demonstrating controlled degradation rather than total failure.

NFR-2 (Reliability): Loss of a single node SHALL NOT result in total service outage, though reduced functionality is acceptable.

Validation
The remaining node continues servicing requests, confirming partial availability under node failure.

FR-5: The platform SHALL expose health, performance, and resource metrics for all running services.

Validation
Monitoring detects node failure within 30 seconds and surfaces the condition without manual inspection.

NFR-3 (Performance): The monitoring system SHALL refresh metrics at least every 15 seconds.

Validation
Node failure is detected within the expected monitoring interval

---Scenario 2: Storage Service Failure (NFS Down)---

Event
Shared storage service becomes unavailable.

Expected Behavior

Containers depending on storage fail predictably.

Errors are logged and observable.

No silent data corruption occurs.

Validation Steps

Stop NFS service

Attempt write operation

Observe container behavior

Review logs and metrics

Validated Requirements: 
FR-2: The platform SHALL support stateful workloads with persistent data surviving container restarts.

Validation
Storage-dependent containers fail predictably without corrupting existing data, and data integrity is preserved once storage is restored.

FR-4: The platform SHALL continue operating in a degraded but predictable state upon failure of a single node.

Validation
Only services dependent on the failed storage subsystem are impacted; unrelated services remain operational.

FR-5: The platform SHALL expose health, performance, and resource metrics for all running services.

Validation
Storage failure is observable via logs and metrics rather than silent failure.

NFR-2 (Reliability): Reduced functionality is acceptable, but total outage is not.

Validation
Failure is localized to affected workloads and does not cascade.

---Scenario 3: Misconfiguration Deployment---

Event
Operator deploys a container with incorrect volume mapping.

Expected Behavior

Service fails fast.

Error is observable through logs and monitoring.

Other services remain unaffected.

Rationale
Simulates real-world human error — the most common failure mode.

Validated Requirements: 
FR-6: The platform SHALL allow a single operator to perform deployment, troubleshooting, and recovery tasks using documented procedures.

Validation
The operator can identify misconfiguration via logs and monitoring and correct the issue without impacting other services.

FR-5: The platform SHALL expose health, performance, and resource metrics for all running services.

Validation
Deployment errors are visible through logs and monitoring rather than hidden failures.

NFR-1 (Operability): A new operator SHALL be able to understand system architecture and operational procedures using repository documentation alone.

Validation
Misconfiguration is diagnosed and corrected using documented procedures without external tooling or tribal knowledge.

NFR-5 (Simplicity): The system SHALL avoid unnecessary orchestration complexity.

Validation
Misconfiguration affects only the targeted service and does not introduce systemic instability.

---Scenario 4: Resource Exhaustion---

Event
One service consumes excessive disk or memory.

Expected Behavior

Monitoring surfaces resource pressure.

Operator can identify offending container.

System does not cascade into full failure.

Validated Requirements: 
FR-5: The platform SHALL expose health, performance, and resource metrics for all running services.

Validation
Disk or memory pressure is surfaced through monitoring before full system failure.

NFR-2 (Reliability): Loss of partial functionality SHALL NOT cascade into total service outage.

Validation
Resource exhaustion is contained to the offending service without platform-wide failure.

NFR-3 (Performance): Monitoring metrics SHALL refresh at least every 15 seconds.

Validation
Resource pressure is observable quickly enough to allow operator intervention.

FR-6: Single operator SHALL be able to troubleshoot and recover the system.

Validation
Operator can identify the offending container and take corrective action using documented procedures.

---Postmortem Template---
Incident Summary:
Root Cause:
Detection Method:
Impact:
Resolution:
Preventive Actions:

## Validation Coverage Summary

All failure scenarios map to one or more functional or non-functional requirements.
Core reliability, operability, observability, and degradation requirements are explicitly validated through controlled fault injection.

