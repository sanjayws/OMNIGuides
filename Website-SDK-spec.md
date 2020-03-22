Expose window.$chatwoot object while using SDK

```js
window.chatwootSettings = {
  hideMessageBubble: false,
  position: 'left'
}
```

### To trigger widget without displaying bubble

```js
window.$chatwoot.open()
```

### To set the user in the widget

```js
window.$chatwoot.setUser({
  email: 'email@example.com',
  customAttributes: {
    // any additional attributes you want to add to the user
    // eg: 
    //   accountId: '',
    //   userId: ''
  }
})
```

### To set labels on the conversation

```js
window.$chatwoot.addLabel('support-ticket')

window.$chatwoot.removeLabel('support-ticket')
```

### To refresh the session (use this while you logout user from your app)

```js
window.$chatwoot.reset()
```