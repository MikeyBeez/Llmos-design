# Sandbox vs. Operating System

**Status: design, not built.**

## The short version

A sandbox is a wall around an agent. It answers one question: what can't the agent reach?

An operating system answers more: who owns the agent, who can change its rights, how agents share things, and what happened afterward.

Sandboxes are useful. They aren't enough. This page goes piece by piece through what a typical sandbox covers and what it leaves out.

## What a typical agent sandbox gives you

- A walled-off space, often a container or virtual machine.
- Rules about which files, network addresses, and programs can be reached from inside.
- Sometimes a policy file that says what's allowed.

NVIDIA OpenShell and similar tools work this way. They are good harnesses. They're the closest thing out there to this design. But they're built around the wall, not around ownership.

## Piece by piece

**Agents are users.**
Sandbox: the agent is "whatever runs inside the box." There's usually no idea of an owner, and no way for a human's role to limit what they can make the agent do.
OS: every agent is a user under a human owner, and humans need group membership to use specific capabilities.

**Tools are files.**
Sandbox: tools are whatever is installed in the box.
OS: every tool has an owner and permissions, checked per agent.

**Checked calls.**
Sandbox: checks happen at the wall, on things like network and file access.
OS: every tool call is checked, with who's asking and on whose behalf.

**Locks.**
Sandbox: usually nothing. Each box is alone, so sharing isn't its problem. Once two agents share a project, it is.
OS: one writer at a time, with version checks.

**Forms.**
Sandbox: the agent can run any command inside the box. The wall limits the damage.
OS: the agent can only fill out the form for the current step.

**Elevation.**
Sandbox: often a box is either trusted or not.
OS: using a more powerful tool is its own permission, granted per tool and per group.

**Defaults.**
Sandbox: depends on how the box was set up.
OS: every new agent starts with almost nothing, by design.

**Roles.**
Sandbox: not part of the model.
OS: roles are set when the agent is built and decide who can make the agent do what.

**Layered tools and fast chat.**
Sandbox: not addressed.
OS: tools load in a tree to keep context small, and chat runs as a user with no tools.

## Both together

These aren't rivals. An OS like this could run inside a sandbox, and should. The wall limits the worst damage. The OS decides who's allowed to do what inside the wall.

The missing piece is ownership. A wall can't tell you whose agent it is, or who is allowed to change what it can do.
