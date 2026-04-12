---
layout: default
title: values
---

# values

*A manifesto on value-driven development.*

---

## The settled question

Agents can figure out how to build things. That question is answered.

When someone types "build me a SaaS landing page with Stripe checkout"
into Bolt, they aren't writing a spec. They're stating a goal and
trusting the system to derive the implementation. And it works, millions
of times a day, across every zero-shot agentic tool on the market. Bolt,
Lovable, Cursor, Claude Code. You describe what you want, not how to
build it, and the system reads the codebase, picks the files, chooses
the approach, writes the tests, and ships the change.

Specs were invented to do that decomposition for the reader, because the
reader couldn't be trusted with it. The reader can be trusted with it
now. That part is settled.

## The unsettled question

That works for throwaway prototypes. What happens on a project that
matters?

A project with an operator who gets paged at 3am and needs the error
message to tell her something useful. A project where a downstream team
wired you into their build last quarter and now depends on a behavior
you never wrote down. A project where "technically correct and quietly
wrong" has real costs.

The agent still has the implementation judgment. What it doesn't have is
the frame: who does this project serve, what have we promised them, and
what are we trying to accomplish this week?

Nobody is writing that down. Specs don't carry it, because specs were
never designed to carry it. They answer "how should this be built?" and
leave "why does this matter and to whom?" to oral tradition and tribal
knowledge. That worked when the reader was a human who could absorb
context from hallway conversations and code review threads. An agent
has no hallway. It has what you write down and the code.

So the question isn't whether agents have judgment. They do. The
question is what to point that judgment at.

## The frame

Instead of a spec, give the agent two things: **stakeholders** and a
**theme**.

**Stakeholders** are the specific people the project serves, written as
prose, not a checklist. Each one has a first encounter with the project,
a notion of what success looks like, and a reason they'd walk away. The
stakeholder prose isn't an introduction that precedes the real document.
It is the document. There's no hidden spec behind it.

**Themes** are what you're trying to accomplish this week. A theme is
narrower than priorities: where, inside everything that matters, you're
going to spend today. *Get the CLI working end-to-end.* *Stop bleeding
contributors on the onboarding path.*

Between stakeholders and a theme there's usually enough context for the
agent to figure out what to do next, and enough for it to notice when
it was wrong about what to do next.

What about the promises each stakeholder is relying on — the claims?
Those belong in your test suite, not in a document. A claim you can't
run in CI is just a spec by another name. Write tests that encode
stakeholder promises, not just implementation correctness: `stop` always
leaves the working tree on the base branch. Every public type in `ir.rs`
has a `cache_line` field. If CI can't break it, you don't really
value it yet. Your CI pipeline is already the falsification loop — you
just have to be intentional about what you put in it.

## The practice

Value-driven development is a daily practice, not a document you write
once.

Each cycle has three phases. A goal-setter reads the stakeholders, the
theme, and the current state of the project, then picks the single
highest-value change. A builder implements it. A verifier runs an
adversarial pass against the builder's work — did it actually meet the
goal? What could break? — and the builder and verifier loop until the
verifier says the goal has been sufficiently met. CI gates every step.

The goal-setter reads its own recent history each cycle — what it
worked on, which stakeholders benefited — so it can notice when one
stakeholder has been getting all the attention and another has been
quietly neglected. The balance is built into the loop, not bolted on
after the fact.

## Try it

The pattern behind this manifesto is already in wide use. Every
zero-shot agentic tool operates on the same principle: direction at the
goal level, agent-derived implementation. What those tools don't do,
because they're aimed at greenfield work, is carry values forward across
hundreds of cycles on a project that matters.

I've been building a tool called
[lathe](https://github.com/libliflin/lathe) that tries to close that
gap. It reads a project, discovers its stakeholders, and encodes their
needs into specialized agents that run the cycle autonomously — with CI
gating every change. It's early, and it's wrong in ways I haven't
found yet.

But you don't need lathe to try this. Take the spec away from one of
your agents. Hand it stakeholder prose and a theme. Let CI enforce the
claims. Watch what happens for a week.

If it works, the writer's job stops being "decompose the goal into
steps" and starts being "make the goal legible enough that the agent can
decompose it on its own."

If you want to argue with this idea, the
[issues on this repo](https://github.com/libliflin/values/issues) are
where to do it. Tell me where the manifesto is wrong, which objection I
failed to preempt, or which part bounced you off. I'd rather find out in
writing than six months from now in production.
