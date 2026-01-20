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

---Scenario 3: Misconfiguration Deployment---

Event
Operator deploys a container with incorrect volume mapping.

Expected Behavior

Service fails fast.

Error is observable through logs and monitoring.

Other services remain unaffected.

Rationale
Simulates real-world human error — the most common failure mode.

---Scenario 4: Resource Exhaustion---

Event
One service consumes excessive disk or memory.

Expected Behavior

Monitoring surfaces resource pressure.

Operator can identify offending container.

System does not cascade into full failure.

---Postmortem Template---
Incident Summary:
Root Cause:
Detection Method:
Impact:
Resolution:
Preventive Actions:
