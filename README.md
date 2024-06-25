# Asset Wallet

A Telegram Bot with wallet functionality for crypto-assets. It tracks your assets and displays charts and reports on demand. Additionally, users can toggle volatility notifications to alert them when the market price of their assets changes rapidly. Financial data is queried through the Binance API.

## Requirements

This bot is intended for use by a single user and requires a host platform to run (e.g., Raspberry Pi) along with API keys for a Telegram Bot and a Binance account. Here are guides for obtaining the [API keys from Binance](https://www.binance.com/en/support/faq/360002502072) and [creating a new Telegram bot](https://core.telegram.org/bots#6-botfather) to obtain its API token.

The bot is designed to handle limited requests simultaneously, making it suitable for a single user or a small group of users. Multiple concurrent requests may result in delays or unexpected outputs.

The code has been tested on Python 3.9.5. Install the required dependencies with:

```sh
pip install python-telegram-bot 
pip install python-binance 
pip install mplfinance
pip install numpy
pip install pandas 
```

**Note:** If hosting this program on a Raspberry Pi, ensure that Python 3 is installed, as the default may be Python 2.7.x.

## How to Startup the Bot

Once the dependencies are installed and the API keys are available, format the file `data/api_keys.txt` as follows (you may need to create `api_keys.txt` depending on the repository status):

```
telegram_bot_token
binance_api_public_key
binance_api_private_key
```

Now, you are all set! Run the `main.py` file with Python:

```sh
python main.py
```

If the bot is launched correctly, you should see these lines:

```
>> [Current Date and Time]-BOT:  Loading Telegram bot: SUCCESS
>> [Current Date and Time]-BOT:  Loading Binance Client: SUCCESS
>> [Current Date and Time]-BOT:  Callbacks initialized. Polling started
```

## Usage

Once the bot is up and running, the main menu is always available with the `/home` command.

### Home Menu

Here is an overview of the main functions of the bot:

- **💰Set Wallet:** Specify your crypto assets in terms of quantity and buy-price, allowing the bot to calculate profits/losses based on the current price.
- **💵My Wallet💵:** Displays a wallet report and charts of the crypto assets on different timescales.
- **💹Check Asset💹:** Displays the chart for any cryptocurrency on any timescale supported by Binance (see the "🚁Help" command for the list of supported queries). This function does not require a wallet.
- **🔔Notifications:** Receive daily reports of your wallet and/or notifications when the current price for the assets in your wallet increases or decreases rapidly.

Check the "🚁Help" button or type `/help` in the chat for live information from the bot.

## Supplementary Information

- The charts sent by the bot are saved in a daily buffer in the `savedfigs` folder, which is emptied nightly at 00:00. The graphs are always available from the Telegram chat.
- The user's wallet is saved as a CSV file in the `data/wallets` folder with the filename syntax: `data/wallets/xxxxxxxxx.csv` (where `xxxxxxxxx` is the Telegram ID of the user).
- Notification preferences are saved in the `data/notification_settings.csv` file with a clear syntax.
- Daily notifications of wallet reports are sent at 9:00 PM (one daily notification) and 12:00 AM (two daily notifications) every day.
- Major bot operations are logged in the console with a datetime stamp and the user ID.