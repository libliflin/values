---
layout: default
title: values
---

# values

*A manifesto on value-driven development.*

---

## The thesis

I write specs for a living. Requirements docs, design docs, tickets, the
whole kit. For a human team they mostly work, and I don't see myself
putting down the pen anytime soon.

What I've started to notice is that when the reader is an agent, my specs
answer the wrong question. I'm writing down *how* to build the thing,
step by step, and the agent is already good at that part. Give it a
codebase and a goal and it will figure out the implementation. That's
what agents do now. Millions of people prove it every day with tools like
Bolt, Lovable, and Cursor: you describe what you want, not how to build
it, and the system derives the rest.

The question the agent can't answer on its own is *why any of this
matters, and to whom*. That's the part my documents have been leaving
out, because specs were never designed to carry it.

## What this is for

A narrow thing: pushing an existing, scoped project forward with an agent
doing the work.

Big questions like microservices versus monolith, which market to target,
or whether to build this thing at all, all belong to the owner. They get
decided in other rooms. My question is smaller: what do you hand an agent
each cycle so it can push the project in a direction the owner would
recognize as progress?

This isn't an argument against specs. Specs remain the right tool
whenever you need a document you can cite in a review: regulated
industries, audited interfaces, cross-team contracts that have to
survive personnel changes. What I'm saying is that for the daily work of
pushing a scoped project forward, the spec is operating at a level the
agent no longer needs help with. You're writing implementation details
for a reader that's better at implementation details than you are.

The short answer is that you need much less than you'd think, and what
you need is at a higher altitude than you'd expect.

## What a spec actually is

A spec answers the question "how should this be built?" It decomposes a
goal into steps, names the components, specifies the interfaces.
That decomposition used to be the hard part. It isn't anymore.

Hand an agent a codebase and the sentence "add runtime bounds checking
for array indexing" and it will read the IR, find the indexed-access
instructions, figure out where to thread the length through, emit the
guard, write the tests, and document the ambiguities it found along the
way. You didn't need to tell it which file to edit or which instruction
to emit. It derived all of that from the goal and the code.

The spec was supposed to save the reader from having to figure that out.
The reader can figure it out now. So the spec is answering a question
nobody is asking anymore, and in the meantime, the question nobody is
answering, who does this serve and what are we trying to protect, goes
unwritten.

Specs also drift, and that drift hits agents harder than it hits humans.
A human catches a stale paragraph and mentally skips it. An agent reads
every sentence as authoritative regardless of whether it still matches
reality. But drift is a symptom, not the disease. Specs drift because
implementation details change faster than anything else in a project.
The higher up you write, the slower the document ages.

## What I'd rather give them

**Stakeholders.** The specific people the project serves, named concretely
enough that I can picture one of them having a bad morning. Maybe it's
the operator who gets paged at 3am and needs the error message to tell
her something useful. Or the contributor opening the repo for the first
time on a Sunday afternoon, deciding in ninety seconds whether this
project is worth her weekend. Or the downstream team that wired us into
their build last quarter and now depends on a behavior we never wrote
down.

Each stakeholder has a first encounter with the project and some notion
of what success looks like for them. They also have a reason they'd walk
away. That last one is the one I most often forget to write down. If I
can't name it, I'm not ready to ask an agent to act on her behalf.

Personas aren't a new idea. What's different here is that the stakeholder
prose isn't an introduction that precedes the real document. It is the
document. There's no hidden spec behind it that the prose is summarizing.
The stakeholders, the claims, and this week's theme are all the agent
gets, and they have to be load-bearing on their own.

**Claims.** The promises each stakeholder is relying on, written concretely
enough that something can actively try to break them.

Good claims look like: `stop` always leaves the working tree on the base
branch. Every public type in `ir.rs` has a `cache_line` field. Something
where I can write an adversarial test that asks whether the promise is
still holding and get back a yes or a no. "The CLI should be reliable"
fails that bar. It's a mood dressed up as a promise.

The falsification loop is the load-bearing part. If you write claims down
but nothing is periodically trying to break them, you don't have claims.
You have sincerely-held beliefs, which is the category the original specs
were in. A claim without that loop around it will drift the same way a
spec drifts, for the same reason: nothing is keeping it honest.

You might notice that the falsification suite is itself a kind of spec,
a specification of the claims that must hold. That's true, and worth
sitting with. The important difference is that it runs. A drifted test
script fails loudly, which forces either a fix or a conscious decision
to update the claim. A drifted human-facing spec is silent, and silence
is the enemy here. The reason to prefer executable claims over written
ones isn't that one is a spec and the other isn't. It's that one breaks
loudly and the other lies quietly.

