---
layout: default
title: values
---

# values

*A manifesto on value-driven development.*

---

## The thesis

I've stopped writing specs for my agents.

Not because the specs were bad. They were usually fine. But the work kept
producing things that were technically correct and quietly wrong — the way
a new hire's first PR can be correct and quietly wrong, because they
followed the instructions and nobody had told them what the instructions
were *for*.

After a while I started to suspect the spec was the wrong artifact.

## What a spec actually is

A spec is a frozen answer to a question that is still being asked. You
write it before the work starts, which is the moment you know the least
about the work. Then the work teaches you something — it always does —
and now you have two problems: the thing you learned, and the spec that
disagrees with it.

You can update the spec. Most of us don't. The spec drifts, the code
moves, and the document that was supposed to align everyone becomes the
document nobody trusts.

An agent working from a drifted spec will follow it anyway. That is the
part I keep getting wrong. The agent is not going to notice that the spec
is a lie; the agent is going to notice that the spec is clear. Clarity
beats correctness when the reader has no other frame.

So the problem isn't spec quality. It's that a spec, by itself, doesn't
carry the thing I actually need the agent to carry: *why any of this
matters, and to whom*.

## What I'd rather give them

Three things, in roughly this order.

**Stakeholders.** Not "users" in the abstract. The specific people the
project serves, named concretely enough that I can picture one of them
having a bad morning. The operator who gets paged at 3am and needs the
error message to tell her something useful. The contributor opening the
repo for the first time on a Sunday afternoon, deciding in ninety seconds
whether this project is worth her weekend. The downstream team that wired
us into their build last quarter and now depends on a behavior we never
wrote down.

Each stakeholder has a first encounter, a notion of success, and a reason
they would walk away. If I can't name those, I don't understand the
stakeholder yet, and I certainly can't ask an agent to work on their
behalf.

**Claims.** The promises each stakeholder is relying on, written concretely
enough that I could falsify them. Not "the CLI should be reliable" — but
`stop` always leaves the working tree on the base branch. Not "the code
should be maintainable" — but every public type in `ir.rs` has a
`cache_line` field. A claim you can't falsify isn't a promise; it's a
mood. The real ones are load-bearing: if they break, a stakeholder leaves.

Claims are the part of "values" that an adversarial test can poke at. I
find I don't really know what I value until I try to write a test that
would prove I've stopped valuing it.

**Themes.** The thing I'm trying to accomplish this week. Not a
priority — priorities come from the stakeholders — but a direction.
*Get the CLI working end-to-end.* *Stop bleeding contributors on the
onboarding path.* A theme biases attention. It answers "where, within
everything that matters, should we be spending today?"

Stakeholders say who. Claims say what was promised. Themes say where to
look next. Between the three of them there is usually enough context for
a capable reader to generate the right spec — and, more usefully, to
notice when the spec they just generated is wrong.

## Judgment is the thing

The reason this works now and didn't work five years ago is that the
reader is different. You could not hand this kind of frame to a 2020
autocomplete and expect a coherent PR. You can hand it to a 2026 agent
and get one.

That's not a claim about intelligence. It's a claim about *judgment*:
the ability to read a situation, weigh competing concerns, and pick a
reasonable next move. Judgment is what specs were invented to avoid
needing — the whole point of a spec was to remove judgment from the
reader and put it in the writer. That tradeoff made sense when the
reader couldn't be trusted with it.

The reader can be trusted with it now. Which means the tradeoff is
upside-down. The writer's job isn't to pre-decide — the writer's job is
to provide the frame the reader needs in order to decide well.

## What the loop looks like

In practice, value-driven development is not a document. It's a rhythm.

You start by reading the project hard enough to figure out who it
actually serves and what you've promised them. You write that down. You
work in small cycles, and each cycle the agent picks the one change that
most improves some specific stakeholder's life, and writes down who
benefited and how. Periodically you stop building and try to break the
promises on purpose — an adversarial pass, looking for the claim that
was secretly decorative. Periodically you look back over the last few
cycles and ask which stakeholder has been getting all the attention and
which one you've been quietly neglecting.

The agent doesn't need a roadmap. It needs the frame, the current state,
and the question: *which stakeholder's day can I make noticeably better
right now?*

That's the whole idea.

## A concrete implementation

I've been building a tool called [lathe](https://github.com/libliflin/lathe)
that tries to operationalize this. It reads a project, writes down the
stakeholders and claims, runs the cycle, and runs an adversarial pass
against its own claims every few cycles. It's early, and it's wrong in
ways I haven't found yet, and that's why the manifesto came first — I
wanted the idea to be legible on its own, without having to defend a
particular implementation of it.

If you want to see the idea with code attached, lathe is where to look.
If you want to argue with the idea itself, this page is the better place.
