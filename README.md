# MontezuBot

MontezuBot is a **Civilization VI Discord game-session bot** built to coordinate multiplayer setup, voting, leader management, concessions, results, and lightweight league/community workflows.

The project grew around the practical friction of organizing Civ games in Discord: getting players aligned on settings, tracking decisions, managing leader-related actions, and keeping the session moving without a human moderator doing everything manually.

> **Status:** Mature lab project. The core bot lives in `civ6_draft_bot.py` and is deployable as a persistent Discord process.

## Core Capabilities

- Starts and coordinates multiplayer game sessions
- Runs settings/player votes inside Discord
- Manages leader-related actions and swaps
- Supports concession voting
- Tracks game outcomes and leaderboard-oriented data
- Provides Discord messages/reactions around session state
- Includes supporting leader-matching and website-sync utilities

Representative commands include:

- `.vote` — start a session and open configuration voting
- `.trade` — offer a leader-list trade between players
- `.cc` — start a timed concession vote

Use the bot's built-in command/help surface as the authority for the complete current command set.

## Repository Layout

```text
civ6_draft_bot.py       Main Discord bot
leader_match.py         Supporting leader matching logic
website_sync.py         Website/data synchronization helper
docs/                   Project and workflow documentation
Procfile                 Hosted process entry point
requirements.txt         Python dependencies
```

## Quick Start

### Requirements

- Python 3
- A Discord application/bot token
- Discord permissions required by the commands you intend to use

### Install

```bash
pip install -r requirements.txt
```

### Configure

Keep Discord tokens and deployment secrets outside source control. Prefer environment variables or the repository's current configuration pattern rather than hard-coding credentials into the bot source.

### Run

```bash
python civ6_draft_bot.py
```

A `Procfile` is included for persistent hosted deployments.

## Development Notes

MontezuBot is intentionally focused on **session orchestration**, not becoming a general-purpose Discord utility bot. When extending it:

- keep game-state changes deterministic and attributable;
- avoid trusting reactions/messages as durable state when a workflow needs restart safety;
- validate authorization for moderator-only actions at execution time;
- prefer small, explicit commands over fragile free-text parsing;
- update documentation when the player-facing workflow changes.

## AI-Assisted Changes

Before AI-assisted implementation, debugging, refactoring, migration, or production fixes, review [`docs/AI_WORKFLOW_GUARDRAILS.md`](./docs/AI_WORKFLOW_GUARDRAILS.md).

The default posture is the smallest safe change with low blast radius, no unrelated rewrites, and explicit consideration of retries, idempotency, rollback, and operational safety where relevant.
