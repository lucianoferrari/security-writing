# What Building a CAN Bus IDS Taught Me About Detection Engineering

*Luciano Ferrari*

A few years ago I built [canids](https://github.com/lucianoferrari/canids), a proof-of-concept intrusion detection system for automotive CAN bus traffic, mostly to support the car-hacking training I teach at LufSec. I expected to learn about cars. I ended up learning more about detection engineering in general than in years of SOC reviews.

CAN is a brutally simple environment. There is no authentication, no encryption, and no source address — any node on the bus can send any message with any identifier. If an attacker gets a foothold (through an infotainment unit, a telematics modem, a diagnostic port), they can inject messages that look exactly like the legitimate ones. There is no "bad packet" to signature.

That constraint forces you to think clearly, and the lessons travel.

## 1. When you cannot detect the attacker, detect the deviation

Because an injected CAN frame is byte-for-byte legitimate, the only signal is behavioral: a message ID appearing more often than its normal cadence, a counter that skips, a physical value that changes faster than physics allows, a frame arriving when the ECU that normally sends it is silent.

Enterprise detection has spent too long on the equivalent of signatures — known-bad hashes, known-bad IPs, known-bad command lines. Those have value, but the attackers who matter use legitimate tools and valid credentials. The durable signal is the same as on the bus: deviation from established behavior. A service account logging in from a workstation. An administrator running a backup tool at 3 a.m. that has never run before. A user downloading ten times their normal volume.

## 2. You cannot baseline what you have not inventoried

The first week of the IDS project was spent not writing detection logic but recording normal traffic and mapping which IDs appeared, how often, and with what payload ranges. Without that map, every alert would have been noise.

Most organizations skip this step in their networks and identity systems. They buy a detection platform, turn on the default rules, and drown. The unglamorous work of knowing what normal looks like — which systems talk to which, who is supposed to have admin, what the daily rhythm of the business is — is what makes anomaly detection possible. Asset inventory is not a compliance checkbox; it is the foundation of detection.

## 3. Timing is a feature, not metadata

On the CAN bus, *when* a message arrives is often more informative than *what* it says. Periodic messages have a cadence; an attacker injecting frames disturbs that cadence even when every byte is plausible.

I now ask the same question of every enterprise log source: are we using the timing? Impossible travel, logins outside working pattern, bursts of API calls, changes made seconds after a new session begins — these are timing signals, and they are consistently among the highest-fidelity detections I have seen in real incidents.

## 4. Tune for the operator, not the demo

The first version of canids flagged everything that deviated from baseline. It was impressive in a lab and useless in a car, because real driving produces legitimate deviations constantly. The version that worked suppressed single anomalies and alerted on *correlated* ones — a cadence change *and* a physically implausible value, within a short window.

SOC teams know this pain. A rule that fires on one weak signal creates fatigue; a rule that fires on two or three correlated weak signals creates confidence. Precision is a design choice, and it should be made with the person who has to look at the alert at 2 a.m. sitting beside you.

## 5. Constraints make you a better defender

CAN gave me no choice: no auth, no crypto, no headers to inspect. I had to be creative about the signals that remained. Enterprise defenders have far richer telemetry and, paradoxically, often do less with it because the abundance invites laziness — "we have EDR, so we're covered."

Periodically pretending you have less than you do is a useful exercise. If the EDR were blind, what would tell you an attacker was moving laterally? If you lost the SIEM for a week, which three logs would you want? The answers reveal which signals are truly load-bearing.

## Why a security executive should still build things

I did not build canids because the company needed it. I built it because teaching car hacking honestly requires understanding the defensive side too, and because building something forces a kind of understanding that reading never does.

The result is that when a vendor tells me their platform "uses behavioral AI to detect unknown threats," I know exactly which questions to ask: What is the baseline period? How do you handle legitimate drift? What is the false-positive rate on a real network, not a demo? How many correlated signals before you alert?

Those questions come from having fought with a few thousand CAN frames on a bench. Every security leader should have a project like that somewhere — something small enough to finish, technical enough to be humbling, and relevant enough that the lessons follow you back to the boardroom.

---

*The canids proof of concept is on [GitHub](https://github.com/lucianoferrari/canids). The car-hacking course it supports is at [lufsec.com](https://lufsec.com).*
