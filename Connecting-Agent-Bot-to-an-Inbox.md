Chatwoot allows you to easily connect your bot logic into conversation handling via AgentBot APIs. 

Once you connect agent bot to an inbox, all the new conversations created in your inbox will initially be assigned 'bot' status. Chatwoot will send each conversation events to your bot URL as webhook events. To which your AgentBot can react through the chatwoot [APIs](https://www.chatwoot.com/developers/api/)


##  Connect an Agent Bot to an inbox

go to your chatwoot directory and ensure your local server is running.  Start a rails console in your directory.

```
bundle exec rails c
```

Inside the rails console, type the following commands to create an agent bot and get its access token. Save the retrieved token as you would need to use in when calling the chatwoot APIs

```
# specify a url when your bot logic resides
bot = AgentBot.create!(name: "Your Bot", outgoing_url: "http://localhost:8000")
bot.access_token.token
```

Connect Agent Bot to your inbox by running the following command

```
# Replace Inbox.first with Inbox.find(inbox_id) for specific inboxes
AgentBotInbox.create!(inbox: Inbox.first, agent_bot: bot)
```

You can also view an example implementation of [agent bots using rasa](https://github.com/chatwoot/rasa-agent-bot-demo).

Also, look into interesting ways to leverage [bot-message types](https://github.com/chatwoot/chatwoot/wiki/Creating-Bot-Messages-Types) on chatwoot.
