---
layout: post
title: Code that Writes Code
post_date: 13 March, 2012 -- Menlo Park, CA
---

Lately, I’ve heard a lot about [frighteningly
ambitious](http://paulgraham.com/ambitious.html) startup ideas. Well,
here’s one idea: *code that writes code*.

Today, humans write most computer programs. If you think of a program as
a specification (or a proof[^1]), then *we* fill in its internals.
That’s great for developers, but it’s not economically efficient. Human
brains are expensive. To the degree that you can limit human agency,
without sacrificing software quality, you can create enormous value.

Limiting human agency sounds bad — think Skynet — but it has actually
been happening for some time. Consider the existence of two common
abstractions: *highly opinionated web-frameworks* and *high-level
programming languages*. Each of these tools removes a degree of freedom
from the human programmer, yet increases productivity.

It’s all about leverage. You sacrifice some control when you switch from
Assembly to Python, but in exchange you get to work at a higher level of
abstraction, and you can write powerful programs more quickly. Likewise,
when you use Ruby on Rails, you trade expressiveness for the convenience
of a domain specific language and quicker web development. So although
you decrease your freedom when you work at a higher level of
abstraction, that’s usually a good thing.

Now let’s get even *more* abstract. After all, I’m not proposing that
someone develop a new programming language or web framework (although
these are great things do do). Rather, I think that soon it will be
possible to automate some kinds of software development, *at the level
of program specifications*. Perhaps that sounds confusing, so let’s call
this specific idea a Magic Compiler.

Give the Magic Compiler a set of *specifications*, and it will spit out
a complete program. Pretty abstract, right? Although this sounds crazy,
[more](http://epr.adaptive.cs.unm.edu/) than a
[few](http://www.cs.berkeley.edu/~bodik/synthesis.html) people have
already begun
[building](http://www.fxpal.com/publications/fxpal-pr-06-374.pdf) tools
along these lines. Particularly when you start automating at the level
of function-building or bug-fixing[^2], things start to become quite
tractable.

I’ll delve into the practicalities of this idea in a later post. The
Magic Compiler isn’t really magic — it just looks like it.

[^1]: See the [Curry–Howard correspondence](http://en.wikipedia.org/wiki/Curry%E2%80%93Howard_correspondence#Origin.2C_scope.2C_and_consequences).

[^2]: Our group at the [UVA](http://www.cs.virginia.edu/~weimer/) and [UNM](http://www.cs.unm.edu/~forrest/) fixed many bugs automatically.
