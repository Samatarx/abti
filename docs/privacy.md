# Privacy

Abti is privacy-first by design. The default version stores nothing, uploads nothing, and phones home nowhere.

## The privacy model

Abti uses only the current session context. It does not create a profile, build a learning history, persist summaries, or send data to a separate service.

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

## Why Abti is stateless

A learning debrief is most useful when a developer trusts it. Statelessness makes the trust boundary simple:

- The debrief is generated from what the assistant can already see in the current session.
- The output remains in the current session.
- No learning record is created by Abti.
- No background process watches the developer.

This keeps Abti lightweight and easy to adopt in personal, open source, and professional codebases.

## Sensitive information

Abti should not include secrets, credentials, tokens, customer data, private keys, or sensitive company information in a learning debrief. If sensitive information appears in the current session context, Abti should briefly warn the developer and exclude it from the debrief.

## Consent

Abti asks before generating a learning debrief during normal PR wrap-up. Direct invocation with `/abti` counts as consent.

Consent matters because a learning debrief should be useful, not automatic noise. It also makes the privacy behaviour visible: Abti runs when the developer asks for it or agrees to it.

## Future work

Future dashboard, sync, or team features may be useful, but they should always be opt-in. They should not change the default behaviour of the lightweight skill: use current session context, generate a learning debrief, store nothing.
