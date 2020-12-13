# jenkins-sandbox

Run a local Jenkins CI server against a GitHub repository

## Installation

- Verify Java is at version 11
  - `java --version`
- Download `jenkins.war` into `./bin` from https://jenkins.io/
- Download `ngrok.exe` into `./bin` from https://ngrok.com/
- Authorize NGrok: `./bin/ngrok authtoken <YOUR_AUTHTOKEN>`

## Configure GitHub

- GitHub, Account, Settings, Developer Settings, Personal Access Tokens
- Scopes: `admin:repo_hook`, `repo`

## Run NGrok

- Reserve subdomain: `xpqf` in region `eu`
- Connect: `./bin/ngrok http -hostname=xpqf.eu.ngrok.io -region=eu 8080`

## Run Jenkins

- Run Jenkins
  - `java -jar ./bin/jenkins.war --httpPort=8080`
- Open http://localhost:8080/
- Follow instructions:
  - Unlock
  - Install suggested plugins
  - Create first admin user
  - Jenkins URL: https://xpqf.eu.ngrok.io/
- Open https://xpqf.eu.ngrok.io/

## Configure Jenkins for GitHub

- GitHub Personal Access Token
- Credentials, System, Global, Add
  - ID: "GITHUB_ACCESS_TOKEN", secret text
  - ID: "Github Personal Access Token", (username with) password credential
- Configure System, Add Github Server, https://api.github.com
  - Credentials, GITHUB_ACCESS_TOKEN
  - Manage hooks
- Configure System, Github API Usage,
  - Never check rate limit

## Create job in Jenkins for GitHub project

- New item, "jenkins-sample-project", Multibranch Pipeline
- Add source, GitHub
  - Add GitHub credentials
  - https://github.com/larsthorup/jenkins-sample-project
- Save

## Configure project on GitHub for Jenkins

- GitHub, project, settings, webhooks, add
- https://xpqf.eu.ngrok.io/github-webhook/
- Github, project, settings, branches
  - \*
  - Require status checks to pass before merging
  - continuous-integration/jenkins/pr-merge
  - Allow Deletions
