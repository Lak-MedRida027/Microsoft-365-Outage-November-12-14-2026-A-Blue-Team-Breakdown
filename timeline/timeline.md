# Timeline (UTC)

Summarized from Microsoft's preliminary Post-Incident Report (Nov 15, 2026) and
public reporting. Times are UTC. Treat as preliminary until Microsoft's final
report.

| When (UTC) | Event |
|---|---|
| **July 2026** | A Windows update is deployed to the Microsoft 365 networking gateway servers, introducing a previously undetected lock-contention bug. |
| **Nov 12, 01:07** | Teams automatically fails over from its alternative gateway to the primary gateway, which also serves Exchange Online. Traffic on that gateway rises. |
| **Nov 12, 16:20** | The outage begins. Connection requests queue as the gateway servers exhaust capacity. Exchange Online cannot fail away from the faulty gateway. |
| **Nov 12, ~17:54** | Microsoft posts its first public acknowledgement and apology, naming a network-capacity upgrade. |
| **Nov 13, 07:20** | A patch is deployed to the gateway servers. |
| **Nov 13, 16:10** | Services restored. Total impact window ~23 hours 50 minutes. |
| **Nov 13 (day two)** | Microsoft Threat Intelligence flags a phishing campaign exploiting the outage, targeting several US industries. |
| **Nov 15** | Microsoft publishes its preliminary Post-Incident Report. |
| **~Nov 20** | Final Post-Incident Report expected. |

**Tracking IDs:** EX1550543 (Exchange Online), MO1550821 (Microsoft 365).

> Note: a few outlets reported slightly different headline durations (for example
> "36 hours" or "Nov 12-14") because recovery tails and mailbox backlogs ran past
> the formal impact window. Microsoft's own record is the ~23h 50m window above.
