# The SOC Angle: Phishing During the Outage

The outage itself was not malicious, but attackers moved quickly to exploit it.
This is the part that sits squarely in a SOC's lane.

## What was observed
- **Fake outage notices.** Attackers sent emails claiming a user's "held" or
  "queued" mail would be deleted unless they clicked a link to "release" it,
  impersonating Microsoft / Outlook service messaging. (Reported by Messageware.)
- **A targeted phishing campaign.** On November 13, Microsoft Threat Intelligence
  identified a phishing campaign targeting organizations across several US
  industries while the outage was still fresh.

## Why outages are an attacker's opening
A large outage creates the perfect social-engineering conditions: users are
anxious, expecting disruption, waiting for official updates, and more likely to
click something that looks like a fix. Helpdesks are overwhelmed, so verification
is slower. The incident becomes the pretext.

## SOC watch list during and after a major provider outage
- Spoofed Microsoft / Outlook / M365 sender domains and display-name impersonation.
- "Release your held mail", "re-authenticate", "your account will be deleted" lures.
- Newly registered lookalike domains (service-status, mail-release, m365-recovery themes).
- Credential-harvesting pages mimicking the Microsoft 365 or Outlook login.
- MFA-fatigue / push-bombing attempts while users and helpdesks are distracted.
- Spikes in password-reset and support requests that a social engineer can ride.
- OAuth consent-grant phishing ("approve to restore access").

## Practical defender actions
- Pre-write a trusted internal comms channel for outages so users have one source
  of truth that is not email.
- Tighten mail rules and user reporting during the event; expect lure volume to rise.
- Watch authentication logs for unusual sign-ins and consent grants during the window.
- After recovery, review what users clicked while email verification was degraded.

> These are detection ideas to validate in your own environment, not drop-in rules.
