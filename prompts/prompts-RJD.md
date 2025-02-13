# Prompts 

## Copilot (GPT 4o)

### Prompt 1

@workspace Hello, can you talk to me about this project, what does it do and a little bit at technical level too

### Prompt 2

@workspace what tests does my project have for both backend and frontend and how can i run them

### Prompt 3

Exclude dist/ from Jest Execution

## ChatGPT 4o

### Prompt 1

I'm trying to connect to an EC2 instance using my `.pem` file and I'm getting the error shown in my terminal. How do I go through and connect?

### Prompt 2

I need to configure secrets on my GitHub repository to connect to my EC2 instance and execute GitHub Actions.

### Prompt 3

Act as a DevSecOps expert and help me create a GitHub Action to deploy my project **AI4DEVS-PIPELINE** on my EC2 instance when a commit is made on `main` or a PR is merged on `main`. I don't know much about this, so let's work slowly step by step.

### Prompt 4

My action is timing out trying to connect to the EC2 instance using an SSH command, help me fix it.

### Prompt 5

At step 2, when rerunning my action, my error changed to:
```log
Run ssh -o StrictHostKeyChecking=no -i private_key.pem $EC2_USER@$EC2_HOST << ‘EOF’
Pseudo-terminal will not be allocated because stdin is not a terminal.
Warning: Permanently added ‘***’ (ED25519) to the list of known hosts.
Load key “private_key.pem”: error in libcrypto
@: Permission denied (publickey,gssapi-keyex,gssapi-with-mic).
Error: Process completed with exit code 255.
```

### Prompt 6

I got a `.pem` key when I was creating my EC2 instance that I'm using to connect from my PC to my instance through SSH. I also generated `github-actions-key.pub` and `github-actions-key` files. Which file is which, and what should we add to my repository? And what should my YAML file reference?

### Prompt 7

I think this is working now. Let's proceed further and make this better. Before we do though, can this application be deployed and tested from my local browser?

### Prompt 8

Instead of binding it to `0.0.0.0` and opening it for everyone, can we do a configuration that allows only me to access it for a test?

### Prompt 9

I added my IP to my EC2, opening port `3000`. What is our next step? My action `Deploy to EC2` is still running just in case and has been running for 7 minutes now, but it doesn’t look like it's stuck. What should we do now?

### Prompt 10

I cannot connect to my instance anymore. It's timing out. I have a budget set to `$1 USD` on my Amazon account. Could it be that I already reached the amount with these tests?

### Prompt 11

Oh, I can connect again. Something else caused it then, but I don't know what it was. Shall we proceed?

### Prompt 12

My problem seems to be with CPU utilization. What can we do about it? It hung when GitHub Action was executed, and the last command I executed before running into this problem again was `npm run build`.

### Prompt 13

I'm getting an error when running the backend on the EC2 instance that I don't get locally.

### Prompt 14

My EC2 backend started at port `3010`, what did we have to do from here?

### Prompt 15

As this is a test to try and deploy through GitHub Actions, we won't auto-start on reboot. Also, we can skip Nginx, but we need to continue. The objective is deploying automatically on `main` update (either by commit push or pull request merge). Consider our EC2 instance has given us problems, probably due to low resource allocation (free tier or low budget), when providing the next steps.

So, what's our goal?

### Prompt 16

Before automating the deployment through GitHub, shall we try to deploy ourselves within the EC2 and try reaching the application from my browser?

### Prompt 17

Our GitHub Action log is showing a fail running Cypress:
```log
Error: Action failed. Missing package manager lockfile. Expecting one of package-lock.json (npm), pnpm-lock.yaml (pnpm) or yarn.lock (yarn) in working-directory /home/runner/work/AI4Devs-pipeline/AI4Devs-pipeline
```

### Prompt 18

It's all working now. To finish this test, which was part of a study session I'm running, can you create a markdown document listing all the prompts I used?