# How to connect DistroKid to Claude Code, ChatGPT and any AI agent

**Yes, Claude, ChatGPT and other AI agents can work in your DistroKid account.** DistroKid has no public API. Cotlet.dev connects your own DistroKid account to any AI agent, so the AI checks releases, earnings and metadata when you ask in plain words.

## What you can ask

> Which of my releases are live on Spotify and Apple Music, and which are still pending?

> What did I earn last month per release and per store?

> Check the credits and lyrics on my new single before release day.

> List my releases that have no YouTube Content ID.

> When does my next DistroKid renewal come up?

## Connect in 2 minutes

Get your API key at https://cotlet.dev/app and export it as `COTLET_API_KEY`.

### Claude Code

```bash
claude mcp add --transport http cotlet https://cotlet.dev/mcp/v1 --header "Authorization: Bearer $COTLET_API_KEY"
```

### ChatGPT

Settings → Apps → add connector URL `https://cotlet.dev/mcp/v1`, then sign in with Cotlet.dev. No API key needed.

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

## Run it locally (stdio)

This repo is a real MCP server. It speaks MCP over stdio, lists its DistroKid tools without any key, and forwards every tool call to the hosted Cotlet.dev server. The hosted URL above stays the recommended way. Use this when your client only starts local servers.

```json
{"mcpServers":{"distrokid":{"command":"uvx","args":["distrokid-mcp"],"env":{"COTLET_API_KEY":"your-key"}}}}
```

Or with Docker:

```bash
docker build -t distrokid-mcp .
docker run -i --rm -e COTLET_API_KEY distrokid-mcp
```

Tools: `distrokid_guide`, `distrokid_status`, `distrokid_open`, `distrokid_read`, `distrokid_click`, `distrokid_type`, `distrokid_close`. Without `COTLET_API_KEY` a tool call answers: "Set COTLET_API_KEY. Get a key at https://cotlet.dev/app".

## Command line

Python 3.10+, nothing else to install. From PyPI:

```bash
pip install distrokid-mcp        # or run it once: uvx distrokid-mcp connect
distrokid-mcp connect
```

Or straight from this repo:

```bash
export COTLET_API_KEY="your-key"
python3 distrokid_agent.py connect   # ready config for Claude Code, Cursor, ChatGPT
python3 distrokid_agent.py status    # is DistroKid ready in your Cotlet.dev account
python3 distrokid_agent.py guide     # DistroKid screens and sign-in link
python3 distrokid_agent.py read      # open DistroKid, read the page, close the browser
python3 distrokid_agent.py tools     # list Cotlet.dev tools
python3 distrokid_agent.py serve     # start the stdio MCP server (same as no argument)
```

## Questions from DistroKid users

**Does DistroKid have an API?**

DistroKid has no public API for artists. Cotlet.dev works in your own DistroKid account, so your AI agent can check releases and earnings without one.

**How do I connect DistroKid to ChatGPT?**

Add Cotlet.dev as an app in ChatGPT (Settings → Apps, connector URL `https://cotlet.dev/mcp/v1`), sign in to DistroKid once in your Cotlet.dev Cloud Browser, and ask ChatGPT in plain words. No code and no DistroKid API key.

**Is there a way to use Claude with DistroKid?**

Yes. In Claude Code run the one-line `claude mcp add` command above; in the Claude app add `https://cotlet.dev/mcp/v1` as a custom connector. Claude then works in your own DistroKid account.

**Is there a DistroKid MCP server?**

DistroKid has no official MCP server. Cotlet.dev is a hosted MCP server that works in DistroKid for you, 24/7, with Claude, ChatGPT, Cursor, Codex, n8n, Make and Zapier.

## Find it on

