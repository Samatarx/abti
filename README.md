<p align="center">
  <img src="assets/abti.png" alt="Abti illustration" width="252">
</p>

# Abti

AI helps you ship faster. Abti helps you understand what you shipped.

A lightweight coding debrief skill that turns AI-assisted coding sessions into learning moments before you open a pull request.

<p align="center">
  <a href="LICENSE"><img alt="License: MIT" src="https://img.shields.io/badge/license-MIT-black.svg"></a>
  <img alt="No telemetry" src="https://img.shields.io/badge/telemetry-none-black.svg">
  <img alt="Stateless" src="https://img.shields.io/badge/storage-stateless-black.svg">
  <img alt="Adapters" src="https://img.shields.io/badge/adapters-Claude%20Code%20%7C%20Codex-black.svg">
</p>

## Why Abti exists

AI coding assistants help developers produce more code than ever before. That is useful, but it creates a quiet problem: after a fast session, it can be hard to tell what you actually practised, what the assistant solved for you, and whether you could explain the implementation yourself.

Abti exists for that moment.

It does not interrupt your coding flow. It waits until PR time, then offers a short learning debrief based only on the current session context. The goal is simple: help you leave the session with a clearer understanding of the code you are about to share.

Abti means “maternal uncle” in Somali. The tone is intentionally calm and practical: a helpful senior engineer sitting with you for a minute before you open the pull request.

## Example

```md
# Abti Learning Debrief

## 1. What You Practised

- Refactored a React form so validation lives beside the submit flow instead of being spread across event handlers.
- Tightened TypeScript types around the API response so the UI no longer assumes optional fields are present.
- Added regression tests for the empty-state and failed-submit paths.

## 2. What The AI Helped With

- Suggested a smaller validation helper and updated the affected call sites.
- Drafted test cases for the failure path and loading state.
- Helped identify a stale mock that no longer matched the API contract.

## 3. What You Should Understand Before Merging

- Why the validation helper returns structured errors instead of throwing.
- How the component behaves when the API returns a partial profile.
- Which tests would fail if the submit button became enabled too early.

## 4. Quick Questions

- What user action triggers validation now?
- Why is `ProfileResponse.email` treated as optional?
- Which test protects the failed-submit path?

Try answering these yourself first. I can check your answers if you want.

## 5. Things To Double-Check

- Confirm the disabled button state still works with keyboard submission.
- Re-run the form tests after rebasing onto the latest API changes.

## 6. One Follow-Up Exercise

Write one additional test for a slow network response where the user edits the form while submission is pending.

## 7. Learning Tags

React, TypeScript, form validation, API contracts, regression testing, accessibility

Nothing was stored — this debrief lives only in this session.
```

## Early Feedback

> "I've kept Abti installed all week. The insights are genuinely useful and it's become part of how I wrap up work before opening a PR."
>
> — Senior Software Engineer

## Features

- PR-time learning debriefs that help you understand what changed before merging.
- Current-session only: Abti uses the current session context and does not rely on saved history.
- Stateless by design.
- Works with Claude Code.
- Works with Codex.
- Generic prompt included for other AI coding assistants, rule files, and prompt libraries.
- Privacy-first: no uploads, no storage, no telemetry, no phone-home behaviour.
- Asks before generating a learning debrief during normal PR wrap-up.
- Direct invocation with `/abti` when you want a learning debrief immediately.

## Installation

From a local checkout of this repository, copy the adapter for your coding assistant.

### Claude Code

```bash
mkdir -p ~/.claude/skills
cp -R skills/claude/abti ~/.claude/skills/abti
```

Restart Claude Code so it can load the skill.

### Codex

```bash
mkdir -p ~/.codex/skills
cp -R skills/codex/abti ~/.codex/skills/abti
```

Restart Codex so it can load the skill.

### Generic Prompt

Use the generic prompt when your assistant supports custom instructions, project rules, prompt libraries, or reusable snippets.

