# Metrics time series

This branch is machine-written by `.github/workflows/metrics.yml`.
Do not edit by hand. Each daily run writes:

- `metrics/snapshots/YYYY-MM-DD.json` — full snapshot
- `metrics/history.csv`               — append-only rolling CSV

Data sources: npm registry downloads API, Docker Hub v2 API,
GitHub repo + traffic API.

## Traffic data (clones, views, referrers, popular paths)

The default `GITHUB_TOKEN` in Actions lacks the `administration:read`
scope that GitHub requires for `/traffic/*` endpoints, so those
fields will be `null` in the snapshot and empty in the CSV.

To enable traffic capture, create a fine-grained PAT with
`Repository permissions → Administration: Read` for this repo and
save it as the `METRICS_TOKEN` secret. The workflow already reads
it preferentially over `GITHUB_TOKEN`.
