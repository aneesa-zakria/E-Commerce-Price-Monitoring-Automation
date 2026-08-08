# E-Commerce Price Monitoring Automation

An autonomous [n8n](https://n8n.io) workflow that tracks e-commerce product prices, logs historical data, and uses AI agents to detect and alert on meaningful price drops — replacing manual price-checking entirely.

## What it does

1. **Trigger** — runs on a schedule (no manual intervention needed)
2. **Scrape** — sends parallel HTTP requests to target product pages and extracts price/title via HTML parsing
3. **Validate** — filters out empty or malformed scrape results
4. **Log** — merges both data streams, processes them via a Python code node, and appends each entry to a Google Sheet (building a historical price log over time)
5. **Analyze** — an AI Agent (OpenAI) reviews each product's current price against its historical log to judge whether it's a genuine price drop
6. **Alert** — if the AI agent flags a significant drop, a Slack message is sent; routine price changes are logged silently without spamming the channel

## Requirements

To import and run this workflow, you'll need:

| Service | Used for |
|---|---|
| [n8n](https://n8n.io) (self-hosted or cloud) | Running the workflow |
| Google Sheets account | Historical price logging |
| OpenAI API key | AI-based price drop analysis |
| Slack workspace + OAuth app | Alert delivery |

## Setup

1. Import `E-Commerce Price Monitoring Automation.json` into n8n via **Workflows → Import from File**
2. Reconnect credentials for each node (Google Sheets, OpenAI, Slack) — the exported file does **not** include your credentials, only references to them
3. Update the **HTTP Request** nodes with the product URLs you want to track
4. Update the **Google Sheets** nodes to point to your own spreadsheet
5. Adjust the **Schedule Trigger** interval to your preferred check frequency
6. Activate the workflow

## Notes

- CSS selectors for price/title extraction are tuned for eBay listing pages — you'll need to adjust these for other marketplaces
- The AI agent's alert threshold is prompt-driven, not a fixed percentage — refine the system prompt if you want stricter or looser drop detection
- This is a personal automation project; use responsibly and in line with the target site's terms of service when scraping

## License

MIT (or your preferred license)
