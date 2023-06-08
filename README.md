# PapayaCoders_Telegram_Chatgpt_Bot
# ChatGPT Telegram Bot

English ｜ (README.md)

A ChatGPT bot for Telegram based on Node.js. Support both browserless and browser-based APIs.


## Features


- Support for both browserless (official, unofficial) and browser-based APIs
- Support for both private and group chats
- Work in privacy mode (the bot can only see specific messages)
- Bot access control based on user and group IDs
- Reset chat thread and refresh session with command
- Queue messages to avoid rate limit
- Typing indicator, Markdown formatting, ...
- Cloudflare bypassing and CAPTCHA automation (for the browser-based API)
- Customize bot identity and behavior (by setting `api.official.systemMessage`)
- User-friendly logging

## Usage

### Differences between the three types of APIs

> Thank @transitive-bullshit for making this easy-to-understand table!

| Type         | Free?  | Robust?  | Quality?                |
| -------------| ------ | -------- | ----------------------- |
| `official`   | ❌ No  | ✅ Yes   | ✅ Real ChatGPT models |
| `unofficial` | ✅ Yes | ☑️ Maybe | ✅ Real ChatGPT         |
| `browser`    | ✅ Yes | ❌ No    | ✅ Real ChatGPT         |

- `official`: Uses the `gpt-3.5-turbo` model by default with the official OpenAI chat completions API (official, robust approach, but it's not free)
- `unofficial`: Uses an unofficial proxy server to access ChatGPT's backend API in a way that circumvents Cloudflare (uses the real ChatGPT and is pretty lightweight, but relies on a third-party server and is rate-limited)
- `browser` (not recommended): Uses Puppeteer to access the official ChatGPT webapp (uses the real ChatGPT, but very flaky, heavyweight, and error prone)

> **Warning**
>
> There are rumors that OpenAI may ban your account if you continue to use the `unofficial` and `browser` API. Use it at your own risk.

### Start the server

#### Option 1: Node
To get started, follow these steps:

1. Clone this project.
2. Create `local.json` under the `config/` folder. You can copy the `config/default.json` as a template.
3. Modify the `local.json` following the instructions in the file. The settings in `local.json` will override the default settings in `default.json`.
  - Set `api.type` to `official` if you want to use the browserless official API. Then provide your [OpenAI API Key](https://platform.openai.com/overview) and other settings. You can refer to [this](https://github.com/transitive-bullshit/chatgpt-api#usage---chatgptapi) for more details. Note that this will cost your credits.
  - Set `api.type` to `unofficial` if you want to use the browserless unofficial API. Then provide your OpenAI access token ([how to get your access token?](https://github.com/transitive-bullshit/chatgpt-api#access-token)) and other settings. You can refer to [this](https://github.com/transitive-bullshit/chatgpt-api#usage---chatgptunofficialproxyapi) for more details.
  - Set `api.type` to `browser` if you want to use the browser-based API (not recommended). Then provide the OpenAI / Google / Microsoft credentials and other settings. You can refer to [this](https://github.com/transitive-bullshit/chatgpt-api/tree/v3#authentication) and [this](https://github.com/transitive-bullshit/chatgpt-api/blob/v3/docs/classes/ChatGPTAPIBrowser.md#parameters) for more details. Make sure you have a Chromium-based browser installed.

Then you can start the bot with:

```shell
pnpm install
pnpm build && pnpm start
```
### Chat with the bot in Telegram

To chat with the bot in Telegram, you can:

- Send direct messages to the bot (this is not supported in groups)
- Send messages that start with the specified command (e.g., `/chat` or the command you specified in the json config file)
- Reply to the bot's last message

> **Note** Make sure you have enabled the privacy mode of your bot before adding it to a group, or it will reply to every message in the group.

The bot also has several commands.

- `/help`: Show help information.
- `/reset`: Reset the current chat thread and start a new one.
- `/reload` (admin required, browser-based API only): Refresh the ChatGPT session.

> **Note** When using a command in a group, make sure to include a mention after the command, like `/help@chatgpt_bot`.


## Advanced

### Running the bot using browser-based API on a headless server

You can use [Xvfb](https://www.x.org/releases/X11R7.6/doc/man/man1/Xvfb.1.xhtml) to create a virtual framebuffer on a headless server and run this program:

```shell
xvfb-run -a --server-args="-screen 0 1280x800x24 -nolisten tcp -dpi 96 +extension RANDR" pnpm start
```

We recommend you to use Google auth to avoid the complicated login Recaptchas. If you use a OpenAI account, you may have to use nopecha or 2captcha or manually solve the Recaptcha (by connecting to the display server using x11vnc). For more details about CAPTCHA solving, please refer to [the api repository](https://github.com/transitive-bullshit/chatgpt-api/tree/v3#captchas).

## Credits

- [ChatGPT API](https://github.com/transitive-bullshit/chatgpt-api): Node.js client for the unofficial ChatGPT API.
- [ChatGPT](https://github.com/acheong08/ChatGPT): ChatGPT API for Python.
- [Node.js Telegram Bot API](https://github.com/yagop/node-telegram-bot-api): Telegram Bot API for NodeJS.
- [🤖️ chatbot-telegram](https://github.com/Ciyou/chatbot-telegram): Yet another telegram ChatGPT bot.

## LICENSE

[MIT License](LICENSE).

**Leave a star ⭐ if you find this project useful.**
