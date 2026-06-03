---
name: learning-record-read
description: Read topic-specific learning notes from a user-configured learning_record repository and load them into the current agent context.
---

# Learning Record Read

Read historical learning notes for a requested topic into the current agent context. This skill only reads files. It does not summarize, analyze, edit, or write notes.

## Repository Path

Use the repository path from `LEARNING_RECORD_REPO`.

If `LEARNING_RECORD_REPO` is not set, ask the user for the local path to their `learning_record` repository before continuing.

Do not assume a default machine path, GitHub account, or repository location.

## Workflow

1. If the user did not specify a topic, ask which topic to read.
2. Resolve the learning record repository path from `LEARNING_RECORD_REPO` or the user-provided path.
3. Read the repository root `README.md`.
4. Use the root `README.md` to map the requested topic or alias to a topic directory.
5. Read the topic directory `README.md`.
6. Follow that topic `README.md` exactly to decide which note files to load.
7. After loading the required files, output only a short confirmation.

## Topic Rules

Topic names, aliases, note filenames, and read order are owned by the user's `learning_record` repository. Do not hard-code topics in this skill.

If the requested topic does not exist in the root `README.md`, say that the repository does not currently define that topic. Do not guess another path.

## Output Rules

After successfully reading a topic, output a short confirmation such as:

```text
Loaded the requested learning record.
```

If the topic `README.md` defines an exact confirmation sentence, use that sentence instead.