- [DistroKid on Cotlet.dev](https://cotlet.dev/integrations/distrokid-api-mcp-server?utm_source=github&utm_medium=readme&utm_campaign=distrokid&utm_content=find)
- [PyPI package distrokid-mcp](https://pypi.org/project/distrokid-mcp/)
- [Glama](https://glama.ai/mcp/servers/cotlet-connect/distrokid-mcp)
- [LobeHub](https://lobehub.com/mcp/cotlet-connect-distrokid-mcp)
- [Odel](https://odel.app/modules/cotlet/distrokid)
- [mcpbeat](https://mcpbeat.com/mcp-servers/cotlet/distrokid/)
- [Step-by-step guide (PDF) on Internet Archive](https://archive.org/details/cotlet-connect-distrokid-to-ai-agents-guide)

## Also works with

- [Mangomint MCP](https://github.com/cotlet-connect/mangomint-mcp)
- [Wanderlog MCP](https://github.com/cotlet-connect/wanderlog-mcp)
- [SmugMug MCP](https://github.com/cotlet-connect/smugmug-mcp)
- [Garmin Connect MCP](https://github.com/cotlet-connect/garmin-mcp)
- [Housecall Pro MCP](https://github.com/cotlet-connect/housecall-pro-mcp)
- [Medium MCP](https://github.com/cotlet-connect/medium-mcp)
- [Crexi MCP](https://github.com/cotlet-connect/crexi-mcp)
- [LinkedIn MCP](https://github.com/cotlet-connect/linkedin-mcp)
- [EstimateOne MCP](https://github.com/cotlet-connect/estimateone-mcp)
- [Google Search Console MCP](https://github.com/cotlet-connect/google-search-console-mcp)
- [Lichess MCP](https://github.com/cotlet-connect/lichess-mcp)
- [Strava MCP](https://github.com/cotlet-connect/strava-mcp)
- [StreamElements MCP](https://github.com/cotlet-connect/streamelements-mcp)
- [Meetup MCP](https://github.com/cotlet-connect/meetup-mcp)
- [AccuRanker MCP](https://github.com/cotlet-connect/accuranker-mcp)
- [GetYourGuide MCP](https://github.com/cotlet-connect/getyourguide-mcp)
- [Idealista MCP](https://github.com/cotlet-connect/idealista-mcp)
- [Riverside MCP](https://github.com/cotlet-connect/riverside-mcp)
- [Udemy MCP](https://github.com/cotlet-connect/udemy-mcp)
- [Faire MCP](https://github.com/cotlet-connect/faire-mcp)
- [Buildertrend MCP](https://github.com/cotlet-connect/buildertrend-mcp)
- [Fresha MCP](https://github.com/cotlet-connect/fresha-mcp)
- [Booksy MCP](https://github.com/cotlet-connect/booksy-mcp)
- [BookingKoala MCP](https://github.com/cotlet-connect/bookingkoala-mcp)
- [Milanote MCP](https://github.com/cotlet-connect/milanote-mcp)
- [Partiful MCP](https://github.com/cotlet-connect/partiful-mcp)
- [Contractor Foreman MCP](https://github.com/cotlet-connect/contractor-foreman-mcp)
- [Pixieset MCP](https://github.com/cotlet-connect/pixieset-mcp)
- [GlossGenius MCP](https://github.com/cotlet-connect/glossgenius-mcp)
- [ZenMaid MCP](https://github.com/cotlet-connect/zenmaid-mcp)
- [FieldEdge MCP](https://github.com/cotlet-connect/fieldedge-mcp)
- [Phorest MCP](https://github.com/cotlet-connect/phorest-mcp)
- [DINGG MCP](https://github.com/cotlet-connect/dingg-mcp)
- [Invoice Simple MCP](https://github.com/cotlet-connect/invoice-simple-mcp)
- [PhotoShelter MCP](https://github.com/cotlet-connect/photoshelter-mcp)
- [RazorSync MCP](https://github.com/cotlet-connect/razorsync-mcp)
- [ShootProof MCP](https://github.com/cotlet-connect/shootproof-mcp)
- [Invoice2go MCP](https://github.com/cotlet-connect/invoice2go-mcp)
- [Appointy MCP](https://github.com/cotlet-connect/appointy-mcp)
- [Contractor+ MCP](https://github.com/cotlet-connect/contractor-plus-mcp)
- [Teachers Pay Teachers MCP](https://github.com/cotlet-connect/teachers-pay-teachers-mcp)
- [Bloom MCP](https://github.com/cotlet-connect/bloom-mcp)
- [All apps connected through Cotlet.dev](https://github.com/cotlet-connect)

---

More: https://cotlet.dev/integrations/distrokid-api-mcp-server?utm_source=github&utm_medium=readme&utm_campaign=distrokid

Start free: https://cotlet.dev/signup?app=distrokid&utm_source=github&utm_medium=readme&utm_campaign=distrokid
