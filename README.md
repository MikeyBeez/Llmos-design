# LLMOS: An Operating System With the LLM as the CPU

**Status: design, not built.** This page describes how the system should work. Most of it does not exist yet. It is here so people can read it, argue with it, and build it.

By Mikey Bonsignore ([Medium](https://medium.com/@mbonsign) · [GitHub](https://github.com/MikeyBeez))

## The problem

Today's AI agents run on chains and sandboxes. A chain strings steps together. A sandbox puts a wall around the agent. Neither one answers basic questions an operating system has answered for fifty years:

- Who owns this agent?
- What is it allowed to touch?
- Who can change what it's allowed to touch?
- What happens when two agents try to write the same file?

Telling a model "don't do that" in a prompt is not an answer. Models miss instructions, or ignore them. The rules have to live outside the model, in something that checks every action before it runs.

## The idea

Treat the LLM like a CPU. It does the thinking. An operating system around it decides what actually happens.

## The pieces

Each piece has its own page in [docs/](docs/) with examples and open questions. The examples there are one way each piece could work. They are meant to be argued with.

**1. Agents are users.** ([details](docs/01-agents-are-users.md))
Every agent is a user on the system, with a user ID and groups, the same as a person on a Unix machine. Each agent lives in a namespace under the human who owns it. A human who wants to use a specific capability of an agent has to be in that agent's group for it.

**2. Tools are files.** ([details](docs/02-tools-are-files.md))
Every tool and every protocol is a file with an owner and permissions. An agent can run a tool only if the permissions allow it. An agent does not get web search, or anything else, just because it exists. Sub-agents must be called on purpose.

**3. Every tool call is checked.** ([details](docs/03-checked-tool-calls.md))
A tool call works like a Unix system call. Something outside the model checks permissions and takes any needed locks before the tool runs. A command never just runs. It runs inside the checking apparatus.

**4. Locks.** ([details](docs/04-locks.md))
Only one writer at a time. Two agents can't silently clobber the same file.

**5. Everything is done through forms.** ([details](docs/05-forms-only.md))
The agent doesn't free-write commands. If the next step needs a form filled out, filling out that form is the only thing the agent can do. The model sits outside the trust boundary. It never touches the actuators directly.

**6. Elevation is its own permission.** ([details](docs/06-elevation.md))
When one function calls another, the called function runs with its own higher permissions only if that is allowed. Being able to raise permissions is itself a permission.

**7. Defaults.** ([details](docs/07-defaults.md))
Every agent starts with safe default settings. The owner can change them. If you don't know enough to change a setting, you probably shouldn't.

**8. Roles are set when the agent is built.** ([details](docs/08-roles.md))
An agent-building tool defines the agent's role groups, like manager and worker roles in a company department. Permissions follow from the role.

**9. Tools load in layers.** ([details](docs/09-layered-tools.md))
Tools are arranged in a tree, so they don't all crowd into the context window. Picking a tool can happen in a separate context window. Only the request and the answer come back to the main one.

**10. Chat that can't act can run fast.** ([details](docs/10-fast-chat.md))
A plain chat tool that calls no other tools can skip the checking apparatus. It's safe because it runs as a different user with no tool permissions at all.

## Start here

- [Walkthrough](docs/walkthrough.md): one task followed through every piece, start to finish.
- [Attacks and what stops them](docs/attacks.md): ten ways agents go wrong, and which piece blocks each.
- [Sandbox vs. OS](docs/sandbox-vs-os.md): what a sandbox covers and what it leaves out.
- [Build order](docs/build-order.md): which piece to build first.
- [Open questions](docs/open-questions.md): every unsolved question in one list. Pick one.
- [Article series](docs/article-series.md): planned Medium articles, one per idea.

## Why not a sandbox?

A sandbox is a wall. It says what's outside the agent's reach. It doesn't say who owns the agent, who can change its rights, or how two agents share a file. Ownership is the piece sandboxes are missing. Tools like NVIDIA OpenShell come close, but they are harnesses, not operating systems. ([More](docs/sandbox-vs-os.md))

## Open questions

- Who is allowed to change permissions?
- Who sets the system-wide defaults? (Possibly government, for what any agent may do by default.)
- How does an agent earn more access? The proposal: by track record over time, not a one-time test and not by who the user is.

[All open questions](docs/open-questions.md)

## What exists today

A coding-agent harness on a single GPU machine, running on Linux. It uses some of these ideas (context isolation for protocols, forced best-guess deadlines, errors treated as missing guardrails). The OS layer described above, meaning agents as users, tools as owned files, permission and lock checks on every call, and forms-only work, is **not built**.

## Read more

- "Agents Should Be Users" on Medium: https://medium.com/@mbonsign

## Want to build it?

Please do. Open an issue to argue with any piece of this, or link your own work.
