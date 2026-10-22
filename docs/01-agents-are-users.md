# 1. Agents Are Users

**Status: design, not built.**

## The rule

Every agent is a user on the system. It has a user ID and belongs to groups, just like a person on a Unix machine. It is not a process that borrows its owner's identity.

## Why

Today most agents run as you. If your agent deletes a file, the system sees *you* deleting it. There's no way to say "my agent may read my email but not send it," because the system can't tell you and the agent apart.

Unix solved this decades ago for people. A web server runs as its own user (often `www-data`) so that a bug in it can't touch your home folder. Agents need the same thing.

## How it works

Each agent lives in a namespace under the human who owns it.

Example: Mikey owns two agents.

```
mikey                 (human, owner)
mikey/coder           (agent)
mikey/researcher      (agent)
```

`mikey/coder` can write to `~/Code`. `mikey/researcher` can use web search but can't write to `~/Code`. If the researcher is tricked by a web page into trying to edit code, the call fails. Not because the model refused, but because the researcher user has no write permission there.

## Humans join an agent's groups

Using an agent isn't all-or-nothing. A human has to be in the right group to use a specific capability.

Example: a company builds an agent `acme/billing`. It has two groups:

```
billing-view     can ask about invoices
billing-issue    can tell the agent to issue refunds
```

A support worker is in `billing-view`. A manager is in both. When the worker asks the agent for a refund, the refund tool checks the *human's* groups too, and the call is refused.

## What this gives you

- A record of who did what. The log says `mikey/coder`, not just `mikey`.
- Limits that hold even when the model is confused, tricked, or wrong.
- A way to turn one agent off without touching anything else.

## Open questions

- Should an agent ever own another agent, or only humans?
- What happens to an agent's files when its owner leaves?
