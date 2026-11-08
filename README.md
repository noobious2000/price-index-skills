# Price index skills

Two agent skills that let AI agents (Claude Code, Cursor, GitHub Copilot and
other tools that support Agent Skills) answer used-price questions from two
public price sites:

| Skill | Site | Answers |
|---|---|---|
| `golf-club-prices` | [golfclubindex.com](https://golfclubindex.com) | What a used golf club is worth, whether a listing is a good deal, the best used clubs under a budget. Figures are **completed eBay sales**. |
| `used-tool-prices` | [usedtoolindex.com](https://usedtoolindex.com) | What a used cordless power tool typically goes for, whether a listing is a good deal, used tools under a budget. Figures are **asking prices of live eBay listings**, with a new-on-eBay comparison. |

## Install

    npx skills add noobious2000/price-index-skills --skill golf-club-prices
    npx skills add noobious2000/price-index-skills --skill used-tool-prices

## Where the data comes from

- **golf-club-prices** uses the Golf Club Index MCP server
  (`https://app.golfclubindex.com/mcp?src=skill`, read-only, no sign-in, the
  same tools as the Golf Club Index connector below) or, without MCP, the
  site's public pages and `https://golfclubindex.com/llms.txt`.
- **used-tool-prices** reads Used Tool Index's public pages and
  `https://usedtoolindex.com/llms.txt`. It has no MCP server.

Both sites update their figures daily. Every answer cites the site and the page
it came from, with the date of its figures: the "Sold prices as of" date on
golfclubindex.com, the "Prices as of" date on usedtoolindex.com. The skills
never build shop or eBay links; they send people to the site's page, which
shows the current listings. Both sites may earn a commission when people buy
through those listings.

Nothing in this repository is secret, and neither skill sends anything about
the person: the golf skill sends only the club details in the question to our
price tool, and the used-tool skill only fetches public pages.

## Golf Club Index connector (MCP server)

The golf price tool is also a remote MCP server that any MCP client can connect
to directly. It is free, read-only and needs no account or sign-in.

- **Server URL (Claude):** `https://app.golfclubindex.com/mcp?src=claudedir`
- **Transport:** Streamable HTTP. **Authentication:** none.
- **In Claude:** Settings > Connectors > Add custom connector, paste the URL.

### Tools (all read-only)

| Tool | Use it for | Returns |
|---|---|---|
| `golf_used_value` | What a used club is worth or should sell for | Fair used price range (25th percentile to median of completed eBay sales), average sale, number of sales, 30-day trend, live asking prices where available, data date, link to the club's page |
| `golf_best_used_under` | The best used clubs of a type under a budget, optionally one brand | Ranked list (model, average sale price, number of sales) and a link to the full page |
| `find_used_deals` | Live listings priced below what a club usually sells for | Up to 5 live eBay listings below the club's median sold price: title, condition, price, usual price and the gap, date checked, and a link. Iron sets are full sets only (4-PW or 5-PW, with or without AW) |

### Example prompts

- "What's a used TaylorMade Stealth 2 driver worth?"
- "Best used Ping irons under $500?"
- "Find me a deal on a used Titleist Vokey SM9 wedge."

### Data, links and disclosure

Figures come from Golf Club Index's own daily dataset of completed and live eBay
listings, gathered through eBay's APIs. Answers link to golfclubindex.com pages.
`find_used_deals` links each listing through app.golfclubindex.com, which counts
the click and forwards to the eBay listing; **Golf Club Index may earn a
commission (eBay Partner Network) on purchases made through those links**, and
every deals answer says so. The server stores no personal data and no
conversation content: it counts tool calls, link clicks and the connecting
client's name per day.

- Privacy: https://golfclubindex.com/privacy
- Methodology: https://golfclubindex.com/methodology
- Support: https://golfclubindex.com/contact

## Layout

    skills/golf-club-prices/SKILL.md
    skills/used-tool-prices/SKILL.md

The files are maintained in the Golf Club Index repository
(`docs/agent-skill/`) and copied here.
