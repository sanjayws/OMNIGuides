## Instructions

### Creating Codespace

- Head over to your codespaces section in GitHub and create a codespace for `chatwoot:chore/codespace`
- GitHub will open up the codespace in VSCode once the build finishes

### Booting for the  First Time
- In the ports tab in the visual studio, add `3000`, `3035`, `8025`  and make them public

### Development Workflow
- start rails server by running `overmind start -f Procfile.dev`
- load the public URL for port 3000, and your chatwoot instance will available to test the changes


### Notes
- You can access the emails using the public URL for Mailhog (port 8025)
- When using a ruby debugger, use `overmind connect backend`, or `overmind connect worker`
- if you see webpack manifest error, wait a minute for the asset complication to finish

