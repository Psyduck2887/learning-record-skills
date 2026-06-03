---
name: learning-record-write
description: Append a compact learning note for an already solved problem to a user-configured learning_record repository.
---

# Learning Record Write

Write a lightweight note about a solved learning problem into a user-owned `learning_record` repository. Keep notes concise and practical. Do not create long retrospectives unless the user asks for that.

## Repository Path

Use the repository path from `LEARNING_RECORD_REPO`.

If `LEARNING_RECORD_REPO` is not set, ask the user for the local path to their `learning_record` repository before continuing.

Do not assume a default machine path, GitHub account, or repository location.

## Workflow

1. If the user did not specify a topic, ask which topic to write to.
2. Resolve the learning record repository path from `LEARNING_RECORD_REPO` or the user-provided path.
3. Read the repository root `README.md`.
4. Use the root `README.md` to map the requested topic or alias to a topic directory.
5. Read the topic directory `README.md`.
6. Follow that topic `README.md` exactly to find the target note file and formatting rules.
7. Draft one compact note from the already solved problem in the current conversation.
8. Check the target note file for similar existing content. Treat content as similar when it records the same topic, same problem, and same key conclusion, command, or configuration.
9. If a similar note already exists, do not append a duplicate. Tell the user similar content already exists.
10. If no similar note exists, append the new note according to the topic rules.
11. Run any validation required by the topic `README.md`.
12. Commit or push only if the user explicitly asks for Git persistence.

## Topic Rules

Topic names, aliases, target note files, formatting rules, validation commands, and commit conventions are owned by the user's `learning_record` repository. Do not hard-code topics in this skill.

If the requested topic does not exist in the root `README.md`, say that the repository does not currently define that topic. Do not guess another path.

## Git Rules

Git operations are optional and must follow the user's request and repository policy.

If the user asks to commit:

1. Check `git status --short`.
2. Run `git pull --ff-only` before committing if the repository has a remote.
3. Commit only the intended learning-record files.
4. Use a commit message that clearly describes the new note.

If pull, commit, push, or authentication fails, stop and explain the reason. Do not apply machine-specific proxy workarounds unless the user asks for them.
