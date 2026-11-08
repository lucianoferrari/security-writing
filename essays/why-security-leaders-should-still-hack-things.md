# Why Every Security Leader Should Still Hack Things

*Luciano Ferrari*

There is a well-worn career arc in security. You start technical — pentesting, network engineering, incident response — and as you move up, you trade the terminal for the slide deck. By the time you are a CISO, the conventional wisdom says your job is strategy, governance, and communication, and the hands-on work belongs to your team.

Most of that is right. The part that is wrong is the implication that you should *stop*.

I have run security for a regulated fintech and for a global software company. I also still teach car hacking, hardware hacking, and LLM prompt hacking, and I still spend weekends with a logic analyzer or a jailbreak test set. I do this not in spite of being an executive but because it makes me a better one. Here is why.

## Judgment about risk is a technical skill

The core job of a security leader is deciding what is actually risky versus what merely looks risky, and spending limited money accordingly. That judgment degrades quickly when it is not grounded in how attacks actually work today.

A leader who has recently watched an LLM agent get talked into emailing data to an attacker-controlled address reads the agentic-AI roadmap differently from one who has only read about it. A leader who has pulled firmware off a device and found hard-coded credentials evaluates the IoT vendor differently. The experience is not about doing the team's job; it is about calibrating the instrument you use to make decisions.

## Vendors can tell when you know

A large portion of the executive security job is buying things. Vendors are very good at describing capability in language that sounds complete. The questions that cut through — what is your false-positive rate on a real network, how do you handle an attacker using valid credentials, show me the detection firing on this specific technique — come from having been on the other side of those claims.

I have saved more budget by asking one well-informed question in a sales call than by any procurement process.

## Engineers extend trust to people who have done the work

Security's relationship with engineering is where most programs succeed or fail. Engineers will accept constraints from someone who clearly understands the system; they will route around constraints from someone who clearly does not.

When I can sit in a design review and point to the exact place a retrieval index leaks across tenants, or explain why a shared service token is the real problem rather than the prompt, the conversation changes. Security stops being the department of no and becomes the colleague who found the bug before the attacker did.

## Teaching is the best forcing function

The reason I never stopped is that I never stopped teaching. You cannot teach car hacking to a room of practitioners from a slide you have not personally validated on a bench. You cannot run an AI red-teaming workshop like Break the Bot if the bypasses you demonstrate stopped working six months ago.

Teaching forces currency. It also forces clarity — if you cannot explain a technique simply enough for someone to reproduce it, you probably do not understand it as well as you think. Both qualities transfer directly to explaining risk to a board.

## How to do it without neglecting the actual job

The objection is always time. Here is what has worked for me.

**Pick one domain and go deep, not wide.** You cannot stay current on everything. Choose the area most relevant to your company's risk — for me, right now, that is AI security — and let the team cover the rest.

**Build something small.** A proof-of-concept detection, a test harness, a lab. Finishing something is more valuable than reading ten things. My CAN bus IDS was a weekend project that taught me more about detection engineering than years of vendor briefings.

**Make it visible, carefully.** Share what you learn with your team and with the community — talks, writing, a GitHub repo. It signals to your team that technical depth is valued, and it builds the external credibility that opens doors. Just be clear that you are learning alongside them, not auditing them.

**Protect the time like a board meeting.** A few hours a week, scheduled, not negotiable. The strategy work will expand to fill whatever you give it; the technical work will not happen unless you defend it.

## The payoff

The security leaders I admire most share a trait: they can walk into a boardroom and into an engineering stand-up on the same day and be credible in both. That range is not a personality trait. It is maintained, deliberately, by people who decided that moving up did not mean moving away from the work.

Keep hacking things. Your board, your engineers, and your own judgment will all be better for it.

---

*More on how this plays out in practice: [What Building a CAN Bus IDS Taught Me About Detection Engineering](what-a-can-bus-ids-taught-me-about-detection.md) and [Prompt Injection Is a Business Risk, Not a Bug](prompt-injection-is-a-business-risk.md).*
