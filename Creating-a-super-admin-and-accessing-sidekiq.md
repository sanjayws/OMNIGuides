In the latest versions of chatwoot, sidekiq access was moved to our super admin area

1) In your rails console type the following to create a super admin
```
s = SuperAdmin.create!(email: "admin@xyc.com", password: "yourpassword")
```
2) Access `yourchatwoot.com/super_admin`

3) authenticate and you can find sidekiq option on the sidebar