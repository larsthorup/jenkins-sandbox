# jenkins-sandbox

Run a local Jenkins CI server against a GitHub repository

## Installation

- Verify Java is at version 11
  - `java --version`
- Download `jenkins.war` into `./bin` from https://jenkins.io/
- Download `ngrok.exe` into `./bin` from https://ngrok.com/
- Authorize NGrok: `./bin/ngrok authtoken <YOUR_AUTHTOKEN>`

## Run Jenkins

- Run Jenkins
  - `java -jar ./bin/jenkins.war --httpPort=8080`
- Open http://localhost:8080/
- Follow instructions:
  - Unlock
  - Install suggested plugins

## Run NGrok

- Connect: `./bin/ngrok http -hostname=xpqf.eu.ngrok.io -region=eu 8080`
- Open https://xpqf.eu.ngrok.io/

## Create job

- Create job:
  - New item, "jenkins-sample-project", Multibranch Pipeline
  - Add source (GitHub: https://github.com/larsthorup/jenkins-sample-project)
  - Save

## TODO

- Configure GitHub to trigger a build
- Configure Jenkins to set build status
