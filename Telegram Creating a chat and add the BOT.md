
### 1. Telegram Bot & Telegram Group

1. **Open Telegram and Search for the "BotFather"**

Open your Telegram app and search for the "BotFather" bot. This is the official bot provided by Telegram for creating and managing other bots.

2. **Start a Chat with BotFather**

Start a chat with the BotFather by clicking on the "Start" button.

3. **Create a New Bot**

Use the `/newbot` command to create a new bot. Follow the instructions provided by the BotFather.

plaintextCopy code

`/newbot`

The BotFather will guide you through the process and ask you to provide a name and username for your new bot.

4. **Copy Token**

Once your bot is created, the BotFather will provide you with a token. Copy this token as it will be used to authenticate your bot with the Telegram API.

 
 5. **Create a New Group**

Telegram > Group
add the bot in to the created group


### 2. Chat ID

Go to URL and you will see this 

https://api.telegram.org/bot<botToken>/getUpdates


``` JSON
{
    "ok": true,
    "result": []
}
```
this means that the bot is working

Now send message in the create group tagging the bot

``` CMD
/my_id @NotifyMateBot
```

refresh the URL

https://api.telegram.org/bot<botToken>/getUpdates

output
```JSON
{
    "ok": true,
    "result": [
        {
            "update_id": 893295108,
            "message": {
                "message_id": 2,
                "from": {
                    "id": 6549483636,
                    "is_bot": false,
                    "first_name": "Yogesh"
                },
                "chat": {
                    "id": -4136951514, #ChatID
                    "title": "Whatsup",
                    "type": "group",
                    "all_members_are_administrators": true
                },
                "date": 1711067781,
                "text": "/my_id @NotifyMateBot",
                "entities": [
                    {
                        "offset": 0,
                        "length": 6,
                        "type": "bot_command"
                    },
                    {
                        "offset": 7,
                        "length": 14,
                        "type": "mention"
                    }
                ]
            }
        }
    ]
}
```

you will get the chat id

use can use this URL to send message to the group using the bot.
https://api.telegram.org/bot<botToken>/sendMessage?chat_id=<chatID>

