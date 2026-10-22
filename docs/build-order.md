# Build Order

**Status: design, not built.** A suggested order for building this, so something small works early and each step adds to it. This is a suggestion, not a plan anyone has committed to.

The idea: start with the parts every other part depends on. Each step should be usable on its own.

## Step 1: Agents as Linux users

Run each agent as a real Linux user. Use plain `useradd`, groups, and file permissions.

This alone gets you a lot. An agent running as `coder` can't touch files only `researcher` can write. Linux already enforces it.

**Done when:** two agents run side by side, and one can't read the other's private folder.

## Step 2: The checker

Build one small program that every tool call goes through. It takes a request (who, which tool, which arguments), checks permissions, runs the tool, and logs the result.

Keep it small. It's the one part everything trusts, so it needs to be easy to read and test.

**Done when:** an agent can't run any tool except through the checker, and every call shows up in the log.

## Step 3: Tools as files

Put tools in a folder tree with owners and permissions. The checker reads those permissions before running anything.

**Done when:** adding an agent to a group gives it a tool, and removing it takes the tool away, with no code change.

## Step 4: Defaults

Decide the starting permissions for a new agent and make the agent-creation script apply them.

**Done when:** a brand-new agent can only read and write its own folder.

## Step 5: Forms

Turn each tool's arguments into a form with checked fields. The agent fills in fields. The checker validates each one.

Start with three forms: read file, edit file, run tests. That's enough for a coding agent.

**Done when:** the agent has no way to send a free-form command.

## Step 6: Locks

Add write locks and version numbers to the edit form.

**Done when:** two agents editing the same file can't erase each other's changes.

## Step 7: Calling other agents

Add an "ask agent" tool. It runs the second agent as itself and logs the hand-off.

**Done when:** the coder can ask the researcher a question, and the researcher still can't edit code.

## Step 8: Fast chat

Make a chat user with no tool permissions that bypasses the checker.

**Done when:** chat is fast and can't call anything.

## Step 9: Layered tools

Show agents only the top of the tool tree. Pick tools in a side context window.

**Done when:** a system with many tools doesn't fill the agent's context window.

## Step 10: Elevation and roles

These depend on everything above, and on the open question of who can change permissions. Build them last.

- Elevation: let specific tools run with their owner's power, for specific groups.
- Roles: an agent-builder that creates users, groups, and permissions from a role description.

**Done when:** a company could build a purchasing agent where only managers can approve large orders.

## Where to start

Steps 1 and 2 are a weekend of work for someone who knows Linux, and they already make an agent safer than most in use today.
