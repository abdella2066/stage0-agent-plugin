# Stage0 agent plugin

Publish and manage your [Stage0](https://www.stage0.dev) projects from your AI agent.

This plugin gives an agent two things:

- **The `stage0-publish` skill** teaches it the draft-to-publish workflow, Stage0's publishing checklist, hackathon tagging, and when to check with you first.
- **The Stage0 MCP server** (`stage-zero`, `https://www.stage0.dev/mcp`) gives it the tools to list, create, update, publish, unpublish, archive, and delete your projects.

You sign in with LinkedIn when your client asks. The agent can only work with your own projects.

## Install

### Claude Code

```bash
claude plugin marketplace add abdella2066/stage0-agent-plugin
claude plugin install stage0@stage0
```

Or inside a session: `/plugin marketplace add abdella2066/stage0-agent-plugin`, then `/plugin install stage0@stage0`. This installs the skill and the MCP server together.

### VS Code with GitHub Copilot

Run **Chat: Install Plugin From Source** from the Command Palette and enter `https://github.com/abdella2066/stage0-agent-plugin`. This installs the skill and the MCP server together.

### Any other agent (skill only)

```bash
npx skills add abdella2066/stage0-agent-plugin
```

The [skills CLI](https://github.com/vercel-labs/skills) needs Node.js 22.20 or later and installs the skill for Claude Code, Cursor, Codex, GitHub Copilot, and many other agents. It doesn't connect the MCP server, so add that as shown below.

### Add only the MCP server

| Client        | Command or config                                                                              |
| ------------- | ---------------------------------------------------------------------------------------------- |
| Claude Code   | `claude mcp add --transport http stage-zero https://www.stage0.dev/mcp`                        |
| VS Code       | `code --add-mcp '{"name":"stage-zero","type":"http","url":"https://www.stage0.dev/mcp"}'`     |
| Cursor        | In `~/.cursor/mcp.json`: `{"mcpServers":{"stage-zero":{"url":"https://www.stage0.dev/mcp"}}}` |
| Anything else | Add an HTTP (Streamable HTTP) MCP server with that URL                                         |

If you installed the plugin, you don't need this.

## Use it

Ask your agent something like "Add my project to Stage0" or "Publish my Stage0 project". Your client asks you to sign in with LinkedIn the first time. With the skill, the agent looks for an existing project first, never invents traction or proof, shows you what will become public, and waits for your approval before publishing.

## What's in this repo

| Path                             | Purpose                                                                                                                       |
| -------------------------------- | ----------------------------------------------------------------------------------------------------------------------------- |
| `skills/stage0-publish/SKILL.md` | The skill                                                                                                                     |
| `plugin.json`, `mcp.json`        | [Agent Plugins](https://agent-plugins.org) manifest and MCP config, read by VS Code and other compatible clients such as Cursor |
| `.claude-plugin/`, `.mcp.json`   | Claude Code plugin manifest, marketplace listing, and MCP config                                                              |

There are no hooks, scripts, or local executables. The MCP server is remote and uses OAuth, and nothing here stores credentials.

## Privacy

The MCP server is operated by Stage0. See the [Stage0 privacy policy](https://www.stage0.dev/privacy) for how your data is handled.

## Updating

When the skill changes, update `skills/stage0-publish/SKILL.md` and bump `version` in both `plugin.json` and `.claude-plugin/plugin.json`. CI checks that the manifests agree and that they are valid for the Agent Plugins schemas, Claude Code, and the skills CLI.

## License

[MIT](LICENSE)
