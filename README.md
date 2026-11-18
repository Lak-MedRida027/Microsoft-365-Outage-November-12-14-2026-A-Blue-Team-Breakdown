# Microsoft 365 Outage, November 12-14, 2026 — A Blue-Team Breakdown

A defender-focused study of the global Microsoft 365 outage that took Outlook,
Teams, and Copilot offline for nearly 24 hours across 74 countries. Not a
cyberattack: a latent bug, a routine failover, and a containment failure that
lined up at the worst possible time.

Part of my **Learning in Public** series. I rebuild notable incidents, attacks
and outages alike, into a timeline, a root-cause write-up, and the lessons a SOC
or IR team should take away.

> **Sources and credit.** This repository summarizes **Microsoft's preliminary
> Post-Incident Report (dated November 15, 2026)** and public reporting from
> outlets including WindowsForum, Al Jazeera, BleepingComputer, and others. All
> findings are theirs; this is written in my own words for learning. Microsoft's
> final Post-Incident Report was expected by November 20, 2026, so treat the root
> cause here as preliminary and verify against Microsoft's final report.

---

## TL;DR

| Field | Value |
|---|---|
| Incident window | Nov 12, 16:20 UTC to Nov 13, 16:10 UTC (~23h 50m) |
| Services | Exchange Online (worst hit), Teams, Copilot, SharePoint, OneDrive, Intune, Purview, more |
| Scope | ~74 countries; businesses, airlines, banks, courts, governments |
| Root cause | Latent gateway bug (July 2026) + Teams failover + failed containment |
| Cyberattack? | No. Microsoft found no indication of malicious activity |
| Tracking IDs | EX1550543, MO1550821 |
| Follow-on risk | Opportunistic phishing during and after the outage |

**One line:** prevention was never the issue here. A change nobody caught for four
months did more damage than most breaches, and attackers used the chaos as cover.

---

## What happened

Microsoft 365 traffic flows through networking gateway servers, effectively the
front door to Exchange Online and many other services. Three failures combined:

1. **A latent bug (July 2026).** A Windows update deployed to the gateway servers
   in July 2026 introduced a previously undetected lock-contention defect. It
   caused no visible harm for four months.

2. **A routine Teams failover (the trigger).** About 15 hours before the outage,
   Teams automatically failed over to the primary gateway, the same one that
   serves Exchange Online. The added traffic pushed the dormant bug into failure.
   Connection requests queued until the servers exhausted their capacity.

3. **Failed containment (the spread).** Partitions between components and regions
   were meant to box the failure in. A separate issue prevented that, so the
   outage spread globally. Exchange Online could not fail over away from the
   faulty gateway, so email had nowhere to go.

It was not a cyberattack. But the outage became cover for social engineering (see
[`soc/phishing-watch.md`](soc/phishing-watch.md)).

---

## Repository contents

| Path | What's inside |
|---|---|
| [`timeline/timeline.md`](timeline/timeline.md) | Minute-by-minute timeline (UTC) |
| [`analysis/root-cause.md`](analysis/root-cause.md) | The three-factor root cause in detail |
| [`soc/phishing-watch.md`](soc/phishing-watch.md) | Opportunistic phishing + SOC watch list |
| [`lessons/resilience-lessons.md`](lessons/resilience-lessons.md) | Blue-team and resilience takeaways |
| [`assets/MS365_Outage_Nov2026_Carousel_Rida.pdf`](assets/MS365_Outage_Nov2026_Carousel_Rida.pdf) | 10-slide LinkedIn carousel |

---

## Why this one

My focus is SOC operations, detection engineering, and incident response. This
incident is a clean study in availability as a security property: cascading
failure, shared-infrastructure blast radius, and the opportunistic phishing that
follows every large outage.

---

## Author

**Mohammed Rida Lakhdari** — Information Security Engineering student, Purple Team instructor.

- Portfolio: https://rlak.vercel.app
- GitHub: https://github.com/Lak-MedRida027

*Learning in Public. Summary of Microsoft's preliminary post-incident report and public reporting; all credit for the original findings is theirs.*
