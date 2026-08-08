# E-Commerce Price Monitoring & AI Alert System

An autonomous [n8n](https://n8n.io) workflow that tracks e-commerce product prices, logs historical data, and uses AI agents to detect and alert on meaningful price drops — replacing manual price-checking entirely.

---

## What It Does

1. **Trigger** — Runs on a custom schedule with zero manual intervention required.
2. **Scrape** — Sends parallel HTTP requests to target product pages and extracts product titles and prices via HTML parsing.
3. **Validate** — Filters out empty, missing, or malformed scrape results to guarantee data integrity.
4. **Log** — Merges data streams, processes items via a Python code node, and appends each entry to Google Sheets to build a historical price log over time.
5. **Analyze** — Leverages an OpenAI-powered AI Agent to review current pricing against historical spreadsheet logs to determine if a genuine price drop has occurred.
6. **Alert** — Dispatches targeted Slack notifications only when significant deals or price drops are detected, allowing routine checks to complete silently without spamming your channels.

---

## Workflow Architecture

```text
[Schedule Trigger] 
       │
       ├──► [HTTP Request 1] ──► [HTML Extract] ──► [Validation] ──┐
       │                                                         ├──► [Merge] ──► [Python Script] ──► [Google Sheets Log] ──► [AI Agent] ──► [Slack Alert]
       └──► [HTTP Request 2] ──► [HTML Extract] ──► [Validation] ──┘

```

---

## Prerequisites & Tech Stack

To run and deploy this workflow, ensure you have access to the following services and accounts:

| Service / Tool | Purpose |
| --- | --- |
| **[n8n](https://n8n.io)** (Self-hosted or Cloud) | Workflow orchestration engine |
| **Google Sheets** | Long-term historical price logging |
| **OpenAI API Key** | AI-driven price drop evaluation and analysis |
| **Slack Workspace & OAuth App** | Real-time alert delivery |
| **Python Integration** | Data formatting and preparation node |

---

## Step-by-Step Setup Guide

1. **Import the Workflow:** Download `E-Commerce Price Monitoring Automation.json` and import it into your n8n instance via **Workflows → Import from File**.
2. **Reconnect Credentials:** Re-link your personal credentials for each node (**Google Sheets**, **OpenAI**, and **Slack**) — exported workflows contain credential references, not authentication secrets.
3. **Configure Targets:** Update the **HTTP Request** nodes with the specific e-commerce product URLs you wish to track.
4. **Link Spreadsheet:** Update the **Google Sheets** nodes to reference your own Google Sheet template.
5. **Set Schedule:** Adjust the **Schedule Trigger** node interval to match your preferred check frequency (e.g., daily or hourly).
6. **Activate:** Save your configurations and toggle the workflow to **Active**.

---

## Important Notes & Customization

* **Marketplace Selectors:** The default CSS selectors for price and title extraction are tuned for **eBay listing pages**. If monitoring other e-commerce marketplaces (e.g., Amazon, Walmart), you will need to update the HTML extraction node selectors accordingly.
* **AI Thresholds:** The AI agent's sensitivity is prompt-driven rather than bound to a strict fixed percentage. Feel free to refine the system prompt within the agent node to adjust drop detection strictness.
* **Responsible Scraping:** This is a personal automation utility. Please use responsibly and ensure your scraping frequency respects the target website's terms of service and robots.txt policies.

---

## License

Distributed under the **MIT License**. Feel free to use, modify, and expand upon this project.
