# 7. Defaults

**Status: design, not built.**

## The rule

Every agent starts with safe default settings. The owner can change them.

## Why

Most people will never touch a setting. Whatever the default is, that's what most agents will do. So the default decides how safe the system really is.

A plain rule of thumb: if you don't know enough to change a setting, you probably shouldn't be changing it. Defaults protect the people who don't know.

## How it works

A new agent gets a starting set of permissions. Something like:

- Can read and write only in its own work folder.
- Can't send messages, spend money, or reach the network.
- Can't call other agents.
- Can't use elevation.

The owner turns on what the agent needs for its job, one piece at a time.

Example: Mikey builds a research agent. By default it can't reach the web. He gives it the `web` group. It still can't write to his code, send email, or spend money, because he never turned those on.

## Who sets the defaults?

There are layers:

1. **The system.** What any new agent gets on this machine.
2. **The owner.** Changes for their own agents.
3. **Possibly the law.** One open position: government could set the baseline for what any agent may do by default, the way building codes set baselines for wiring.

## What this gives you

- An agent that's never been configured is a safe agent.
- Every extra power is something a person chose to grant.

## Open questions

- What exactly belongs in the default set?
- Should some powers need a second person to approve before an owner can turn them on?
