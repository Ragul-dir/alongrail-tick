# alongrail-tick

The clock for Alongrail's outreach queue, and nothing else.

Alongrail sends its outreach letters from a queue on its own server. The
queue needs something to wake it every few minutes. These scheduled
workflows do that: each one calls `https://www.alongrail.com/api/outreach/tick`
with a bearer token held as the Actions secret `CRON_SECRET`. The token is
not in any file here. Without it the endpoint answers 404.

- `tick.yml` — every five minutes.
- `backstop.yml` — once an hour, in case GitHub drops the five-minute runs.
- `keepalive.yml` — once a month. GitHub turns off a public repository's
  schedules after 60 days without activity; this re-enables the two
  workflows and, if the last commit is 25 days old or more, adds an
  empty commit.

If the clock stops, the Alongrail daily digest says so after two hours of
silence. To restart it: open Actions, enable `tick` and `backstop` if
GitHub disabled them, and run `keepalive` by hand.

The application code lives in a private repository.
