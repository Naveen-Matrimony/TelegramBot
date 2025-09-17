# Telegram Chat Bot (Grok / xAI)

A minimal Telegram bot written in Python that forwards user messages to Grok (xAI) via its OpenAI-compatible Chat Completions API and replies with the model's answer. Includes simple per-chat memory (last 10 turns) and `/reset`.

## Features

- Chat with Grok using Telegram.
- Per-chat context memory (last 10 user/assistant turns).
- Commands: `/start`, `/help`, `/reset`.
- Config via environment variables and `.env`.

## Requirements

- Python 3.10+
- A Telegram Bot Token from BotFather
- xAI (Grok) API Key

## Setup

1. Clone or copy this project to your machine.
2. Create and activate a virtual environment (recommended).

   Windows (PowerShell):
   ```powershell
   python -m venv .venv
   .\.venv\Scripts\Activate.ps1
   ```

3. Install dependencies:
   ```powershell
   pip install -r requirements.txt
   ```

4. Create a `.env` file based on `.env.example` and fill in your keys:
   ```env
   TELEGRAM_BOT_TOKEN=1234567890:ABC-YourTelegramBotTokenHere
   XAI_API_KEY=xaik-YourGrokApiKeyHere
   # Optional overrides
   #XAI_BASE_URL=https://api.x.ai/v1
   #XAI_MODEL=grok-2-latest
   #SYSTEM_PROMPT=You are a helpful assistant.
   #MAX_TOKENS=512
   #TEMPERATURE=0.7
   ```

## Run the bot

From the project root:
```powershell
python -m src.bot
```

If everything is configured correctly, you'll see "Bot started" in the console. Open Telegram and send a message to your bot.

## Project structure

```
.
├─ requirements.txt
├─ .env.example
├─ README.md
└─ src/
   ├─ __init__.py
   ├─ bot.py          # Telegram bot entry point
   ├─ config.py       # Settings and .env loading
   └─ grok_client.py  # Minimal xAI Grok chat client (OpenAI-compatible)
```

## Notes

- The memory is ephemeral and in-process only; restarting the bot clears it.
- Replies are sent with Markdown parse mode. If you see Markdown parse errors for certain outputs, we can switch to plain text or escape more aggressively.
- The code uses `python-telegram-bot` v21 (async API).

## Troubleshooting

- If you get `TELEGRAM_BOT_TOKEN is not set` or `XAI_API_KEY is not set`, ensure your `.env` or environment variables are present before starting the bot.
- If you see HTTP errors from xAI, verify your API key is valid and the model name is correct.
- To reduce cost or verbosity, lower `TEMPERATURE` or set `MAX_TOKENS`.
