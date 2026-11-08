# The CISO's First 90 Days in a Regulated Fintech

*Luciano Ferrari*

Every new security leader arrives with a mental list of things to fix. In a regulated fintech — where PCI DSS, bank-partner audits, state regulators, and card-brand rules all have opinions about your program — that list gets long fast. The temptation is to start fixing on day one.

Don't. The first 90 days are not for fixing. They are for understanding the business, earning the right to be heard, and leaving with a roadmap someone else has agreed to fund.

## Days 1–30: Listen more than you talk

The most useful thing I did in my first month in a payments company was sit with people who were not in security: the head of risk, the compliance officer who lived inside the bank-partner relationship, the engineering leads who shipped the platform, and finance. I asked each of them the same two questions: *where has security helped you, and where has it slowed you down?*

The answers tell you more about the real state of the program than any tool dashboard. If engineering says security is where releases go to die, you have a process problem before you have a technology problem. If compliance says they are the ones writing the security answers for auditors, you have an ownership problem.

Alongside the conversations, build a factual inventory. Not a maturity assessment yet — just facts. What is deployed. What is actually used. Which contracts renew in the next year. What the last pen test found and whether anyone closed it. When backups were last restored from, not just taken. Where regulated data actually lives versus where the data-flow diagram says it lives.

Then write a one-page brief for your CEO or CIO: here is what I found, here is what worries me, here is what I am *not* going to ask for yet. That last line matters. Executives are used to new leaders arriving with a budget request. Arriving without one buys you credibility you will spend later.

## Days 31–60: Quick wins and a tabletop

By the second month you should know the three to five things that are cheap, visible, and genuinely reduce risk. In most companies they are the same: close MFA gaps on privileged and finance accounts, block legacy authentication, burn down the critical patch backlog on internet-facing systems, and confirm that the incident-response phone tree actually has current phone numbers in it.

Do those. Quietly. Then announce them in the context of risk reduced, not work done.

The single highest-leverage activity in this phase is a tabletop exercise with the executive team. Pick a realistic scenario — a ransomware event that takes down the payment platform during month-end, or a business-email compromise that redirects a merchant payout — and walk through it for ninety minutes. Nothing aligns a leadership team faster than discovering, together, that nobody knows who is authorized to take the platform offline, or that the company's position on paying a ransom has never been discussed.

This is also when you establish the risk register with business owners. If every risk is owned by security, nothing will get fixed. Risks need owners who feel the consequence.

## Days 61–90: Commit to a roadmap and present it upward

Now you can write the plan. I structure it in three horizons: **stabilize** (the next two quarters — foundational hygiene and the gaps that would embarrass us in an audit), **mature** (the following year — detection coverage, identity, third-party risk, AI governance), and **differentiate** (the things that make security a reason customers choose us — attestations, transparency, speed of response).

Each line in the roadmap maps to one of three justifications: a regulatory obligation, a material business risk, or a revenue enabler. If it maps to none of those, it does not go in the plan. This discipline is what turns a security budget from a cost center into something a CFO can defend.

Present it to the executive team first, then to the board or audit committee. Keep the board material to one page plus appendix: posture, trend, incidents, decisions needed. Directors do not want a vulnerability count. They want to know whether the company is more or less exposed than last quarter, and what you need from them.

## What I would tell my earlier self

Three things.

First, **recovery capability is the control that matters most on your worst day**. I would move backup immutability and restore testing to the front of every plan.

Second, **write down every decision and risk acceptance**. When a regulator or an auditor asks why something was done a particular way — and in fintech, they will — the answer "we discussed it" is worth nothing. A dated entry with options considered and rationale is worth everything.

Third, **stay technical enough to be dangerous**. Your credibility with engineering depends on it, and your judgment about what is actually risky versus what merely looks risky depends on it even more. Which is a subject for another essay.

---

*A structured 30/60/90 checklist version of this approach lives in my [security-playbooks-templates](https://github.com/lucianoferrari/security-playbooks-templates) repository.*