I find I don't really know what I value until I try to write a test that
would prove I've stopped valuing it.

**Themes.** What I'm trying to accomplish this week. Priorities come from
the stakeholders. A theme is narrower: it says where, inside those
priorities, I'm going to spend today. *Get the CLI working end-to-end.*
*Stop bleeding contributors on the onboarding path.* A theme biases
attention. It answers the question: where, within everything that
matters, should I be looking this afternoon?

Between those three, there's usually enough context for the agent to
figure out what to do next, and enough for it to notice when it was
wrong about what to do next.

## Judgment is the bet

The word I want is *judgment*. The ability to read a situation and pick a
reasonable next move. Specs were invented to avoid needing it: the whole
point of a spec was to move judgment out of the reader's hands and into
the writer's, because the reader couldn't be trusted with it.

That bet has already been settled at the implementation level. When
someone types "build me a SaaS landing page with Stripe checkout" into
Bolt, they aren't writing a spec. They're trusting the system to derive
the implementation from the goal. And it works, millions of times a day,
across every zero-shot agentic tool on the market. Nobody debates
whether agents can exercise implementation judgment anymore. They just
do it.

The interesting question is what happens when you extend that trust from
a throwaway prototype to a project that matters. A project with users
who depend on specific behaviors. A project where "technically correct
and quietly wrong" has real costs. The agent still has the judgment. What
it lacks is the frame: who does this serve, what have we promised them,
and what are we trying to accomplish this week?

That's the gap this manifesto is about. Not whether agents can figure
out *how* to build something, they obviously can, but whether anyone is
telling them *why* and *for whom*.

The cheapest way to check is to take the spec away from one of your
agents, hand it the stakeholder prose, the claims, and a theme, and
watch what happens for a week. That's how I figured it out. A week of
honest trial will tell you whether the claim holds on your project.

If it does, the writer's job stops being "decompose the goal into steps"
and starts being "make the goal legible enough that the agent can
decompose it on its own."

## This is a daily practice

Value-driven development is a daily practice. The unit of work is the
question "what meaningful improvement can I make right now?" You show up,
you make today's version a little better, you commit, you go home.

This is local gradient by design. The agent walks one project forward,
one step at a time, under direction from a human who is steering. The
method is for patient, aligned collaborators pushing an existing project
forward. A blank-page architect needs a different tool, and that tool is
not this one.

## What the loop looks like

In practice, value-driven development is more rhythm than document.

You start by reading the project hard enough to figure out who it actually
serves and what you've promised them. You write that down as prose, not
as a checklist. You work in small cycles, and each cycle the agent picks
the one change that most improves some specific stakeholder's life, then
writes down who benefited and how. Periodically it stops building and
runs the adversarial pass: does every claim still hold? Did the last few
cycles quietly break something? A claim that can't be broken on purpose
is either load-bearing or decorative, and you want to know which before
you ship.

Every few cycles you look back over the recent work and ask which
stakeholder has been getting all the attention, and which one has been
quietly neglected. The owner reads those retros and decides whether the
tool is earning its keep. That's the feedback loop, and it lives outside
the system, held by the human whose project it is. Nothing in this method
tries to self-grade. The grading is the owner's job and stays that way.

The agent's input is the frame, the current state, and the question:
*which stakeholder's day can I make noticeably better right now?*

That's the whole idea.

## A concrete implementation

The pattern behind this manifesto is already in wide use. Every zero-shot
agentic tool, Bolt, Lovable, Cursor, operates on the same principle:
the user provides direction at the goal level, the system derives the
implementation. What those tools don't do, because they're aimed at
greenfield work, is carry the values forward across hundreds of cycles
on a project that matters.

I've been building a tool called [lathe](https://github.com/libliflin/lathe)
that tries to close that gap. It reads a project and writes an `agent.md`
capturing the stakeholders and claims it finds there, then runs the cycle
on its own, with an adversarial pass against its own claims every few
iterations. The goal isn't to replace the zero-shot tools. It's to bring
the same principle, values-level direction with agent-derived
implementation, to long-lived projects where someone has to care about
the promises made to real users.

It's early, and it's wrong in ways I haven't found yet, and that's part
of why the manifesto came first. I wanted the idea to be legible on its
own, before having to defend any particular implementation of it.

If you want to see the idea with code attached, that's what lathe is for.
If you want to argue with the idea itself, the
[issues on this repo](https://github.com/libliflin/values/issues) are
where to do it. Open one. Tell me where the manifesto is wrong, which
objection I failed to preempt, or which part bounced you off. I'd rather
find out in writing than six months from now in production.
