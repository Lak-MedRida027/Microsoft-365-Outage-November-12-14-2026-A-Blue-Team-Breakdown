# Resilience and Blue-Team Lessons

What this outage should change in how teams think about availability and risk.

## 1. Single points of failure hide in shared infrastructure
Many services shared one gateway path. When it failed, Exchange Online could not
fail away from it, so email had nowhere to go. Shared "front door" infrastructure
is efficient, but it concentrates blast radius. Map where many services depend on
one component.

## 2. Latent defects are time bombs
The bug shipped in July and detonated in November. Changes that pass testing can
still carry defects that only surface under specific load or timing. Treat the
window after any infrastructure change as an extended watch period, not just the
first few hours.

## 3. Safety mechanisms fail too
The partitioning meant to contain the failure did not work because of a separate
issue. A containment control you never exercise under real failure is an
assumption. Test failure-domain isolation the way you test backups: by actually
triggering it.

## 4. Provider uptime is not your business continuity
Some organizations fell back to fax to keep trading. Provider availability and
your continuity are different things. Know your plan B for email, chat, and
identity when a major provider goes dark for a day.

## 5. Availability is a security property
The A in the CIA triad (confidentiality, integrity, availability) failed here as
completely as a breach would compromise the C or the I. Availability belongs in
the security conversation, not only the operations one.

## 6. Every outage is a social-engineering event
Attackers exploited the confusion within hours. Build the phishing surge into your
outage playbook from the start (see [`../soc/phishing-watch.md`](../soc/phishing-watch.md)).
