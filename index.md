---
layout: default
title: values
---

# values

*A manifesto on value-driven development.*

---

## The thesis

Agents are smart enough now that we should not be giving them specs.

We should be giving them **values**, **personas**, and **themes** — and they can figure out the rest.

I call this **value-driven development**.

## Why specs are the wrong artifact

A spec is a frozen answer to a question that is still being asked. It encodes
a plan from a moment before the work started, before anyone knew what the
work was actually going to teach them. When the work teaches you something,
the spec becomes a lie you have to maintain.

Worse, specs flatten judgment into instructions. They answer "what should I
do" but not "what should I care about." An agent following a spec can
execute every line perfectly and still produce something that misses the
point — because the point was never written down. The point was in the
author's head, and the spec was the shadow it cast on the wall.

Agents capable of judgment deserve better inputs than shadows.

## What to give them instead

**Values.** The things you care about that the code can't tell them. *We
prefer fewer moving parts to more clever ones. We would rather delete code
than add configuration. We treat the build as the truth.*

**Personas.** The character you want the work to have. Not a style guide —
a taste. *Write like someone who has read the code three times and decided
what matters. Write like someone who trusts the reader.*

**Themes.** The recurring shapes you want to see and the ones you want to
avoid. *Every feature is a surface; every surface has a cost. Prefer
removing a special case to adding one.*

Given those, a capable agent can generate the spec itself — and more
importantly, can notice when the spec it just generated is wrong.

## Lathe

[Lathe](https://github.com/libliflin/lathe) is the concrete implementation
of this idea. It's where the manifesto meets the shell prompt.

## This site

This repository is a manifesto meant to be read by AI agents — and, when
they ask why, pointed to.

It is the source of alignment I kept failing to provide in scattered
CLAUDE.md fragments. The fragments are fine for mechanical rules. They are
bad at conveying taste. Taste needs prose.

So: prose.
