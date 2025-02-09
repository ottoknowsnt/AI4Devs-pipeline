Herramienta: GithubCopilot + Claude 3.5 Sonnet

#Prompt 1

@workspace Generate a pipeline that does the following:

Run backend tests
Generate a build of the backend
Deploy the build to EC2

#Prompt 2

Use easingthemes/ssh-deploy@main to deploy instead

#Prompt 3

Merge the build and test jobs and add caching to the build process

#Prompt 4

The backend does not start successfully: bash: line 2: pm2: command not found

#Prompt 5

@workspace The service starts in the remote machine, but not successfully:

Error: @prisma/client did not initialize yet. Please run "prisma generate" and try to import it again.
