# CLAUDE.md

Read BRIEF.md first. It's the source of truth for what we're building and why.

## How to work here

- Follow Apple's Human Interface Guidelines for the app. Use BelleviewOS for anything web (tokens, type scale, spacing). If a value isn't in the tokens, don't invent one. Ask.
- Write copy in plain, direct sentences. No em dashes, no jargon.
- Keep v1 small. If something isn't in BRIEF.md, ask before building it.
- When we make a decision, add it to the Decisions log below with the date.

## Planned layout

- `app/`: SwiftUI multiplatform app (iOS, iPadOS, macOS)
- `worker/`: Cloudflare Worker that renders and serves published sites
- `template/`: the website template and content type components

## Decisions log

- 2026-11-18: First audience is small associations, guilds and nonprofits.
- 2026-11-18: Build around content types, not layouts. Audience starters are presets on one shared system.
- 2026-11-18: Look settings are limited to type, width and accent.
