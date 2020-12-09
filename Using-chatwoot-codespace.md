## Steps

- create a codespace
- github will open up the codespace in vscode once build finishes
- edit the .env file and update values for postgres and redis hosts to localhost
- run 'bundle exec rake db:reset`
- start the rails server && webpacker in separate terminals

## To be fixed
- figure out how to get WebSockets working
- Clean up and document the implementation further