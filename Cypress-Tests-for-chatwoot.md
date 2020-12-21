```
#prepare database
RAILS_ENV=test bin/rake db:drop
RAILS_ENV=test bin/rake db:create
RAILS_ENV=test bin/rake db:schema:load

# start chatwoot in test environment 
overmind start  -f Procfile.test RAILS_ENV=test
```

Load `localhost:5050` on your browser and ensure that chatwoot is working

```
# in separate window start cypress
yarn cypress open --project ./spec

```