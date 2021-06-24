## Steps

- create a codespace
- GitHub will open up the codespace in vscode once the build finishes
- In the ports section in the visual studio make 3000,3025,8025 open to public
- edit the .env file
  - update frontend URL with the public URL for port 3000
  - update values for `postgres`, `mailhog` and `redis` hosts to localhost
- run 'bundle exec rake db:reset`
- run `yarn`
- run `overmind start -f Procfile.dev`
