## Accessing Rails console 

run the following command in your console from the root folder of your chatwoot rails app

```
RAILS_ENV=production bundle exec rails c
```

*if you running chatwoot in a docker container, you would need to access the shell inside your container first.*

### Caprover

```
docker exec -it $(docker ps --filter name=srv-captain--chatwoot-web -q) /bin/sh
```


## Creating Super Admin

1) In your rails console type the following to create a super admin.
```
s = SuperAdmin.create!(email: "admin@xyc.com", password: "yourpassword")
```
2) Access `yourchatwoot.com/super_admin`.

3) Authenticate and you can find Sidekiq option on the sidebar.
*In the latest versions of Chatwoot, Sidekiq access was moved to our super admin area*


