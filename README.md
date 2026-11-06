# Hypotize for Hermes Agent

Turn Hermes into a disciplined growth hacker. This plugin connects Hermes Agent to [Hypotize](https://hypotize.ai/?utm_source=hermes&utm_medium=marketplace), the agent-native Growth OS for growth, product and marketing teams.

With Hypotize connected, Hermes reads what the team already tested before proposing anything new. It writes hypothesis-first ideas, scores them with ICE, PIE, RICE or your own framework, moves experiments through an enforced lifecycle (Idea, Approved, Ready, Running, Analyzing, then a measured outcome) and records the result and the learning. The next conversation starts from what you already know.

Hypotize does not run A/B tests or assign traffic. Keep your analytics and experimentation tools: Hypotize keeps the record before and after an experiment runs.

## What is inside

- **MCP server**: the hosted Hypotize server at `https://api.hypotize.ai/mcp`, OAuth 2.1. You sign in to Hypotize in the browser when Hermes connects.
- **Skills**:
  - `hypotize-growth-experiments`: the method. Read before proposing, vote with evidence, follow the lifecycle, close with a measured result.
  - `hypotize-weekly-review`: a read-only pipeline review that ends with what needs a decision.
  - `hypotize-backlog-import`: move a spreadsheet or Notion backlog into Hypotize, in atomic batches of 50.

## Install in Hermes Agent

```bash
hermes plugins install hypotize
```

Requires Node.js 20.18.1 or newer with npm, because sign-in runs through `mcp-remote`. When Hermes calls a Hypotize tool and you are not signed in yet, a browser window opens: sign in with Google or email and approve access. If Hermes stops waiting before you finish signing in, run `/reload-mcp` once you are done: the saved sign-in is reused. Then ask Hermes, for example: "Read my Hypotize backlog and tell me which idea to test next."

You need a Hypotize account. The free plan works: [sign up](https://hypotize.ai/auth?utm_source=hermes&utm_medium=marketplace).

## What the plugin does on your machine

- **Network calls**: every tool call goes to Hypotize's hosted server (`api.hypotize.ai`) and acts on your Hypotize account with your role in each project. The tool set is served by that server at runtime and is not part of the pinned commit.
- **Sign-in**: Hermes starts the pinned `mcp-remote@0.1.49` through `npx`. Until you sign in, it opens a browser and a local callback port, then stores OAuth tokens under `~/.mcp-auth`. Run it once in an interactive session: an unattended run (cron, the messaging gateway) cannot complete the browser sign-in.
- **Approvals**: the package marks the server `untrusted`, so Hermes asks before every tool the server does not mark read-only and refuses them in unattended runs. Delete access is off unless you grant it when you sign in.
- **No telemetry** in the plugin. Hypotize stores the experiments, votes, comments and learnings you or Hermes write, under the [privacy policy](https://hypotize.ai/privacy).

## Links

- [Hypotize](https://hypotize.ai/?utm_source=hermes&utm_medium=marketplace)
- [MCP setup for other agents](https://hypotize.ai/mcp?utm_source=hermes&utm_medium=marketplace)
- Support: hello@hypotize.ai

## License

MIT
