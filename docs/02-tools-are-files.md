# 2. Tools Are Files

**Status: design, not built.**

## The rule

Every tool and every protocol is a file. Each file has an owner, a group, and permissions. An agent can run a tool only if the permissions allow it.

## Why

Today an agent gets a list of tools when it starts, and it can call any of them. If web search is in the list, the agent can search. Nobody decided that this agent, for this job, should be able to search. It was just there.

In Unix, a program you can't execute is a program you can't run. That's the whole check, and it's enough.

## How it works

Tools live in a folder tree, like programs in `/usr/bin`.

```
/tools/web/search          owner: system   group: web      perms: r-x for group
/tools/code/edit_file      owner: mikey    group: coders   perms: r-x for group
/tools/mail/send           owner: mikey    group: mail     perms: r-x for owner only
```

`mikey/coder` is in the `coders` group, so it can run `edit_file`. It isn't in `web`, so it can't search. Only Mikey himself can run `mail/send`.

Protocols work the same way. A protocol is a file of instructions. An agent can load it only if it has read permission.

## Sub-agents are called on purpose

An agent doesn't quietly spin up helpers. Calling a sub-agent is a tool call like any other, checked the same way. If `mikey/coder` wants `mikey/researcher` to look something up, it has to have permission to call that agent, and the call shows up in the log.

## What this gives you

- You can see exactly what an agent is able to do by listing the files it can run.
- Adding a tool to an agent is a permission change, not a code change.
- A new tool installed on the system doesn't automatically reach every agent.

## Open questions

- Who may install new tools into shared folders?
- Should a tool file also carry a description of what it does, signed by its author?
