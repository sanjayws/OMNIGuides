# The chatwoot conversation data model


<img width="500px" alt="chatwoot data modeling" src="https://i.imgur.com/TRQOiy6.png">

## Data Models
- Contacts: _represents the contacts_
- Inboxes: _represent a particular inbox_
- Contact Inboxes: _connects a contact to the inbox with the source id_
- Conversations: _A session holding messages of a particular issues/ period_

## Associations 

### Inbox 
Any channel which you connect in chatwoot like you website, facebook, email etc will create an associated Inbox.

### Contact 
Represents a Person in your chatwoot CRM. a contact can have conversations in multiple inboxes via the contact Inbox relationship. The contact models helps to agregate conversations from variaous inboxes belonging to a single identity. 

### Contact Inbox 
This model ties a Contact & Inbox using the appropriate `source_id`. The `source_id` could be the identifier hash in case of a webwidget, `twitter_id` in case of a twitter profile and `email` in case of email channel.  

When an external conversation comes in, it gets mapped to the appropriate contact if system can find a contact inbox with the mentioned source id. If no contact Inboxes are present the system creates a new contact inbox and a contact. 

ideas : 
- Your email/twitter/facebook inbox would only have on contact inbox between each contact and each inbox
- In webwidget case, there could be multiple contact inboxes between each contact and the inbox. This could occur in case where same user chats from different broweser sessions. ex: User using chrome, switching to firefox on next session. 

### Conversations 
Conversation Creation uses `source_id` to tie the session and the messages together 

----


# Import Contacts from your exisiting CRM / Software 

If you are integrating chatwoot to an existing system or bringing in data from another system. Use the following.

## Use the API 
APIs : https://www.postman.com/chatwoot/workspace/chatwoot-apis
( /application apis/contacts/import)

- api_access_token should be an administrators token. 
- the csv headers should match the key attributes [ identifier, email, name, phone number ] 
- Everything else other than key attributes will get updated to the jsonb colum custom attributes. this is a good place to tie your custom fields for the contact.

## Script in ruby

if you want to do specific customizations or build additional associations like contact_inbox associations do the import via a ruby script.

```ruby
# set up the account to which you are bringing in the contact
account = Account.find(1)

# replace the `data_import.import_file.download` with your csv source info
CSV.parse(data_import.import_file.download, headers: true).each do |row|
  # building a new contact and assigning attributes
  c = account.contact.new
  c.name = row[:name]
  c.identifier = row[:identifier]
  # custom attributes lets you store your custom fields
  c.custom_attributes = {
    val1 = row[:val1],
    val2 = row[:val2]
  }
  c.save!
end

```


## Keeping The system in sync 

If you are using chatwoot along with another system, the contacts creation happens in the other system. Keep the contacts in sync to chatwoot using the contact creation API, ever time a contact gets created/ updated. 

APIs : https://www.postman.com/chatwoot/workspace/chatwoot-apis
- ( /application apis/contacts/create)
- ( /application apis/contacts/update)

---

# Custom Use Cases 

The chatwoot APIs let you build powerful custom workflows beyond what chatwoot provides out of the box. 

## Sending outbound messages

At the time of writing chatwoot doesn't allow you to trigger outbound messages. But lets take a look at this use case to build outbound messages through twilio using chatwoot APIs. 

connecting an external system containing a form to send an sms message to a contact via twilio. Connecting this system with chatwoot will let the owner to recieve the replies to the outbound messages and continue the conversation.

### Prerequisites 
1) **Sync the existing users and implement a mechanism to keep the new contacts synced using the instructions mentioned above**
2) **Create a twilio Inbox in chatwoot**
3) **Create contact Inboxes for the contact**

#### Using APIs

Create contact inboxes for existing contact running a script. Implement mechanism for creating contact inbox for the newer contacts

APIs : https://www.postman.com/chatwoot/workspace/chatwoot-apis
( /application apis/contacts/contact_inbox/create)

#### Script in ruby to do intial sync in bulk

```ruby
account = Account.find(1)

account.contacts.each do |contact| 
  cinbox = contact.contact_inboxes.new
  cinbox.inbox_id = 2 # could be your twilio inbox 
  cinbox.source_id = contact.phone_number # (ensure its pattern +132423)
  cinbox.save!
end
```

## Creating outbound conversations

### Use the API to create conversation

APIs : https://www.postman.com/chatwoot/workspace/chatwoot-apis ( /application apis/conversations/create)
the source id parameter will be the twilio phone number in this case. 

### Send the outboud message using API or redirect the user to chatwoot
Redirect the user to chatwoot conversation UI so they can type and send the message or use the APIs
APIs : https://www.postman.com/chatwoot/workspace/chatwoot-apis ( /application apis/conversations/send message)
use the above mentioned conversation ID 