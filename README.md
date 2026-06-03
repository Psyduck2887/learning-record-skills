# Learning Record Skills

Two portable agent skills for reading and writing lightweight learning notes from a user-owned `learning_record` repository.

This repository contains:

- `learning-record-read`: loads notes for a requested topic into the current agent context.
- `learning-record-write`: appends a compact note for a solved learning problem.

The skills do not require a specific note topic, directory layout, GitHub account, or local machine path. Your own `learning_record` repository defines topics, aliases, and per-topic read/write rules.

## Repository Layout

```text
skills/
  learning-record-read/
    SKILL.md
  learning-record-write/
    SKILL.md
examples/
  learning_record/
    README.md
    typescript/
      README.md
      notes.md
```

## Install

Copy the skill directories into the skill location used by your agent runtime.

Common examples:

```sh
mkdir -p ~/.agents/skills
cp -R skills/learning-record-read ~/.agents/skills/
cp -R skills/learning-record-write ~/.agents/skills/
```

Some runtimes use `~/.codex/skills`, a project-local `.agents/skills`, or another configured skill directory. If your runtime documents a different location, copy the two folders there instead.

To confirm installation, start a fresh agent session and ask it to list or use `learning-record-read` and `learning-record-write`. The skill names must stay lowercase and hyphenated.

If your runtime cannot list installed skills, use a smoke-test prompt instead:

```text
Use learning-record-read to read TypeScript learning records from the example learning_record repository.
```

## Configure

Set `LEARNING_RECORD_REPO` to the absolute path of your own learning record repository.

Example:

```sh
export LEARNING_RECORD_REPO=/path/to/learning_record
```

If the variable is not set, the skills instruct the agent to ask for the repository path before reading or writing.

For persistent shell configuration, add the export line to your shell startup file, such as `.zshrc` or `.bashrc`. Agent runtimes do not always inherit interactive shell variables, so verify the value inside the same environment that launches the agent.

If your agent does not inherit `LEARNING_RECORD_REPO`, provide the repository path in the prompt. Both skills are written to ask for the path when the variable is missing.

## Learning Record Format

Your learning record repository should have a root `README.md` that lists supported topics and aliases. Each topic directory should have its own `README.md` that describes what files to read and how new notes should be written. Paths in topic rules should be relative to the topic directory unless the topic README says otherwise.

See `examples/learning_record/` for a minimal working template.

Root `README.md` template:

```md
# Learning Record

## Topics

| Topic | Aliases | Directory |
|---|---|---|
| TypeScript | TS, typescript | `typescript/` |
```

Topic `README.md` template:

```md
# Topic Name

## Read Rules

When reading this topic, load:

1. `notes.md`

## Write Rules

Target file:

`notes.md`

Describe the note format, duplicate-check rule, and any validation command.
```

## Recommended Workflow

1. Create your own `learning_record` repository.
2. Add a root `README.md` with topic aliases.
3. Add one directory per topic.
4. In each topic directory, add a `README.md` with read/write rules.
5. Set `LEARNING_RECORD_REPO`.
6. Ask your agent to use `learning-record-read` or `learning-record-write`.

## Troubleshooting

- Skill is not found: confirm that your runtime's skill directory contains `learning-record-read/SKILL.md` and `learning-record-write/SKILL.md`.
- Repository path is not found: set `LEARNING_RECORD_REPO` in the environment that launches the agent, or include the path in your prompt.
- Topic is not found: add the topic and aliases to the root `README.md` of your learning record repository.
- Write rules are unclear: make the topic `README.md` name the target note file, note format, duplicate-check rule, and optional validation command.
- Duplicate checks vary by agent: define a stricter duplicate rule in the topic `README.md` when you need more deterministic behavior.

## Safety Notes

- Review generated notes before publishing them.
- Do not store secrets, private credentials, or personal tokens in learning notes.
- Keep personal machine paths out of shared templates.
- Git commit and push are optional. The write skill only performs them when the user explicitly asks for repository persistence.
