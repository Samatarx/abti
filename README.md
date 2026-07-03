<p align="center">
  <img src="assets/abti.png" alt="Abti illustration" width="252">
</p>

# Abti

Your helpful uncle for AI-assisted coding — turning coding sessions into learning debriefs before you open a PR.

Abti is a lightweight, platform-agnostic coding debrief skill. Near the end of an AI-assisted coding session, it helps you pause and understand what changed, what you practised, what the AI helped with, and what you should be comfortable explaining before you merge.

## Origin

Abti means “maternal uncle” in Somali.

The idea is simple: after you use AI to build something, Abti is the helpful uncle who sits with you for a minute and explains what just happened. Warm, practical, honest, and encouraging — not a school report, not a performance review, and not surveillance.

## What Abti does

- Summarises what changed
- Identifies concepts practised
- Explains what the AI helped with
- Lists what the developer should understand before merging
- Asks quick understanding-check questions
- Suggests one follow-up exercise
- Produces learning tags

## Privacy

The free skill is stateless.

Abti:

- Does not store prompts
- Does not store code
- Does not store summaries
- Does not store learning tags
- Does not upload anything
- Does not track the user
- Only uses the current session context

It should not include secrets, credentials, tokens, customer data, or sensitive company information in a debrief.

## Platform support

Abti is platform-agnostic.

Supported adapters are included for Claude Code and Codex. A generic prompt version is also included for other AI coding tools, custom instruction files, rule files, or prompt libraries.

## Installation

### Codex

Copy the Codex skill into your local Codex skills directory:

```bash
mkdir -p ~/.codex/skills
cp -R skills/codex/abti ~/.codex/skills/abti
```

Then restart Codex so it can load the skill.

### Claude Code

Copy the Claude Code skill into your local Claude skills directory:

```bash
mkdir -p ~/.claude/skills
cp -R skills/claude/abti ~/.claude/skills/abti
```

Then restart Claude Code so it can load the skill.

## Usage

During normal coding, Abti stays out of the way. It should not interrupt implementation, debugging, refactoring, or test-writing.

Near PR time, when you are preparing a PR summary, commit message, branch name, diff summary, release note, or final review, Abti asks whether you want a learning debrief.

You can also invoke it directly with:

```text
/abti
```

Direct invocation counts as consent. If there is enough session context, Abti generates the debrief. If not, it asks for a diff, PR summary, files changed, or a short task summary first.

## Optional end-of-session reminders

Abti is usually invoked by the assistant when it notices that you are wrapping up a coding session.

Sometimes the model can miss that moment.

You can always invoke Abti manually:

```text
/abti
```

For Claude Code users, Abti can also be paired with an optional `Stop` hook that prints a reminder at the end of coding sessions with recent git activity.

The hook does not store anything.

It does not upload anything.

It does not read file contents.

It does not analyse prompts or code.

It only checks whether the current directory is a git repo with recent changes or recent commits, then prints a reminder.

Example reminder:

```text
Abti: session ending — if this work is heading to a PR, commit, or branch, ask whether the user wants an Abti learning debrief.
```

Example Claude Code hook command:

```sh
git -C "$CLAUDE_PROJECT_DIR" rev-parse --is-inside-work-tree >/dev/null 2>&1 \
  && [ -n "$(git -C "$CLAUDE_PROJECT_DIR" status --porcelain 2>/dev/null)$(git -C "$CLAUDE_PROJECT_DIR" log --oneline -3 --since='8 hours ago' 2>/dev/null)" ] \
  && echo "Abti: session ending — if this work is heading to a PR, commit, or branch, ask whether the user wants an Abti learning debrief."
```

This is optional. Abti still works without hooks by manually invoking `/abti` or by asking for a PR summary, commit message, branch name, diff summary, release note, or final review.

For non-Claude tools, use the generic prompt or adapter-specific instructions. Any reminder should remain optional and privacy-preserving.

## Example trigger phrases

- “Write a PR summary”
- “Create a commit message”
- “Summarise this diff”
- “Is this ready to push?”
- “Help me prepare this PR”

## Roadmap

- Generic prompt
- Cursor rules
- Windsurf rules
- OpenCode support

## License

MIT. See [LICENSE](LICENSE).
