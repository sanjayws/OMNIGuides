## Architecture 

<img src="https://i.imgur.com/7WjRCJ1.png">


## Overview

AgentBot is a web service connected to a chatwoot inbox and can act as a bot handling customer queries.

- The connected agent bot receives events like `widget_triggered`, `message_created`, `message_updated` etc based on customer action
- The agent bot can process the information received and come up with a response. 
- The agent bot can also rely on external system APIs to fetch additional user information like order status, booking trigger, etc
- The agent bot can also rely on services like rasa, dialogflow, lex etc to do intent detection
- The agent bot can post the generated response back into the widget by calling chatwoot APIs like message_create
- The agent bot can toggle a conversation status to open to hand off the conversation to a human agent
- The agent bot can continue to listen to open conversations and see if it can provide contextual information to the support agent.

## Use Cases

- Businesses with high volume customer support queries can use a bot to further authenticate and filter queries before passing to agents
- Ecom websites can hook up  the bot to their existing database and provide order/shipping status
- News/Content websites can leverage card messages to send recommendations via bot
- Hotel/Movie booking websites can handle the booking via bot

## Implementation Examples
1) https://github.com/chatwoot/dialogflow-agent-bot-demo : example hotel booking implementation using dialogflow
2) https://github.com/chatwoot/rasa-agent-bot-demo : example implementation using rasa