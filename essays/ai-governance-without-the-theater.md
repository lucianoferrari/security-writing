# AI Governance Without the Theater

*Luciano Ferrari*

Most AI governance programs I have seen fall into one of two failure modes. The first is the committee that meets monthly, produces a principles document with words like "transparency" and "accountability," and has no idea which AI systems the company is actually running. The second is the security team that blocks every AI tool until engineering quietly builds its own and nobody tells security anything.

Both are theater. One performs responsibility; the other performs control. Neither reduces risk.

Having sat on AI governance committees inside a regulated company and having built tooling to test AI systems adversarially, here is the operating model I have found actually works — one that a board will fund and that engineers will not route around.

## Start with an inventory, not a policy

You cannot govern what you cannot see. Before writing a single policy, find out what exists: every chatbot, copilot, embedded AI feature in a SaaS product, internal experiment, and vendor that processes your data through a model. Include the ones people are embarrassed about.

For each, capture five things: what data it touches, what it can do (talk only, or act), who uses it, who owns it, and which model provider is behind it. This takes a few weeks and produces more clarity than a year of principles.

## Tier by consequence, not by technology

Not every AI system deserves the same scrutiny. A tool that summarizes internal meeting notes and a tool that decides which transactions to flag as fraud are not the same risk, even if they use the same model.

I tier by two axes: **data sensitivity** (public, internal, confidential, regulated) and **autonomy** (informs a human, recommends to a human, acts with human approval, acts autonomously). The top-right corner — regulated data, autonomous action — gets a full assessment, adversarial testing, legal review, and committee sign-off. The bottom-left gets a lightweight checklist and an inventory entry. Everything in between scales accordingly.

This is the same proportionality logic every mature risk program already uses. AI does not need a new philosophy; it needs the existing one applied honestly.

## Make the review gate fast and useful

The reason engineers route around governance is that governance is slow and does not help them. The fix is to make the review gate produce something they want.

In practice that means: a checklist they can self-assess against before coming to you, a red-team test set they can run in CI, clear rules about tool permissions and data isolation that are the same every time, and a turnaround commitment — a low-tier system gets a decision in days, not months.

When security shows up with a working test harness that finds a prompt-injection path in an afternoon, engineering stops seeing governance as paperwork and starts seeing it as free QA.

## Govern the vendors, too

A growing share of AI risk arrives through procurement, not engineering. The SaaS vendor that quietly turned on an AI assistant trained on customer data, the HR platform that added automated screening, the analytics tool that now sends your data to a model provider you have never heard of.

Add AI questions to the vendor assessment — does the vendor train on our data, who are the model sub-processors, is there human review for consequential decisions, how are AI features logged — and make "AI processing of our data" a factor that raises a vendor's risk tier.

## Give the committee real decisions

A governance committee exists to make decisions no single function should make alone: what level of autonomy is acceptable for a given use case, which risks the company accepts, when to pause a system. If the committee only receives updates, dissolve it and send an email.

Bring it the hard cases. Bring it the test results. Bring it the incidents. Make its decisions and rationale part of the record — regulators and auditors increasingly want to see *how* decisions about AI were made, not just that a policy existed.

## Measure what matters

Three metrics have been enough for me to tell a board whether the program is working:

1. **Coverage** — what percentage of known AI systems are inventoried and tiered
2. **Testing** — what percentage of medium- and high-tier systems have been adversarially tested in the last twelve months
3. **Incidents and near misses** — how many, how severe, and what changed afterward

If all three are trending the right way, you have governance. If you only have a principles document, you have a poster.

## Why this matters now

Regulators in multiple jurisdictions are converging on the same expectations: know your systems, assess their risk, test them, keep humans accountable for consequential decisions, and be able to show your work. The audit-oriented framing of the responsible-AI governance curriculum I went through for the C|RAGE certification reflected exactly this shift — away from ethics as aspiration and toward governance as evidence.

Companies that build the evidence-producing machinery now will find compliance to be a byproduct. Companies that wait will find themselves reconstructing it under deadline. I know which position I would rather be in when the examiner arrives.

---

*An AI acceptable use policy, an LLM application review checklist, and a vendor questionnaire with AI sections are in my [security-playbooks-templates](https://github.com/lucianoferrari/security-playbooks-templates) repository.*
