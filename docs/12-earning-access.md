# 12. Earning Access

**Status: design, not built.** This is a policy idea, not a piece of software. It's here because the OS needs an answer to "who gets more power, and how?"

## The rule

Everyone starts on a weaker model and a more limited agent. You move up by earning badges for kinds of work, over time.

## Why

There are three common ways to decide who gets powerful AI. Each one fails.

- **A one-time test.** An AI can take the test for you.
- **Who you are.** Judging by profile gets it wrong too often, and it shuts out people who don't fit the profile.
- **Who you work for.** If only big labs and their partners get access, licensing gets captured by the big labs.

A track record over time is harder to fake, and it doesn't care who your employer is.

There's a second payoff. Matching the model to the task saves compute. Most work doesn't need the biggest model.

## How it works

### Badges, like the Boy Scouts

You earn a badge for a kind of work: say, safe use of code tools, or careful handling of medical records. A badge says you showed steady, good behavior doing that work, over time and in real use, not by answering a few questions once.

### Send the badge, not the work

To move up, you send your badges, not your work. Whoever grants access never sees your files, your chats, or your code. Your privacy stays with you.

### No single judge

Different badges are judged by different people:

- **The computer** judges the simple ones, the kind a checker can verify on its own.
- **Companies** judge the middle ones, in their own fields.
- **The government** judges the highest ones, with an in-person test where you can't use a phone or a computer. Like a driver's license.

No one agency holds all the keys.

## How it connects to the OS

- [Defaults](07-defaults.md) decide where everyone starts.
- Badges decide how far a person can move up.
- The same idea, track record over time, decides which permission changes an agent gets signed automatically (see [Changing Permissions](11-changing-permissions.md)).

## Read more

- The article on this idea: [We Have Nothing. Messy Beats Nothing.](https://www.linkedin.com/pulse/we-have-nothing-messy-beats-michael-bonsignore-yi2oc/)

## Open questions

- What counts as a "kind of work"? Who writes the list of badges?
- How is a badge made hard to fake or copy? Signed by whoever granted it?
- Can a badge be taken away, and who decides?
- Who keeps track of badges, without seeing the work behind them?
