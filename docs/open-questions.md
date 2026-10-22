# Open Questions

**Status: design, not built.** Every open question from the design pages, in one place. If you want to help, pick one. Open an issue with your answer, or a link to someone who already solved it.

## The big ones

1. **Who is allowed to change permissions?** If an agent can change its own, nothing else holds. If only humans can, how does a busy human keep up? ([Elevation](06-elevation.md))
2. **Who sets the system-wide defaults?** The machine, the owner, or the law? One position: government sets the baseline for what any agent may do by default. ([Defaults](07-defaults.md))
3. **How does an agent earn more access?** The proposal: by track record over time. Not a one-time test, which an AI can pass for you. Not by who the user is, which gets it wrong too often.

## Agents as users

4. Should an agent ever own another agent, or only humans? ([01](01-agents-are-users.md))
5. What happens to an agent's files when its owner leaves? ([01](01-agents-are-users.md))

## Tools as files

6. Who may install new tools into shared folders? ([02](02-tools-are-files.md))
7. Should a tool file carry a description of what it does, signed by its author? ([02](02-tools-are-files.md))

## Checking

8. How much does checking every call slow things down, and where is skipping it worth it? ([03](03-checked-tool-calls.md))
9. Should the checker be able to ask a human before allowing a risky call? ([03](03-checked-tool-calls.md))

## Locks

10. How long can an agent hold a lock before it's taken away? ([04](04-locks.md))
11. Should a lock cover one file, a folder, or a whole project? ([04](04-locks.md))

## Forms

12. Who writes the forms, and how do new ones get added? ([05](05-forms-only.md))
13. What happens when a task needs a step no form covers? ([05](05-forms-only.md))

## Elevation

14. Can elevation chain? If an elevated tool calls another elevated tool, whose rules apply? ([06](06-elevation.md))

## Defaults

15. What exactly belongs in the default set? ([07](07-defaults.md))
16. Should some powers need a second person to approve before an owner can turn them on? ([07](07-defaults.md))

## Roles

17. How does a role change after the agent is built, and who approves it? ([08](08-roles.md))
18. Should there be a standard library of common roles? ([08](08-roles.md))

## Layered tools

19. How deep should the tool tree go before picking a tool takes too many steps? ([09](09-layered-tools.md))
20. How does the main agent know which branch to open without seeing inside it? ([09](09-layered-tools.md))

## Fast chat

21. Can the chat user hand a task to a checked agent, and does that hand-off need a check? ([10](10-fast-chat.md))
22. Should the chat user be able to read anything, or nothing at all? ([10](10-fast-chat.md))
