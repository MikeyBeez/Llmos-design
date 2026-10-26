# 11. Changing Permissions Is a Form

**Status: design, not built.**

## The rule

Nobody changes their own permissions. A permission change is a form. Anyone can fill it out, agent or human. Someone else has to sign it.

## Why

This is the piece everything else leans on.

- If an agent can change its own permissions, none of the other rules mean anything. It just gives itself what it wants.
- If a human has to approve every change, a busy human starts clicking "yes" without reading. A rubber stamp is no safer than no check at all.

So the answer can't be "the agent decides" or "the human decides everything." It has to be a process, with sizes.

## How it works

### 1. The request is a form

An agent that needs more access doesn't take it. It fills out a change form (see [Forms](05-forms-only.md)):

```
who:      mikey/researcher
wants:    read access to ~/Code/llmos/docs
why:      summarize the design pages for an article
how long: 2 hours
```

The form goes to the checker (see [Checked tool calls](03-checked-tool-calls.md)), like any other call.

### 2. Three signing rules

The checker sends the form to someone who can sign it. Three rules hold every time:

1. **You can't sign your own request.**
2. **You can't grant what you don't have.** A signer can only hand out permissions the signer holds.
3. **The signer has to be outside the requester's chain.** An agent can't get its approval from an agent it owns, or one that works for it.

### 3. Changes come in sizes

- **Small.** Read one more folder inside the owner's own files. Use a tool the agent's role already allows, for a short time.
  Signed automatically, if the agent has a good track record. Still logged. The owner sees a short daily list of what was granted.
- **Big.** Elevation, network access, sending messages, spending money, calling other agents.
  The owner signs every time.
- **Biggest.** Anything past the system-wide defaults (see [Defaults](07-defaults.md)).
  The owner plus a second person, so one tired person can't open the door alone.

### 4. Grants run out

Every grant has an end time. When it runs out, the permission goes away by itself. An agent that still needs it has to ask again. Nothing piles up quietly over months.

### 5. No answer means no

If the signer is away, the request just waits. The agent can't proceed until someone signs. Waiting is safe. Guessing "yes" is not.

## Example

`mikey/researcher` asks to read `~/Code/llmos/docs` for two hours.

- It's a small change, inside Mikey's own files.
- The researcher has run for three months with no refused or flagged calls, so it's signed automatically.
- It shows up on Mikey's daily list. In two hours the access ends.

Later the researcher asks to send email.

- That's a big change. It waits for Mikey.
- Mikey reads it, sees no reason for a research agent to send email, and says no. The refusal is logged too.

## How this helps the busy human

- Small changes don't reach him at all, except on a daily list.
- Big changes are rare, so he can afford to read each one.
- Grants expire, so a mistake fixes itself.
- An agent's track record decides what counts as routine for it. This is the same idea as [Earning Access](12-earning-access.md), applied to agents.

## What this gives you

- No agent can raise its own power, ever.
- Every change has a name on it: who asked, who signed, and why.
- People spend their attention on the few changes that matter.

## Open questions

- Who decides which changes are small? The system, the owner, or the law?
- What if an agent asks too often? Should requests be rate-limited, so it can't wear the owner down?
- Can a signer be another agent, say one with a manager role (see [Roles](08-roles.md))? Or must every big change end with a human?
- How much track record is enough for auto-signing, and can one bad call reset it?
