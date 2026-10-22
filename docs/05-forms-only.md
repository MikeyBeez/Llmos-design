# 5. Everything Is Done Through Forms

**Status: design, not built.**

## The rule

The agent doesn't write free-form commands. At each step, it fills out a form. Filling out that form is the only thing it can do.

## Why

Chains let a model produce any text, then try to run it. If the model writes `rm -rf ~`, something has to catch that after the fact.

A form flips that around. The system decides what the next step can be. The model just fills in the blanks. It can't do something the form has no blank for.

This is how the model stays outside the trust boundary. It never touches the actuators (the things that actually change the world). It hands a filled-out form to the system, and the system acts.

## How it works

Example: the next step is editing a file. The agent gets this form:

```
Edit file
  file:      [________]   must be a path the agent can write
  find:      [________]   exact text to replace
  replace:   [________]   new text
```

The agent fills it in. The system checks each field. Is the path allowed? Does the "find" text really appear in the file? Then it runs the edit.

There is no blank for "also run this shell command." So the agent can't.

## Forms can lead to forms

A task becomes a series of forms. Example, fixing a bug:

1. **Pick a file to read** → the agent names a file.
2. **Say what's wrong** → a short description.
3. **Edit file** → the form above.
4. **Run tests** → choose which tests from a list.

Each form only allows what makes sense at that step.

## What this gives you

- The model's freedom is limited to what the form allows.
- Every field can be checked on its own.
- It's easy to see, and log, exactly what the agent decided at each step.

## Open questions

- Who writes the forms, and how do new ones get added?
- What happens when a task needs a step no form covers? (One answer: the agent fills out a "request a human" form.)
