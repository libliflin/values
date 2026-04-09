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

What I've started to notice is that when the reader is an agent pushing
an existing project forward, the documents I've been writing don't
translate. I hand over a clean ticket and a link to three CLAUDE.md files
and an architecture sketch, and the work comes back technically correct
and quietly wrong. The way a new hire's first PR can be correct and
quietly wrong: they followed the instructions, and nobody told them what
the instructions were *for*.

After a while I started to suspect the problem lived in document shape,
not document quality.

## What this is for

A narrow thing: pushing an existing, scoped project forward with an agent
doing the work.

Big questions like microservices versus monolith, which market to target,
or whether to build this thing at all, all belong to the owner. They get
decided in other rooms. My question is smaller: what do you hand an agent
each cycle so it can push the project in a direction the owner would
recognize as progress, without drowning it in documentation?

The short answer is that you need much less than you'd think, and it
needs to be in a different shape than you'd expect.

## What a spec actually is

A spec is a frozen answer to a question that is still being asked. You
write it before the work starts, which is the moment you know the least
about the work. Then the work teaches you something, as it always does,
and now you have two problems: the thing you learned, and the spec that
disagrees with it.

You can update the spec. Most of us don't. The spec drifts, the code
moves, and the document that was supposed to align everyone becomes the
document nobody trusts.

A human reader catches that drift. They push back on stale parts, they
ask clarifying questions, they mentally skip the sentences that don't
make sense anymore. An agent reads every sentence as authoritative text
and runs with it. To an agent, a clear spec looks trustworthy regardless
of whether it still corresponds to reality. Clarity beats correctness
when the reader has no other frame.

And scattering five clean specs across a repo doesn't solve the problem.
It makes it worse. Now you have five drifted documents to satisfy at
once, and the agent will dutifully try to satisfy all of them. The
documentation overload people complain about when working with agents
isn't a volume problem. It's a shape problem.

So a spec, by itself, doesn't carry the thing I actually need the agent
to carry: *why any of this matters, and to whom*.

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

**Claims.** The promises each stakeholder is relying on, written concretely
enough that something can actively try to break them. A claim isn't a
claim if nothing is attacking it. A promise nobody is attacking is a wish.

Good claims look like: `stop` always leaves the working tree on the base
branch. Every public type in `ir.rs` has a `cache_line` field. Something
where I can write an adversarial test that asks whether the promise is
still holding and get back a yes or a no. "The CLI should be reliable"
fails that bar. It's a mood dressed up as a promise.

The adversarial part is load-bearing and non-negotiable. If you write
claims down but nothing in your loop is periodically trying to falsify
them, you don't have claims. You have sincerely-held beliefs, which is
the category the original specs were in. The whole point of a claim is
to be the kind of statement that something else is actively trying to
break, on a schedule, as part of normal work. Otherwise the claim drifts
the same way the spec did and for the same reason: nothing is keeping it
honest.

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

## Judgment is the thing

The word I want is *judgment*. The ability to read a situation and pick a
reasonable next move. Specs were invented to avoid needing it: the whole
point of a spec was to move judgment out of the reader's hands and into
the writer's, because the reader couldn't be trusted with it.

The reader can be trusted with it now. Which means the tradeoff is
upside-down. The writer's job now is to provide the frame the reader
needs in order to decide well.

## This is a daily practice

Value-driven development is a daily practice. The unit of work is the
question "what meaningful improvement can I make right now?" You show up,
you make today's version a little better, you commit, you go home.

This is local gradient by design. The agent walks one project forward,
one step at a time, under direction from a human who is steering. This
frame is for patient, aligned collaborators pushing an existing project
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
tool is earning its keep. That's the feedback loop. It lives outside the
system, held by the human whose project it is.

The agent's input is the frame, the current state, and the question:
*which stakeholder's day can I make noticeably better right now?*

That's the whole idea.

## A concrete implementation

I've been building a tool called [lathe](https://github.com/libliflin/lathe)
that tries to put this into practice. It reads a project and writes an
`agent.md` capturing the stakeholders and claims it finds there, then
runs the cycle on its own, with an adversarial pass against its own
claims every few iterations. It's early, and it's wrong in ways I haven't
found yet, and that's part of why the manifesto came first. I wanted the
idea to be legible on its own, before having to defend any particular
implementation of it.

If you want to see the idea with code attached, that's what lathe is for.
This page is the better place to argue with the idea itself.
