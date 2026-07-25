# Mm Strategy Bot

Market-making / short-squeeze signal bot that scans funding, open interest, taker ratios, regimes, and metrics for selected crypto markets. It is used for monitoring MM-style strategy conditions, not generic notifications.

## Features

- Scans market regime, OI, funding, and taker long/short ratio inputs.
- Provides Telegram commands for scan, metrics, regime, status, and help.
- Documents setup for exchange data APIs and runtime service deployment.

## Architecture

- **Repository:** `MilaArtyNew/mm-strategy-bot`
- **Primary stack:** Python, systemd, Railway
- **Entrypoints and scripts:**
  - `main.py`
- **Notable dependencies:** `apscheduler`, `httpx`, `python-dotenv`, `python-telegram-bot`

## Configuration

Configure the service with environment variables. Do not commit real secrets to the repository.

- `BINANCE_API_KEY` — required or optional runtime configuration. See deployment environment for the actual value.
- `BINANCE_API_SECRET` — required or optional runtime configuration. See deployment environment for the actual value.
- `TELEGRAM_CHAT_ID` — required or optional runtime configuration. See deployment environment for the actual value.
- `TELEGRAM_TOKEN` — required or optional runtime configuration. See deployment environment for the actual value.

## Setup

```bash
git clone https://github.com/MilaArtyNew/mm-strategy-bot
cd mm-strategy-bot
python3 -m venv .venv
source .venv/bin/activate
pip install -r requirements.txt
```

## Running Locally

```bash
python main.py
```

## Bot Commands

- `/help` — Show help and available commands.
- `/metrics` — Show strategy or project metrics.
- `/regime` — Show current market regime.
- `/scan` — Run a scan.
- `/start` — Start the bot and show the main entry message.
- `/status` — Show current service or strategy status.

If a command requires extra input and the argument is missing, the bot should ask a follow-up question instead of failing silently.

## Deployment Notes

- Keep secrets in the deployment platform environment variables, not in Git.
- Use the default branch as the source of truth for deployments.
- Check logs after every deployment and verify the `/status` or health endpoint when available.
- If the project uses a scheduler, verify timezone assumptions and idempotency before enabling it in production.

## Operational Notes

- Review logs after startup for missing environment variables or API authentication errors.
- Keep command names in English and document every user-facing command in this README.
- For Telegram bots, `/help` should list the same commands documented here.
- Inline buttons should edit the original message with the final status rather than sending duplicate messages.

## Troubleshooting

- **Bot does not respond:** verify the bot token, webhook/polling mode, and chat permissions.
- **Missing data:** check API keys, rate limits, and upstream service status.
- **Deployment starts but exits:** inspect platform logs for missing environment variables or import errors.
- **Commands differ from README:** update the command list here and in the bot command menu at the same time.

## Security

- Never commit `.env` files, API keys, private keys, Telegram tokens, or session strings.
- Use `.env.example` for placeholders only.
- Rotate any credential that was accidentally committed.
