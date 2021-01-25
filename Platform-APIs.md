Chatwoot lets you add omnichannel customer communication experience easily into your existing product. 


Platform APIs : [https://www.postman.com/chatwoot/workspace/chatwoot-apis](https://www.postman.com/chatwoot/workspace/chatwoot-apis)

## Usage 

### Creating Platform App

From rails console, create a platform app and obatain the access token required for the APIs

```
app = PlatformApp.create(name: 'name')
app.access_token.token
```

### Preparing your system

Implement the following logic into your system on account/User creating to sync auth info to chatwoot.

- Create an Account using the `Platform/Account` API
- Create a User using the `Platform/User` API
- Create an Account User using the `Platform/Account/AccountUser` API
- Associate the User Id / Account Id values obatained from API into your user database

#### Existing Users

If you have existing users in your system, you can write a script that will iterate over your user info and make the above mentioned API calls.

### Authenticating a Synced User
Once the user finished authentication on your system.
- Call `Platform/User/Login` Chatwoot API to and redirect the user to chatwoot installation via sso URL returned

