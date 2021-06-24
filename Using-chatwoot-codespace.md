## Steps

- create a codespace
- github will open up the codespace in vscode once build finishes
- open up ports 3000,3025,8025 to public
- edit the .env file
  - update frontend URL with the public URL for port 3000
  - update values for postgres, mailhog and redis hosts to localhost
- run 'bundle exec rake db:reset`
- run `yarn`
- run `foreman start -f Procfile.dev`

## To be fixed
- figure out how to get WebSockets working
- Clean up and document the implementation further