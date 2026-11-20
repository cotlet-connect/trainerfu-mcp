# Trainerfu MCP server for ChatGPT and Claude

Trainerfu connects training plans, activity and client conversations. Cotlet.dev connects ChatGPT, Claude and other AI agents to your signed-in Trainerfu account through its hosted Cloud Browser connection.

## What you can ask

> Review the selected client's training plan.

> Review recorded progress entries for the selected client and period.

> Read the client diary before drafting a check-in response.

> Look up the selected client's assigned workouts.

## Connect your AI agent

Start at https://cotlet.dev/signup?app=trainerfu and sign in to Trainerfu in your Cotlet Cloud Browser. ChatGPT and Claude use Cotlet sign-in; editors and scripts use an API key from https://cotlet.dev/app, exported as `COTLET_API_KEY`.

### ChatGPT

Settings → Apps & Connectors → Create, connector URL `https://cotlet.dev/mcp/v1/connect`, then sign in with Cotlet.dev. No API key needed.

### Claude

Settings → Connectors → Add custom connector, URL `https://cotlet.dev/mcp/v1/connect`, then sign in with Cotlet.dev.

### Claude Code

```bash
claude mcp add --transport http cotlet https://cotlet.dev/mcp/v1 --header "Authorization: Bearer $COTLET_API_KEY"
```

### Cursor

Copy `.cursor/mcp.json` from this repo into your project:

```json
{
  "mcpServers": {
    "cotlet": {
      "url": "https://cotlet.dev/mcp/v1",
      "headers": {
        "Authorization": "Bearer ${COTLET_API_KEY}"
      }
    }
  }
}
```

## Run the local MCP bridge

Python 3.10+, with no dependencies. Clone this repository, set your Cotlet.dev API key, then run:

```bash
export COTLET_API_KEY="your-key"
python3 trainerfu_agent.py serve
```

This local stdio bridge lists seven browser helper tools: `trainerfu_guide`, `trainerfu_status`, `trainerfu_open`, `trainerfu_read`, `trainerfu_click`, `trainerfu_type` and `trainerfu_close`.
It forwards calls to the hosted Cotlet.dev MCP server.
The coaching capabilities described on the integration page are available through the hosted connection.

Without a key, the local bridge can list its helpers; calls return setup instructions.

```bash
python3 trainerfu_agent.py connect
python3 trainerfu_agent.py guide
python3 trainerfu_agent.py status
```

## Questions from Trainerfu users

**Does Trainerfu have an official API or MCP server?**

The Cotlet.dev integration page reports that no general-purpose API reference, API-key setup, official MCP server or ChatGPT or Claude connector was found in vendor sources checked on 12 November 2026.

**What does Trainerfu AI Copilot cover?**

The integration page describes creating and editing workouts and training blocks. Cotlet.dev connects AI agents to account screens for client record reviews and follow-up work.

**How do I get access?**

Create an account at https://cotlet.dev/signup?app=trainerfu, open Trainerfu in the Cotlet Cloud Browser and sign in to your own account. Then enable it for agents and follow the connector steps in your console.

**Is this an official Trainerfu integration?**

No. Cotlet.dev is independent and is not affiliated with Trainerfu.

## Integration details

[Trainerfu tools and setup on Cotlet.dev](https://cotlet.dev/integrations/trainerfu-api-mcp-server?utm_source=github&utm_medium=readme&utm_campaign=trainerfu)

---

More: https://cotlet.dev/integrations/trainerfu-api-mcp-server?utm_source=github&utm_medium=readme&utm_campaign=trainerfu

Start free: https://cotlet.dev/signup?app=trainerfu&utm_source=github&utm_medium=readme&utm_campaign=trainerfu
