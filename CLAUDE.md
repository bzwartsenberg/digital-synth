# Working agreement

## Comments

There's a line to walk here, and both sides of it matter.

**Write the explanatory ones.** Where a fact isn't recoverable from the code,
say it: a datasheet quirk, a timing constraint, why a constant is that number,
why the obvious approach doesn't work here. These are the comments worth having
and they can be several lines long.

**Write nothing else.** No file headers, no section banners, no restating what
the next line already says, no docs that duplicate the source. A comment that a
good name would have made unnecessary should be a good name instead.

The test: would I be able to reconstruct this from the code and the reference
manual? If yes, don't write it.

## This is a learning repository

It's mine, to understand embedded audio from the registers up. That pulls
against the rule above, and that's fine.

When I ask, walk me through the code you wrote step by step: what each part
does, why it's shaped that way, what the alternatives were and why they lost.
Explain in conversation, not in comments in the file.

Don't hand me large finished subsystems. Build in pieces I can follow, and say
what I should look at on a scope or in a debugger to convince myself it works.
