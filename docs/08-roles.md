# 8. Roles Are Set When the Agent Is Built

**Status: design, not built.**

## The rule

An agent-building tool defines an agent's role groups at the time the agent is built. Permissions follow from the role.

## Why

Setting permissions one by one is slow and easy to get wrong. Companies don't do that for people. They have roles: a manager can approve spending, a worker can submit it. You get the right permissions by getting the right role.

Agents should work the same way. And the role should be decided when the agent is made, on purpose, not added later when something breaks.

## How it works

The person building an agent uses a builder tool. The builder asks what the agent is for and what roles it has, then creates the agent's user, its groups, and their permissions all at once.

Example: a small team builds an agent to handle purchase orders.

```
agent:   team/purchasing
roles:
  requester    can draft a purchase order
  approver     can approve orders under $1,000
  manager      can approve any order, can change approver limits
```

People are added to roles. A worker is a `requester`. The team lead is an `approver`. The department head is `manager`. The agent's tools check these roles on every call.

The builder writes all of this down, so anyone can look up what the agent can do and who can make it do what.

## What this gives you

- Agents that match how organizations already work.
- Permissions that are planned, not bolted on.
- A written record of every agent's design.

## Open questions

- How does a role change after the agent is built, and who approves that?
- Should there be a standard library of common roles?
