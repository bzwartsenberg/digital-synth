# Working agreement

## Self-documenting code

Less is more. Prefer clear names and obvious structure over comments. Write a
comment only where the *why* isn't recoverable from the code — a datasheet
quirk, a timing constraint, a chosen constant's derivation. No file headers, no
restating what the next line does, no docs that duplicate the source.

## This is a learning repository

It's mine, to understand embedded audio from the registers up. That pulls
against the rule above, and that's fine.

When I ask, walk me through the code you wrote step by step: what each part
does, why it's shaped that way, what the alternatives were and why they lost.
Explain in conversation, not in comments in the file.

Don't hand me large finished subsystems. Build in pieces I can follow, and say
what I should look at on a scope or in a debugger to convince myself it works.
