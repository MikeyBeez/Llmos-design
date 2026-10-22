# 3. Every Tool Call Is Checked

**Status: design, not built.**

## The rule

The model never runs anything itself. It asks. Something outside the model checks the request, then runs it or refuses.

## Why

You can tell a model "don't hack anyone." It might follow that. It might not see it. It might be talked out of it by a web page. A rule that lives only in the prompt is a hope, not a rule.

In Unix, a program can't open a file directly. It asks the kernel with a system call, and the kernel checks permissions first. The program can be as buggy or hostile as it likes. The kernel still says no.

## How it works

Every tool call passes through a checker before it runs:

1. **Who is asking?** The agent's user ID, and the human behind the request.
2. **Can they run this tool?** Check the tool file's permissions.
3. **Can they touch these things?** Check permissions on every file or resource the call names.
4. **Is anything locked?** Take the locks the call needs (see [Locks](04-locks.md)).
5. **Run it.**
6. **Log it.** Who, what, when, and the result.

Example: `mikey/researcher` asks to run `edit_file` on `~/Code/llmos/main.py`.

- Step 2 fails. The researcher isn't in `coders`.
- The call is refused and logged. The model gets back "permission denied," the same answer a Unix program would get.

The model never had a way around this, because it never had direct access to anything.

## What this gives you

- Safety that doesn't depend on the model behaving.
- A complete log of every action, by every agent.
- One place to add new rules for the whole system.

## Open questions

- How much does checking every call slow things down, and where is it worth skipping? (See [Fast chat](10-fast-chat.md).)
- Should the checker be able to ask a human before allowing a risky call?
