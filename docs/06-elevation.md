# 6. Elevation Is Its Own Permission

**Status: design, not built.**

## The rule

When one function calls another, the called function normally runs with the caller's permissions. It only runs with its own, higher permissions if that is allowed. Being able to raise permissions is itself a permission.

## Why

Some jobs need more power than the agent asking for them. A backup tool may need to read every file. You don't want to give the agent permission to read every file. You want the agent to be able to *ask for a backup*, and only the backup tool reads everything.

Unix handles this with `setuid` and `sudo`. A program can be marked to run as its owner instead of as the person who started it. That's powerful and risky, so it's tightly controlled.

## How it works

A tool file can be marked "runs as owner." But that mark only works if the *caller* is allowed to use elevation for that tool.

Example:

```
/tools/system/backup     owner: system   runs as owner: yes
                         elevation allowed for: group backup-users
```

- `mikey/coder` is in `backup-users`. It calls `backup`. The backup runs as `system` and can read everything. The coder still can't read everything itself.
- `mikey/researcher` is not in `backup-users`. It calls `backup`. The backup runs as the researcher, sees only what the researcher can see, and backs up much less, or fails.

## What this gives you

- Powerful tools can be shared without handing out power.
- Every elevation is a decision someone made on purpose, and it's logged.

## Open questions

- **Who can change permissions?** This is the next big open piece. If an agent can change its own permissions, none of this means anything. If only humans can, how does a busy human keep up? A first answer is on [Changing permissions](11-changing-permissions.md).
- Can elevation chain? If an elevated tool calls another elevated tool, whose rules apply?
