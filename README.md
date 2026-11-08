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
  same two tools as the Golf Club Index app in ChatGPT) or, without MCP, the
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

## Layout

    skills/golf-club-prices/SKILL.md
    skills/used-tool-prices/SKILL.md

The files are maintained in the Golf Club Index repository
(`docs/agent-skill/`) and copied here.
