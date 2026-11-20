# Onboarding — Discord for AI Agents

**Goal: a working, bot-managed Discord server in under 2 minutes.**

---

## The three steps

### 1 · Install (30 s)

Inside Claude Code:

```
/plugin marketplace add JCodesMore/jcodesmore-plugins
/plugin install discord@jcodesmore-plugins
```

**Fully quit and reopen Claude Code.** Skills are loaded at startup; a hot-reload will not pick them up.

### 2 · Setup wizard (60 s)

```
/discord:setup
```

The wizard, in chat:

- Asks if you already have a bot. If no, it links you to the Discord developer portal and tells you exactly where to click.
- Takes your token (paste once; stored locally at `${CLAUDE_PLUGIN_DATA}/credentials.json`).
- Verifies the token against Discord.
- Generates an invite URL if the bot isn't in a server yet.
- Locks in an **active guild** — the server all future commands target until you switch.

### 3 · Build (the rest is talking)

```
/discord make me a Product Hunt launch server for clow.studio
```

or pick a bundled template:

```
/discord apply the clow-studio-launch template
```

That's it. Everything else is one chat message away.

---

## Day-two cheat sheet

| Intent                          | Say to Claude                                                             |
| ------------------------------- | ------------------------------------------------------------------------- |
| Switch active server            | `/discord switch to guild <id>`                                           |
| See what's configured           | `/discord show me the current guild + tool count`                         |
| Dry-run a template              | `/discord preview the dev-community template`                             |
| Add one channel                 | `/discord create #announcements under category Info with topic "..."`     |
| Give yourself a role            | `/discord add Admin role (color #ED4245, admin perms) and grant it to me` |
| Lock down invite spam           | `/discord add an AutoMod rule blocking discord.gg invites for non-mods`   |
| Schedule an event               | `/discord schedule "Launch stage" in Launch Stage voice, Fri 7pm UTC`     |
| Welcome screen                  | `/discord set a welcome screen with rules, intros, and openclaw channels` |
| Nothing wrapped? Use the escape | `/discord raw request to PATCH /guilds/{id}`                              |

---

## Bundled templates

| Template                           | Use when                                                        |
| ---------------------------------- | --------------------------------------------------------------- |
| `ai-community`                     | General AI builders / researchers / discord server              |
| `blockchain-enterprise-community`  | Web3 / token / validator community                              |
| `clow-ecosystem`                   | PicoClaw + OpenClaw contributor + research community            |
| **`clow-studio-launch`**           | **Product Hunt launch-day HQ for clow.studio** (new)            |
| `content-creator`                  | Streamer / YouTuber audience hub                                |
| `dev-community`                    | Open-source project community                                   |
| `gaming-community`                 | Game / esports / tournament server                              |
| `startup-team`                     | Small internal team server                                      |
| `study-group`                      | Cohort-based learning                                           |

Any template is a JSON spec in `templates/`. Copy, tweak, re-apply.

---

## Troubleshooting (90% of issues)

| Symptom                                   | Fix                                                                     |
| ----------------------------------------- | ----------------------------------------------------------------------- |
| "Unknown token" / 401                     | Token was rotated. Reset at discord.com/developers, re-run `/discord:setup`. |
| "Missing Permissions" / 50013             | Your bot's role isn't above the role/channel it is editing. Drag it up. |
| Member-related tool fails                 | Turn on **Server Members Intent** in the Bot tab of the dev portal.     |
| New channels not visible                  | Fully quit and reopen Discord — client cache.                           |
| Skills didn't load after install          | Fully quit and reopen **Claude Code** — same cache story on that side.  |

---

## Safety defaults

- **Create-only**: templates and the architect agent never delete or overwrite. Name collisions are silently skipped.
- **Dry-run first** for destructive intents: ask Claude to "preview" or "show me the plan" before applying.
- **Tokens stay local**: the only place the token is written is `${CLAUDE_PLUGIN_DATA}/credentials.json`. It is never sent anywhere except `discord.com`.
- **MFA flag**: if your bot owner account has 2FA, tick "Bot owner has MFA enabled" in `/plugin` config — needed for kick/ban in production servers.

---

## For AI agents reading this

- MCP server URL: see `package.json` → `"bin": "discord-mcp"`
- Capability card: `/.well-known/ai-plugin.json`
- LLM summary: `/llms.txt`
- Canonical repo: https://github.com/JCodesMore/discord-for-ai-agents
