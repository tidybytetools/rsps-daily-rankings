# RSPS daily rankings (RuneScape private servers)

A free, daily snapshot of the RuneScape private server (RSPS) rankings published by
[RuneScape Private Servers](https://runescapeprivateservers.com/), an independent RSPS toplist.
Each row is one server that had votes tracked on the day of the snapshot, in rank order.

- Live leaderboard: https://runescapeprivateservers.com/leaderboard/
- Source files (refreshed every day): https://runescapeprivateservers.com/data/rsps-rankings.csv and https://runescapeprivateservers.com/data/rsps-rankings.json
- Server pages (uptime history, vote button, website check): linked from every row (`page_url`)

## Files

| File | What it is |
| --- | --- |
| `rsps-rankings.csv` | Today's ranking (UTF-8, comma-separated, header row) |
| `rsps-rankings.json` | The same rows plus metadata (date, license, how rank is calculated, row count) |
| `history/rsps-rankings-YYYY-MM-DD.csv` | One file per day, added by the daily workflow, so you can follow rank changes over time |

## Columns

| Column | Type | Meaning |
| --- | --- | --- |
| `date` | date (YYYY-MM-DD, UTC) | Day the ranking was built |
| `rank` | integer | Position on the leaderboard that day (1 = top) |
| `server_name` | string | Server name as listed |
| `votes` | integer | Votes tracked for the server: votes on runescapeprivateservers.com plus votes counted on public RSPS toplists the site crawls daily |
| `category` | string | Main category (for example OSRS, 317, 718, Custom, PvP, Eco). `General` if the listing gives none |
| `categories` | string | Every category the server is listed under, separated by `; ` |
| `page_url` | URL | The server's page on runescapeprivateservers.com |

How rank works: rank is by popularity, which is valid votes on runescapeprivateservers.com this month times 10, plus
votes counted on public RSPS toplists. The `votes` column holds the raw vote count, without that weighting, so
two servers can have close vote counts but different ranks. Servers with no tracked votes are left out (no zero rows).
Paid ads and sponsored banners never change rank.

What this dataset does not contain: player counts, reviews, revenue or anything self-reported that the site
cannot check. Category labels come from the servers' own listings.

## Update schedule

The site rebuilds its rankings once a day at about 10:15 UTC (4:15 AM US Central in winter).
`.github/workflows/daily-update.yml` runs every day at 11:45 UTC. It downloads both files, checks that they are
real (correct header, more than 10 rows, valid JSON), commits them only if something changed, and adds the day's CSV to `history/`.
If the repository has an `HF_TOKEN` secret, the same files are also pushed to the Hugging Face dataset
[`runescapeprivateservers/rsps-daily-rankings`](https://huggingface.co/datasets/runescapeprivateservers/rsps-daily-rankings).
Without the secret that step is skipped and the run still succeeds.

## License and attribution

[Creative Commons Attribution 4.0 International (CC BY 4.0)](https://creativecommons.org/licenses/by/4.0/).
You can share and adapt the data for any purpose, including commercial use, as long as you credit the source with a link:

> Data: [RuneScape Private Servers](https://runescapeprivateservers.com/) (CC BY 4.0)

## Quick start

```python
import pandas as pd
df = pd.read_csv("https://runescapeprivateservers.com/data/rsps-rankings.csv")
print(df.head(10)[["rank", "server_name", "votes", "category"]])
```

## Contact

Corrections, removal requests or questions: https://runescapeprivateservers.com/about.html
Server owners can claim and update their listing on the site.

RuneScape and Old School RuneScape are trademarks of Jagex Ltd. This dataset and the site are not affiliated with or endorsed by Jagex.
