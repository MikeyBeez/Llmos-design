# 10. Chat That Can't Act Can Run Fast

**Status: design, not built.**

## The rule

A plain chat tool that calls no other tools can skip the checking apparatus. It's safe because it runs as a different user with no tool permissions at all.

## Why

Checking every call has a cost. If someone just wants to talk, or ask a question, running every word through forms and permission checks is slow for no reason.

But you can't just turn the checks off. A chat that could quietly call tools would be a hole in the whole system.

The answer is to make the chat a separate user that has *no* permissions. It can't call tools, so there's nothing to check.

## How it works

```
mikey/chat       user with no tool permissions, no group memberships
mikey/coder      user with code permissions, all calls checked
```

When Mikey just wants to talk, he talks to `mikey/chat`. Responses come back as fast as the model can produce them.

If the chat says "you should edit that file," it can't do it. It has no way to. Mikey, or a checked agent, has to take that action.

## What this gives you

- Fast conversation with zero risk of the chat acting on its own.
- A clear line between talking and doing.

## Open questions

- Can the chat user hand a task to a checked agent, and if so, does that hand-off itself need a check?
- Should the chat user be able to *read* anything, like the owner's notes, or nothing at all?
