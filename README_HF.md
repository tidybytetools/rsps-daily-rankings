---
license: cc-by-4.0
pretty_name: RSPS Daily Rankings (RuneScape Private Servers)
language:
- en
tags:
- runescape
- rsps
- osrs
- private-servers
- gaming
- mmorpg
- rankings
- tabular
size_categories:
- n<1K
configs:
- config_name: default
  data_files:
  - split: train
    path: rsps-rankings.csv
- config_name: history
  data_files:
  - split: train
    path: history/*.csv
---

# RSPS Daily Rankings (RuneScape Private Servers)

Daily snapshot of the RuneScape private server (RSPS) leaderboard from
[RuneScape Private Servers](https://runescapeprivateservers.com/), an independent RSPS toplist.
One row per server with votes tracked that day, in rank order. Updated every day.

- Live leaderboard: https://runescapeprivateservers.com/leaderboard/
- Source files: https://runescapeprivateservers.com/data/rsps-rankings.csv and `.json`

## Columns

| Column | Meaning |
| --- | --- |
| `date` | Build date (UTC, YYYY-MM-DD) |
| `rank` | Leaderboard position that day (1 = top) |
| `server_name` | Server name as listed |
| `votes` | Votes tracked: votes on runescapeprivateservers.com plus votes counted on public RSPS toplists crawled daily |
| `category` | Main category (OSRS, 317, 718, Custom, PvP, Eco, ...; `General` if none) |
| `categories` | All listed categories, `; `-separated |
| `page_url` | The server's page on runescapeprivateservers.com |

Rank is by popularity, which is valid votes on the site this month times 10, plus public toplist votes. `votes` is the
raw count, without that weighting. Servers with no tracked votes are left out. Ads never change rank. There are no player counts,
reviews or other figures the site cannot check.

The `history` config holds one CSV per day (`history/rsps-rankings-YYYY-MM-DD.csv`).

## License

CC BY 4.0. Please credit: **Data: [RuneScape Private Servers](https://runescapeprivateservers.com/) (CC BY 4.0)**

RuneScape and Old School RuneScape are trademarks of Jagex Ltd. Not affiliated with or endorsed by Jagex.
