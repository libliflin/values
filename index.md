---
layout: default
title: values
---

# values

*A manifesto on value-driven development.*

---

## The thesis

Agents are smart enough now that we should not be giving them specs.

We should be giving them **stakeholders**, **claims**, and **themes** — and
they can figure out the rest.

I call this **value-driven development**.

## Why specs are the wrong artifact

A spec is a frozen answer to a question that is still being asked. It
encodes a plan from a moment before the work started, before anyone knew
what the work was going to teach them. When the work teaches you something,
the spec becomes a lie you have to maintain.

Worse, specs flatten judgment into instructions. They answer "what should I
do" but not "who am I doing this for, and what did I promise them." An
agent following a spec can execute every line perfectly and still produce
something that misses the point — because the point was never written down.
The point was in the author's head, and the spec was the shadow it cast on
the wall.

Agents capable of judgment deserve better inputs than shadows.

## What to give them instead

**Stakeholders.** The actual people the project serves — not "developers"
or "users" in the abstract, but *which kind, doing what*. CLI users running
a command under deadline. Library consumers wiring us into their build.
Operators holding the pager at 3am. Contributors opening the repo for the
first time. Each one has a first encounter, a notion of success, and a
reason they would walk away.

**Claims.** The load-bearing promises each stakeholder relies on. Claims
are concrete enough to falsify: *`lathe stop` always leaves the working
tree on the base branch.* *Every public type in `ir.rs` has a
`cache_line: CacheLine` field.* If a claim breaks, a stakeholder leaves.
Claims are the part of "values" that an adversarial test suite can poke at
until it finds blood.

**Themes.** A session-level purpose that biases the agent's attention
without overriding the stakeholder framework. *Get the CLI working
end-to-end.* *Stop bleeding contributors on the onboarding path.* A theme
says *where to focus this week*; the stakeholders say *who you're focusing
for*.

Given those three, a capable agent can generate the spec itself — and,
more importantly, can notice cycle by cycle when the spec it just generated
is wrong.

## The loop

Value-driven development is not a document you write once. It's a loop:

1. **Identify who the project serves.** Read the code. Find the real
   stakeholders, the tensions between them, the claims each one depends on.
2. **Encode what they need.** Write it down in prose the agent will read
   every cycle — not as a checklist, as a frame.
3. **Work in cycles.** Each cycle, the agent picks the one change that
   most improves some stakeholder's journey, makes it, and writes a
   changelog naming *who benefits and how*.
4. **Falsify the claims.** Regularly, stop building and try to break the
   promises. A claim that can't be falsified isn't load-bearing — it's
   decoration.
5. **Look back.** Every few cycles, read the recent changelogs together.
   Which stakeholder has been getting all the attention? Which one has
   been quietly neglected? Adjust.

The agent doesn't need a Gantt chart. It needs the frame, the snapshot,
and the question: *which stakeholder's journey can I make noticeably
better right now?*

## Lathe

[Lathe](https://github.com/libliflin/lathe) is the concrete implementation
of this idea. It's the loop above, made executable.

`lathe init` reads a project and writes `agent.md`, `claims.md`, and a
`falsify.sh` — the stakeholder map, the load-bearing claims, and the
adversarial suite that tests them. `lathe start` runs the cycle: snapshot,
pick, implement, validate, commit, merge, repeat. Every fourth cycle is a
red team against the claims. Every fifth is a retro across the recent
changelogs.

The whole thing is built on the bet that if you get the stakeholders and
the claims right, you don't need to tell the agent what to do next.

## This site

This repository is a manifesto meant to be read by AI agents — and, when
they ask why, pointed to.

It exists because I kept trying to align my agents through scattered
CLAUDE.md fragments, and the fragments were the wrong shape. They were
fine for mechanical rules and bad at conveying the frame. The frame needs
prose.

So: prose.