```bash
cat skills/generic/abti.md
```

Copy the contents of `skills/generic/abti.md` into the relevant instruction or rules location for your tool.

## Usage

Normal flow:

```text
Code with your AI assistant
↓
Ask for a PR summary, commit message, diff summary, release note, or final review
↓
Abti offers a learning debrief
↓
You choose whether to generate it
↓
Nothing is stored
```

Abti stays quiet during implementation, debugging, refactoring, and test-writing. If you ask for a PR summary, it should help with the PR summary first, then ask whether you want an Abti learning debrief too.

Direct invocation:

```text
/abti
```

Direct invocation counts as consent. If there is enough current session context, Abti generates the learning debrief immediately. If there is not enough context, it asks for a diff, PR summary, files changed, or a short task summary.

## How it works

Abti is a small instruction set for AI coding assistants:

```text
Developer
↓
Coding assistant
↓
Abti
↓
Learning debrief
```

It intentionally sits after implementation instead of during it. During coding, your assistant should focus on helping you build. Near PR time, Abti helps you pause and understand what happened.

Read more in [docs/architecture.md](docs/architecture.md) and [docs/behaviour.md](docs/behaviour.md).

## Privacy

Abti is privacy-first because learning debriefs only work when developers trust the tool.

Abti does **not**:

- Upload prompts.
- Upload code.
- Store code.
- Store prompts.
- Store learning history.
- Store learning tags.
- Phone home.
- Include telemetry.
- Analyse anything in the background.

Everything happens inside the current session context. If sensitive information appears in the session, Abti should exclude it from the learning debrief and briefly warn you.

Read the full privacy notes in [docs/privacy.md](docs/privacy.md).

## FAQ

### Why doesn’t Abti save anything?

Because the first version is meant to be trusted, lightweight, and easy to reason about. Abti helps you understand the current session, then leaves no learning history behind.

### Why isn’t it automatic?

Because a learning debrief should be a choice. Abti asks before generating one during PR wrap-up and only runs immediately when you invoke `/abti` directly.

### Can I use it outside Claude Code?

Yes. Use the generic prompt in `skills/generic/abti.md` with any assistant that supports reusable instructions or rules.

### Can I use it with Codex?

Yes. A Codex adapter is included in `skills/codex/abti`.

### Can I use it with Cursor?

Not as a dedicated adapter yet. You can use the generic prompt today, and Cursor support is on the roadmap.

### Why ask before generating the debrief?

Consent keeps Abti from becoming noise. It also reinforces the privacy model: the debrief is generated only when you ask for it or agree to it.

### Will there be a dashboard?

Possibly, but not in the current lightweight skill. Any future dashboard, sync, or team feature should be opt-in and should not change the default “store nothing” behaviour.

## Roadmap

These are future work, not current features:

- Improve adapters.
- Cursor support.
- Windsurf support.
- OpenCode support.
- Local dashboard.

## Contributing

Contributions should keep Abti small, clear, and privacy-first.

Good contributions include:

- Clearer installation instructions.
- Better examples from real software engineering work.
- Adapter improvements for existing tools.
- Documentation that makes behaviour and privacy easier to understand.
- New adapters that preserve consent and statelessness.

Please avoid adding telemetry, analytics, storage, cloud services, dashboards, authentication, or monetisation features in this repository unless they are explicitly scoped as opt-in future work.

## Support Abti

If Abti helped you understand something you built, here are a few ways you can support the project:

- ⭐ Star the repository
- 🐛 Report bugs or suggest improvements
- 💡 Open an issue if something feels confusing
- 🤝 Share Abti with another developer

Every issue, discussion, suggestion and star helps make Abti better.

## Built by the Team Behind Offdays

Abti is an independent open source project created by the team behind **Offdays**.

Offdays helps people plan and manage their time off with a calm, privacy-first experience.

If you'd like to support the people building Abti, take a look:

→ https://offdays.io

## License

MIT. See [LICENSE](LICENSE).
