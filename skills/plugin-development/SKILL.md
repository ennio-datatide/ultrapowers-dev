---
name: Plugin Development
description: >
  Use when creating, structuring, validating, or publishing Claude Code plugins
  and self-hosted marketplaces — covers plugin.json manifests, skill authoring,
  marketplace setup, versioning, and multi-platform distribution.
---

# Plugin Development

Build plugins that work across Claude Code, Cowork, and Cursor. A plugin bundles skills, hooks, agents, and MCP servers into a single installable package.

## When to Use

- Creating a new Claude Code plugin from scratch
- Adding skills, hooks, or agents to an existing plugin
- Setting up a self-hosted marketplace for distribution
- Publishing to the official Anthropic marketplace
- Managing versions and updates across multiple plugins

## Plugin Structure

```
my-plugin/
├── .claude-plugin/
│   └── plugin.json          # Required — only plugin.json goes here
├── skills/                   # Optional — skill directories
│   └── my-skill/
│       └── SKILL.md
├── agents/                   # Optional — custom agents
├── hooks/                    # Optional — hooks.json for event handlers
│   └── hooks.json
├── commands/                 # Optional — slash commands
├── .mcp.json                 # Optional — MCP server configs
├── .lsp.json                 # Optional — LSP server configs
├── settings.json             # Optional — default plugin settings
├── README.md                 # Recommended — documentation
├── LICENSE                   # Recommended — license file
└── CHANGELOG.md              # Recommended — version history
```

**Critical:** Only `plugin.json` goes inside `.claude-plugin/`. Skills, agents, hooks, and commands go at the plugin root.

## plugin.json Manifest

```json
{
  "name": "my-plugin",
  "description": "What this plugin does",
  "version": "1.0.0",
  "author": {
    "name": "Your Name",
    "url": "https://yoursite.com"
  },
  "homepage": "https://docs.yoursite.com",
  "repository": "https://github.com/you/my-plugin",
  "license": "MIT",
  "keywords": ["skills", "relevant", "tags"]
}
```

| Field | Required | Notes |
|-------|----------|-------|
| `name` | Yes | Kebab-case, lowercase, no spaces |
| `description` | No | Shown in plugin manager |
| `version` | No | Semantic versioning (MAJOR.MINOR.PATCH) |
| `author` | No | Object with `name`, optional `email` and `url` |
| `homepage` | No | Documentation URL |
| `repository` | No | Source code URL |
| `license` | No | SPDX identifier (MIT, Apache-2.0) |
| `keywords` | No | Array of discovery tags |

## Writing Skills

Each skill lives in its own directory with a `SKILL.md` file.

```markdown
---
name: My Skill
description: Use when [trigger condition] — [what it does]
---

# My Skill

[Opening line — what this skill helps with]

## When to Use

- [Specific trigger condition 1]
- [Specific trigger condition 2]

## [Main content sections]
```

**The `description` field is critical.** It determines when the agent automatically activates the skill. Write it as a clear trigger condition, not a marketing blurb.

### Skill Best Practices

- **One concern per skill** — don't combine unrelated topics
- **Actionable content** — patterns, rules, and examples, not theory
- **Tables over prose** — agents parse structured data faster
- **Include "When to Use"** — explicit activation criteria
- **No frontmatter = validation warning** — always include `---` delimiters with at least `name` and `description`

## Validation

Always validate before publishing:

```bash
claude plugin validate .
```

Checks: JSON syntax, manifest schema, skill frontmatter, hook configurations. Fix all errors and warnings — aim for zero warnings.

## Self-Hosted Marketplace

A marketplace is a GitHub repo with a `marketplace.json` that lists available plugins. Users add it once and can install any plugin from it.

### marketplace.json

```json
{
  "name": "my-marketplace",
  "metadata": {
    "description": "What this marketplace offers"
  },
  "owner": {
    "name": "Your Name",
    "url": "https://yoursite.com"
  },
  "plugins": [
    {
      "name": "local-plugin",
      "description": "Plugin in same repo",
      "version": "1.0.0",
      "source": "./"
    },
    {
      "name": "external-plugin",
      "description": "Plugin from another repo",
      "version": "1.0.0",
      "source": {
        "source": "github",
        "repo": "owner/other-repo"
      }
    }
  ]
}
```

The marketplace.json goes in `.claude-plugin/marketplace.json` — it can coexist with `plugin.json` in the same repo.

### Source Types

