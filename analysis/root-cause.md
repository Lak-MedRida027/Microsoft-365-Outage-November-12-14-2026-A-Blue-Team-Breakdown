# Root Cause Analysis

Microsoft's preliminary Post-Incident Report attributes the outage to three
factors that aligned. Summarized in my own words; verify against Microsoft's
final report.

## The front door: networking gateway servers
Microsoft 365 connections pass through networking gateway servers, the "front
door" to Exchange Online and many other services. A fault here has an unusually
wide blast radius because so many services depend on the same path.

## Factor 1 — a latent bug (July 2026)
A Windows update deployed to the gateway servers in July 2026 introduced a
previously undetected defect, described in reporting as a lock-contention bug. It
produced no visible symptoms for roughly four months and was not caught by
monitoring or testing before it detonated.

**Takeaway:** a change that passes every test can still carry a latent defect that
only surfaces under specific load or timing conditions.

## Factor 2 — a routine Teams failover (the trigger)
About 15 hours before the outage, Teams automatically failed over from its
alternative gateway to the primary gateway, which also serves Exchange Online.
The additional traffic pushed the dormant bug into failure: new connection
requests queued until the servers exhausted their processing capacity.

**Takeaway:** the trigger was normal, healthy operations, not an attacker or a
malicious input.

## Factor 3 — failed containment (the spread)
Partitioning between components and regions was designed to contain a failure
like this. A separate issue prevented the partitioning from working, so the
outage spread globally. Automated health checks pulled failing servers offline,
which concentrated load on the servers still running and accelerated the cascade.
Exchange Online, unable to fail over away from the faulty gateway, had nowhere to
route mail.

**Takeaway:** a containment control that is never exercised under real failure is
an assumption, not a guarantee.

## Not a cyberattack
Microsoft reported no indication of malicious activity or AI-agent involvement.
The defect was specific to the gateway servers and does not affect general
Windows deployments; customer tenants required no changes.

## Remediation
A patch was deployed to the gateways at 07:20 UTC on November 13, with the impact
window closing that afternoon. Microsoft said a final Post-Incident Report with
root cause and defense-in-depth actions would follow.
