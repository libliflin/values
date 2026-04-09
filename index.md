---
layout: default
title: values
---

# values

*A manifesto on value-driven development.*

---

## The thesis

I've stopped writing specs for my agents.

The specs were usually fine, honestly. The problem was that the work kept
producing things that were technically correct and quietly wrong. The way
a new hire's first PR can be correct and quietly wrong: they followed the
instructions, and nobody told them what the instructions were *for*.

After a while I started to suspect the spec was the wrong artifact.

## What a spec actually is

A spec is a frozen answer to a question that is still being asked. You
write it before the work starts, which is the moment you know the least
about the work. Then the work teaches you something, as it always does,
and now you have two problems: the thing you learned, and the spec that
disagrees with it.

You can update the spec. Most of us don't. The spec drifts, the code
moves, and the document that was supposed to align everyone becomes the
document nobody trusts.

An agent working from a drifted spec will follow it anyway. That is the
part I keep getting wrong. To an agent, a clear spec looks trustworthy
regardless of whether it still corresponds to reality. Clarity beats
correctness when the reader has no other frame.

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
enough that I could falsify them. `stop` always leaves the working tree on
the base branch. Every public type in `ir.rs` has a `cache_line` field.
Something where I can write an adversarial test that asks whether the
promise is still holding and get back a yes or a no. "The CLI should be
reliable" fails that bar. It's a mood dressed up as a promise. Real claims
are load-bearing. Break one, and a stakeholder walks.

Claims are the part of "values" that an adversarial test can poke at. I
find I don't really know what I value until I try to write a test that
would prove I've stopped valuing it.

**Themes.** What I'm trying to accomplish this week. Priorities come from
the stakeholders. A theme is narrower: it says where, inside those
priorities, I'm going to spend today. *Get the CLI working end-to-end.*
*Stop bleeding contributors on the onboarding path.* A theme biases
attention. It answers the question: where, within everything that
matters, should I be looking this afternoon?

Between those three, there's usually enough context for the agent to
generate the right spec, and more importantly, to notice when the spec it
just generated has gone wrong.

## Judgment is the thing

The word I want is *judgment*. The ability to read a situation and pick a
reasonable next move. Specs were invented to avoid needing it: the whole
point of a spec was to move judgment out of the reader's hands and into
the writer's, because the reader couldn't be trusted with it.

The reader can be trusted with it now. Which means the tradeoff is
upside-down. The writer's job now is to provide the frame the reader
needs in order to decide well.

## What the loop looks like

In practice, value-driven development is more rhythm than document.

You start by reading the project hard enough to figure out who it actually
serves and what you've promised them. You write that down. You work in
small cycles, and each cycle the agent picks the one change that most
improves some specific stakeholder's life, then writes down who benefited
and how. Periodically you stop building and try to break the promises on
purpose, running an adversarial pass to find the claim that was secretly
decorative. Every few cycles you also look back over the recent work and
ask which stakeholder has been getting all the attention, and which one
you've been quietly neglecting.

The agent's input is the frame, the current state, and the question:
*which stakeholder's day can I make noticeably better right now?*

That's the whole idea.

## A concrete implementation

I've been building a tool called [lathe](https://github.com/libliflin/lathe)
that tries to put this into practice. It reads a project and writes down
the stakeholders and claims it finds there, then runs the cycle on its
own, with an adversarial pass against its own claims every few iterations.
It's early, and it's wrong in ways I haven't found yet, and that's part
of why the manifesto came first. I wanted the idea to be legible on its
own, before having to defend any particular implementation of it.

If you want to see the idea with code attached, that's what lathe is for.
This page is the better place to argue with the idea itself.
