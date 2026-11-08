# Prompt Injection Is a Business Risk, Not a Bug

*Luciano Ferrari*

When I run my Break the Bot workshop, the first thing participants learn is how quickly a well-behaved assistant can be talked out of its instructions. A few lines of carefully worded text and the model that was supposed to answer only questions about a product catalog is cheerfully summarizing the system prompt, or following instructions it found inside a PDF someone uploaded.

The second thing they learn is more uncomfortable: there is no patch for this.

## Why there is no patch

Traditional vulnerabilities have a root cause in code. SQL injection exists because untrusted input is concatenated into a query; parameterize the query and the class of bug disappears. Prompt injection exists because a language model has a single channel for both instructions and data. The developer's instructions, the user's message, the retrieved document, and the tool's output all arrive as text, and the model does its best to reconcile them. There is no parameterized query for natural language.

Model providers have made real progress with training and system-prompt hierarchy, and input and output filters catch the obvious attempts. But every filter I have tested in the last two years has been bypassable with enough creativity — encoding, translation, multi-turn escalation, splitting the payload across a retrieved document and a user message. If your security model for an AI feature is "the filter will catch it," you do not have a security model.

## What this means for a security leader

The reframe that helped me is this: **treat the model as an untrusted component that will, eventually, do what an attacker tells it to.** Then ask what happens next.

If the model can only talk, the consequence of a successful injection is embarrassing output. That is a reputational and compliance problem, and it is manageable.

If the model can *act* — call tools, query databases, send emails, move money, change records — then the consequence of a successful injection is whatever those tools can do with the credentials they hold. That is where real losses happen, and it is where most of the current rush toward agents is heading without enough thought.

So the risk is not the injection. The risk is the blast radius of what the injected model is allowed to do.

## The controls that actually work

In practice, the controls that reduce this risk are architectural and organizational, not clever prompts.

**Least privilege for tools.** Every tool an agent can call should run with the minimum permissions for the task, ideally scoped to the specific user, never with a shared administrative token. This is the single most important control and the one most often skipped because it is inconvenient.

**Isolation of untrusted content.** Retrieved documents, web pages, emails, and tool results should be clearly delimited and treated as data. Some teams render them in a different format, strip instruction-like content, or pass them through a separate model that summarizes rather than executes. None of this is perfect, but it raises the cost.

**Human confirmation for consequential actions.** Payments, deletions, external communications, and changes to access should require a person to approve — and the approval screen must show enough context that the person can actually tell what they are approving. A confirmation dialog that says "Proceed?" is theater.

**Allow-lists for destinations.** If the agent can only email internal domains and only call pre-approved endpoints, exfiltration becomes much harder regardless of what the model is persuaded to try.

**Tenant-aware retrieval.** If a RAG system shares one index across customers and relies on the model to "only use documents from this customer," it is a data breach waiting for a prompt. Authorization belongs in the retrieval layer, enforced in code.

**Full tracing and a kill switch.** When — not if — something goes wrong, you will need the exact prompt, context, model version, and tool calls to understand it, and you will need to turn the feature off in minutes.

## Governance is part of the control set

The organizational half matters as much as the technical half. Someone has to know which AI systems exist, what data they touch, and what they can do. Someone has to decide which use cases are acceptable without a human in the loop. Someone has to test these systems adversarially before they reach production and again when the model or the tools change.

That is why I built AI Risk Inspector around *testing and evidence* rather than policy documents: a governance program that cannot show how a system behaved under attack is not governance, it is paperwork. And it is why the responsible-AI governance material I studied for the C|RAGE certification resonated — the audit-oriented framing is exactly what regulators are starting to ask for.

## The conversation to have with your executives

If you are the security leader, the message to your leadership is not "AI is dangerous." It is: *AI features that only talk are a moderate risk we can manage with monitoring. AI features that act carry whatever risk the actions carry, and we need to design and fund the controls accordingly before we ship them.*

Framed that way, prompt injection stops being a curiosity from a conference talk and becomes what it is — a business risk with a cost, an owner, and a set of controls that either exist or do not.

---

*A pre-production review checklist and an incident playbook for LLM applications are in my [security-playbooks-templates](https://github.com/lucianoferrari/security-playbooks-templates) repository. A demo of AI Risk Inspector is [here](https://youtu.be/0Lm11OSdJnw).*
