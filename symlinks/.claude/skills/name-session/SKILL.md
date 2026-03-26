---
name: name-session
description: Rename the current session and its plan file to a descriptive yyyy-mm-dd-kebab-case name. Use when the user runs /name-session, asks to name/rename the current session, or says "name this". Also use proactively at the end of a conversation when a plan was created but left with a random auto-generated name.
---

# /name-session — Name Session & Plan

Rename the current session and its associated plan file to a human-readable `yyyy-mm-dd-descriptive-kebab-case` name.

## When to run

- The user explicitly asks (`/name-session`, "name this session", "rename this")
- A plan was just created or accepted and still has an auto-generated random name (e.g., `buzzing-booping-clover`)
- Triggered by the Stop hook as a reminder before ending an unnamed session

## Step 0: Check if naming should be skipped

Before proceeding, evaluate whether the session has enough meaningful content to warrant a name. **Skip naming** (and tell the user you're skipping) if:

- The session is empty or has only a greeting/small-talk exchange
- There is no anchor topic — no code changes, no research, no debugging, no planning
- The conversation is too short or generic to produce a slug more specific than `work-session` or `misc-chat`

If skipped, output: `Skipped naming — no meaningful anchor topic.` and stop.

## Step 1: Determine the date

Use today's date in `yyyy-mm-dd` format.

## Step 2: Generate a descriptive slug

Read the conversation context (or plan file content if renaming an existing plan) and produce a short kebab-case slug (2-5 words) that captures the essence of the work. The slug should be specific enough to distinguish this session from others.

**Good slugs:**
- `bulk-picklists-endpoint`
- `fix-filter-operators-camelcase`
- `extract-list-controller`
- `zed-ruby-keyword-subcategories`
- `pr-breakdown-atomic-units`

**Bad slugs:**
- `work-session` (too vague)
- `fix-bug` (too generic)
- `update-the-metadata-controller-to-add-a-new-bulk-picklists-endpoint-with-filtering` (too long)
- `session-2026-03-26` (date is already the prefix)

## Step 3: Rename the session

Session metadata is stored in `~/.claude/sessions/<pid>.json`. Find the current session's file (match on `$$` for the PID), read it, and update the `name` field:

```bash
# Find session file for current process
PID=$$
SESSION_FILE="$HOME/.claude/sessions/${PID}.json"
```

Read the session JSON, then write it back with the updated `name` using the Edit tool or a JSON-aware rewrite. Do NOT use `/rename` — it is a built-in CLI command that cannot be invoked programmatically.

## Step 4: Rename the plan file (if one exists)

Check the configured plans directory for a plan file associated with this session. The plans directory is configured in `~/.claude/settings.json` under the `plansDirectory` key. If not set, fall back to `~/.claude/plans/`.

Look for files with auto-generated random names (three-word pattern like `adjective-verb-noun.md`). If the most recently modified random-named file matches the current session's plan, rename it:

```bash
mv "<plansDir>/random-name.md" "<plansDir>/yyyy-mm-dd-slug.md"
```

If the plan file already has a descriptive name, skip this step.

## Step 5: Confirm

Tell the user the new name. Keep it brief:

```
Named: 2026-03-26-bulk-picklists-endpoint
```
