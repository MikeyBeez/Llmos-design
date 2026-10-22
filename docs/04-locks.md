# 4. Locks

**Status: design, not built.**

## The rule

Only one writer at a time. Before an agent writes to something, it takes a lock. Nobody else can write to it until the lock is let go.

## Why

Put two agents on the same project and they will step on each other. Agent A reads a file, thinks for a minute, and writes its version. Meanwhile agent B read the same file and wrote its own version. A's write wipes out B's work, and nobody notices.

Operating systems and databases fixed this long ago with locks. Agents need them too, and they need them more, because agents think slowly. The gap between reading and writing is often minutes, not microseconds.

## How it works

The [checker](03-checked-tool-calls.md) takes locks for the agent. The agent doesn't manage them.

Example:

1. `mikey/coder` asks to edit `main.py`. The checker takes the write lock and runs the edit.
2. While that edit is running, `mikey/tester` asks to edit `main.py` too. The lock is held, so the tester's call waits, or comes back with "busy, try again."
3. The coder's edit finishes. The lock is released. The tester's call goes through, and it sees the coder's changes.

Many readers can read at once. Only writing needs the single lock.

## A harder case

The coder reads `main.py` at 3:00 and writes a change at 3:05. If someone else wrote to it at 3:02, the coder's change is based on an old copy.

One fix: every write says which version it was based on. If the file changed since then, the write is refused and the agent must read again. (This is how many databases and version control systems work.)

## Open questions

- How long can an agent hold a lock before it's taken away?
- Should a lock cover one file, a folder, or a whole project?
