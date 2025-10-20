---
description: Generate a commit message based on current changes
---


# Commit Command

You need to help the user generate a high-quality commit message. Please strictly follow the process below to ensure each commit addresses only one thing (single responsibility) and that branch logic is clear:

## 0. Use the bg-worker agent to perform the following steps

## 1. Fetch Git Information

Run the following commands in parallel to get the current repository state:

- `git diff` - View unstaged changes
- `git diff --staged` - View staged changes
- `git status` - View current branch and file status
- `git log --oneline -10` - View the last 10 commits to understand the commit message format style

## 2. Analyze Changes (Branch & Single Responsibility)

Based on the fetched information, analyze:

- Current branch name, ensuring the branch is clearly named and follows team conventions
- File types and scope of changes, confirming this commit only involves a single independent change (e.g., only fixing one bug, only adding one feature, or only optimizing one piece of code)
- Nature of changes (feature, fix, refactor, docs, etc.), avoiding mixing multiple types of changes in one commit
- Commit message format style in history (whether using emoji, English/Chinese, following conventional commits, etc.)

> **Note: If multiple independent changes are detected, help the user to split them into multiple commits, each commit addressing only one thing.**

## 3. Generate Commit Message

Based on the above analysis, generate a commit message that meets the following requirements:

- **Follow project style**: Based on the historical commit format seen in git log
- **Accurately describe changes**: Clearly explain what was changed and briefly state the reason (why), not just what was done (what)
- **Be concise**: Keep the first line within 50-72 characters (if in English)
- **Use correct type**: Such as feat, fix, docs, refactor, test, chore, etc. (if the project uses conventional commits)
- **Single responsibility**: Ensure the each commit message only describes one independent change

## 4. Output Format

After generating the commit message, display it directly to the user and ask whether to:

1. Use this message to commit
2. Modify it
3. Regenerate

**Important Notes**:

- If there are no changes (git status shows clean), inform the user there are no changes to commit
- If there are only unstaged changes, ask the user if they need to add files first
- If multiple independent changes are detected, remind the user to split them into multiple commits
- The commit message should describe "why" the change was made, not just "what" was done
