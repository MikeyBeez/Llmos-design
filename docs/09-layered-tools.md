# 9. Tools Load in Layers

**Status: design, not built.**

## The rule

Tools are arranged in a tree, so they don't all crowd into the model's context window. Choosing a tool can happen in a separate context window. Only the request and the answer come back to the main one.

## Why

Every tool an agent knows about takes up room in its context window. A hundred tools can eat thousands of tokens before the agent has done anything. The model also gets worse at picking the right tool when the list is long.

Your computer doesn't load every program into memory at boot. It loads what it needs, when it needs it.

## How it works

Tools sit in folders, like the tree in [Tools are files](02-tools-are-files.md):

```
/tools/
  code/      edit_file, read_file, run_tests ...
  web/       search, fetch ...
  mail/      read, send ...
```

The main agent only sees the top level: "code, web, mail." When it needs to do something with code, a side task opens in a fresh context window. That side task looks inside `/tools/code/`, picks the right tool, and fills in its [form](05-forms-only.md).

Only two things go back to the main window:

- what was asked
- what came back

All the in-between work, like reading tool descriptions and trying options, stays in the side window and is thrown away.

One way to make this fast: start the side window from a copy of the main window's cached prefix (the KV cache), so it doesn't have to reread everything.

## What this gives you

- A main context window that stays small and clear.
- Room for thousands of tools on a system without slowing any one agent down.
- The same trick works for protocols, not just tools.

## Open questions

- How deep should the tree go before picking a tool takes too many steps?
- How does the main agent know which branch to open without seeing what's inside?
