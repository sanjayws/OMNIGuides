## Instructions

### Creating Codespace

- Head over to your codespaces section in GitHub and create a codespace for `{you_chatwoot_repo}:{your_branch}`
- GitHub will open up the codespace in VSCode once the build finishes

### Development Workflow
- start rails server by running `overmind start -f Procfile.dev`
- load the public URL for port 3000, and your chatwoot instance will be available to test the changes

### Notes
- You can access the emails using the public URL for Mailhog (port 8025)
- if the public URL fails to load. In codespace port mapping, remove the existing mapping for the port. Add the port again. Make it public and retry again
- When using a ruby debugger, use `overmind connect backend`, or `overmind connect worker`
- if you see webpack manifest error, wait a minute for the asset complication to finish