| Type | Format | Use Case |
|------|--------|----------|
| Relative path | `"./"` or `"./plugins/foo"` | Plugin in same repo |
| GitHub | `{"source": "github", "repo": "owner/repo"}` | Public/private GitHub repos |
| Git URL | `{"source": "url", "url": "https://..."}` | GitLab, Bitbucket, self-hosted |
| Git subdirectory | `{"source": "git-subdir", "url": "...", "path": "..."}` | Monorepo plugins |
| npm | `{"source": "npm", "package": "@org/plugin"}` | npm registry |

Pin versions with `"ref": "v2.0.0"` or `"sha": "a1b2c3d4..."` on any git source.

### User Commands

```bash
# Add marketplace (one time)
/plugin marketplace add owner/repo

# Install a plugin
/plugin install plugin-name@marketplace-name

# Update marketplace index
/plugin marketplace update

# Update installed plugins
/plugin update plugin-name
```

## Publishing to Official Marketplace

Submit through the web form at:
- https://claude.ai/settings/plugins/submit
- https://platform.claude.com/plugins/submit

No CLI submission — web form only. Anthropic runs automated review before listing. Plugins with "Anthropic Verified" badge get additional manual review.

## Versioning

Use semantic versioning: `MAJOR.MINOR.PATCH`

| Change | Bump | Example |
|--------|------|---------|
| Breaking changes | MAJOR | Removed a skill, changed behavior |
| New features | MINOR | Added a skill, new capability |
| Bug fixes | PATCH | Fixed typo, improved description |

**Always bump version before pushing.** Claude Code caches plugins — if you change code without bumping version, users won't see updates.

## Multi-Platform Distribution

| Platform | Install Method |
|----------|---------------|
| Claude Code | `/plugin install name@marketplace` |
| Claude Cowork | Browse plugins in Customize menu |
| Cursor | `/add-plugin name` or marketplace search |
| Codex | Clone + symlink to `~/.agents/skills/` |
| OpenCode | Add to `plugin` array in `opencode.json` |
| Gemini CLI | `gemini extensions install github-url` |

### Platform-Specific Config Files

```
.claude-plugin/plugin.json     # Claude Code + Cowork
.cursor-plugin/plugin.json     # Cursor
.codex/INSTALL.md              # Codex install guide
.opencode/INSTALL.md           # OpenCode install guide
gemini-extension.json          # Gemini CLI
```

## Development Workflow

1. **Develop locally** — edit skills in your local clone
2. **Test locally** — `claude --plugin-dir ./` loads local version
3. **Validate** — `claude plugin validate .` before every push
4. **Bump version** — update `version` in plugin.json
5. **Commit and push** — changes flow to marketplace automatically
6. **Users update** — `/plugin update name` or `/plugin marketplace update`

## Environment Variables

Two variables available inside plugin files:

| Variable | Purpose |
|----------|---------|
| `${CLAUDE_PLUGIN_ROOT}` | Absolute path to plugin install directory (wiped on update) |
| `${CLAUDE_PLUGIN_DATA}` | Persistent directory for state across updates |

Use `CLAUDE_PLUGIN_DATA` for anything that must survive updates (caches, user config). Use `CLAUDE_PLUGIN_ROOT` for referencing bundled scripts and assets.

## Cross-Platform Hooks

Hooks must work on Windows, macOS, and Linux. Use a polyglot `.cmd` wrapper:

```cmd
: << 'CMDBLOCK'
@echo off
"C:\Program Files\Git\bin\bash.exe" -l -c "\"$(cygpath -u \"$CLAUDE_PLUGIN_ROOT\")/hooks/my-hook.sh\""
exit /b
CMDBLOCK

# Unix shell runs from here
"${CLAUDE_PLUGIN_ROOT}/hooks/my-hook.sh"
```

Windows CMD sees `:` as a label and runs the batch block. Unix bash sees it as a no-op heredoc and skips to the shell command. Point `hooks.json` to the `.cmd` file, not the `.sh` file.

## Common Mistakes

| Mistake | Fix |
|---------|-----|
| Putting skills inside `.claude-plugin/` | Move to plugin root `skills/` |
| Missing `description` in SKILL.md frontmatter | Add `description:` field — it controls auto-activation |
| Not bumping version | Users won't get updates due to caching |
| `description` at root of marketplace.json | Use `metadata.description` instead |
| Hardcoded paths in hooks | Use `${CLAUDE_PLUGIN_ROOT}` variable |
| No validation before push | Always run `claude plugin validate .` |
